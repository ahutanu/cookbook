# Fine-Tuning GPT-4 for PII Classification on Azure OpenAI Service

This notebook demonstrates how to **fine-tune a GPT-4 model** on Azure OpenAI Service for a privacy-focused text classification task (e.g., identifying PII vs non-PII text). It covers Azure setup, data preparation, fine-tuning, monitoring, evaluation, and deployment steps. The examples use Python and Azure CLI, with clear guidance for each step.

## Prerequisites

- **Azure subscription** with permissions to create resources and deploy Azure OpenAI models (Contributor role).  
- **Azure CLI** installed and logged in (`az login`) [oai_citation:0‡learn.microsoft.com](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/create-resource#:~:text=Sign%20in%20to%20the%20Azure,CLI).  
- **Azure OpenAI Service** access (request access if needed).  
- **Python 3.8+** with required libraries (`openai`, `azure-storage-blob`, `requests`, `tiktoken`, etc.).  
- **Resource planning:** Estimate fine-tuning costs and training data size [oai_citation:1‡learn.microsoft.com](https://learn.microsoft.com/en-us/azure/ai-services/openai/tutorials/fine-tune#:~:text=We%20recommend%20reviewing%20the%20pricing,incur%20the%20hourly%20hosting%20cost). At least 50 high-quality examples are recommended [oai_citation:2‡learn.microsoft.com](https://learn.microsoft.com/en-us/azure/ai-services/openai/tutorials/fine-tune#:~:text=While%20these%20three%20examples%20are,training%20examples%20to%20be%20successful).

## 1. Azure Resource Setup

First, create an Azure Resource Group and an Azure OpenAI resource using the Azure CLI. You can also create a Storage Account for datasets. For example:

```bash
# Create a resource group (replace names/locations as needed)
az group create \
  --name MyResourceGroup \
  --location eastus

# Create an Azure OpenAI service resource (replace placeholders)
az cognitiveservices account create \
  --name MyOpenAIResource \
  --resource-group MyResourceGroup \
  --location eastus \
  --kind OpenAI \
  --sku s0 \
  --subscription <YOUR_SUBSCRIPTION_ID>
```

These commands correspond to Azure’s documentation for creating resource groups and OpenAI resources. After creation, retrieve your OpenAI endpoint and keys:

```bash
# Get the endpoint URL
az cognitiveservices account show \
  --name MyOpenAIResource \
  --resource-group MyResourceGroup \
  --query "properties.endpoint" -o tsv

# Get an API key (key1)
az cognitiveservices account keys list \
  --name MyOpenAIResource \
  --resource-group MyResourceGroup \
  --query "key1" -o tsv
```

Store the endpoint (e.g., https://<MyOpenAIResource>.openai.azure.com/) and API key for later (or set them as environment variables AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_API_KEY).

Next, create an Azure Storage Account and a Blob container to hold the training/validation files:

```bash
# Create a general-purpose storage account
az storage account create \
  --name mystorageacct \
  --resource-group MyResourceGroup \
  --location eastus \
  --sku Standard_LRS \
  --kind StorageV2

# Create a blob container (requires Blob Data Contributor role)
az storage container create \
  --account-name mystorageacct \
  --name trainingdata \
  --auth-mode login
```

This storage account will hold our JSONL dataset for fine-tuning. According to Azure guidelines, training data files must be JSONL, UTF-8 encoded, and < 512 MB. For large datasets, importing from Blob Storage is recommended.

2. Prepare Training Data (JSONL)

We now generate a small synthetic dataset labeled for PII vs Non-PII classification. Each example will be formatted with a system prompt, a user query (the text to classify), and the assistant’s response (the label). Azure OpenAI requires chat-completion JSONL format. For example:
```json
{"messages": [
    {"role": "system", "content": "You are a privacy classifier that labels text as PII or Non-PII."},
    {"role": "user", "content": "Text: 'My SSN is 123-45-6789' - classify it."},
    {"role": "assistant", "content": "PII"}
]}
```

In code, we can create such a JSONL file as follows:

```python
import json

# Example dataset: list of (text, label) pairs
examples = [
    ("My SSN is 123-45-6789", "PII"),
    ("Contact me at john.doe@example.com", "PII"),
    ("The weather today is sunny", "Non-PII"),
    ("We will meet at the public park.", "Non-PII"),
    ("Credit Card Number: 4111 1111 1111 1111", "PII"),
    ("Hello, how are you?", "Non-PII"),
    ("Passport: X12345678", "PII"),
    ("See you tomorrow!", "Non-PII")
]

# Create chat-format JSONL entries
training_data = []
for text, label in examples[:-2]:  # use first 6 for training
    msg = {
        "messages": [
            {"role": "system", "content": "You are an assistant that classifies text as PII or Non-PII."},
            {"role": "user", "content": f"Text: '{text}'. Classify it as PII or Non-PII."},
            {"role": "assistant", "content": label}
        ]
    }
    training_data.append(msg)

validation_data = []
for text, label in examples[-2:]:  # last 2 as validation
    msg = {
        "messages": [
            {"role": "system", "content": "You are an assistant that classifies text as PII or Non-PII."},
            {"role": "user", "content": f"Text: '{text}'. Classify it as PII or Non-PII."},
            {"role": "assistant", "content": label}
        ]
    }
    validation_data.append(msg)

# Write to JSONL files
with open("training_set.jsonl", "w", encoding="utf-8") as f:
    for record in training_data:
        f.write(json.dumps(record) + "\n")

with open("validation_set.jsonl", "w", encoding="utf-8") as f:
    for record in validation_data:
        f.write(json.dumps(record) + "\n")

print("Training examples written:", len(training_data))
print("Validation examples written:", len(validation_data))
```

This code creates training_set.jsonl and validation_set.jsonl in the required Azure format. We used at least 6 training examples (not ideal, but sufficient for this demo). The system prompt clarifies the role, and the label is the assistant’s content.

3. Upload Dataset to Azure Blob Storage

Upload the JSONL files to the blob container we created. You can use the Azure CLI or Python SDK. Using CLI:

```bash
# Upload training set
az storage blob upload \
  --account-name mystorageacct \
  --container-name trainingdata \
  --name training_set.jsonl \
  --file training_set.jsonl

# Upload validation set
az storage blob upload \
  --account-name mystorageacct \
  --container-name trainingdata \
  --name validation_set.jsonl \
  --file validation_set.jsonl
```

This stores the files in Azure Blob. As noted, large files should be uploaded via Blob to avoid multi-part upload issues. Azure OpenAI expects uploaded files to be < 512 MB and properly formatted.

4. Start Fine-Tuning Job

We use the Azure OpenAI Python SDK (OpenAI Python 1.x) to create a fine-tuning job. First, install or upgrade the OpenAI SDK if needed:

```bash
pip install --upgrade openai
```

Then, configure the client with your endpoint and key:

```python
from openai import AzureOpenAI
import os

# Replace with your endpoint and key
endpoint = "https://<MyOpenAIResource>.openai.azure.com/"
api_key = "<YOUR_API_KEY>"

client = AzureOpenAI(
    azure_endpoint=endpoint,
    api_key=api_key,
    api_version="2024-10-21"   # fine-tuning API version
)
```

Next, upload the JSONL files to the Azure OpenAI service (this returns file IDs):

```python
# Upload files for fine-tuning
with open("training_set.jsonl", "rb") as train_file:
    train_response = client.files.create(file=train_file, purpose="fine-tune")
training_file_id = train_response.id

with open("validation_set.jsonl", "rb") as val_file:
    val_response = client.files.create(file=val_file, purpose="fine-tune")
validation_file_id = val_response.id

print(f"Training file ID: {training_file_id}")
print(f"Validation file ID: {validation_file_id}")
```

According to Azure docs, you should use client.files.create(..., purpose="fine-tune") to upload training data. The returned IDs (file-...) are used in the fine-tuning job.

Now create the fine-tune job. Choose a base GPT-4 model (e.g., gpt-4o-mini-2024-07-18 if available). The model name must match Azure naming (dashes instead of dots). For example:

```python
response = client.fine_tuning.jobs.create(
    training_file=training_file_id,
    validation_file=validation_file_id,
    model="gpt-4o-mini-2024-07-18",  # Base GPT-4 model ID
    seed=42
)
job_id = response.id
print(f"Fine-tune job created. Job ID: {job_id}")
```

This call enqueues the fine-tuning job. The response.id is the job ID, which we can use to track progress.

5. Monitor Fine-Tuning Job

The fine-tuning process can take some time. You can poll the job status or use Azure AI Studio. For example, using the SDK:

```python
import time

# Poll job status
while True:
    status_resp = client.fine_tuning.jobs.get(job_id)
    status = status_resp.status
    print(f"Job status: {status}")
    if status in ("succeeded", "failed", "canceled"):
        break
    time.sleep(10)

print("Fine-tuning job completed with status:", status)
```

Azure returns job details including events and final model name once complete. You can also list all jobs or check events via client.fine_tuning.jobs.list() or the Azure portal. The SDK example above matches Azure guidance: use the job ID to monitor status.

When the job succeeds, the response will include the fine-tuned model name (e.g., gpt-4o-mini-2024-07-18:ft-<id>). Save this model ID for deployment.

6. Evaluate the Fine-Tuned Model

Once fine-tuning is done, test the model on new examples to verify it classifies correctly. First, deploy the fine-tuned model (see next section). Then use the deployed endpoint. For demonstration, suppose the deployment name is pii-classifier. Use the chat completion API to classify sample texts:

```python
# Example inference using the deployed fine-tuned model
sample_texts = [
    "The patient SSN is 987-65-4321",
    "It's raining outside today"
]

for text in sample_texts:
    completion = client.chat.completions.create(
        deployment_name="pii-classifier",
        messages=[{"role": "user", "content": f"Text: '{text}'. Classify as PII or Non-PII."}],
        temperature=0
    )
    label = completion.choices[0].message.content
    print(f"Text: '{text}' -> Model Prediction: {label}")

```
Here we use client.chat.completions.create(...) with temperature=0 for deterministic classification. Replace deployment_name with the actual deployed name. The model should ideally return “PII” for the first and “Non-PII” for the second. (Note: in Azure OpenAI, you must call the deployment name, not the underlying model name.)

7. Deploy the Fine-Tuned Model for Inference

To use the custom model in production, deploy it as a new model deployment. You can do this in the Azure portal or via API/CLI. For example, using Azure REST API (or CLI):
```python
import requests

# Example of deploying via Azure management REST API
token = "<YOUR_AZURE_ACCESS_TOKEN>"  # e.g. from `az account get-access-token`
subscription_id = "<YOUR_SUBSCRIPTION_ID>"
resource_group = "MyResourceGroup"
resource_name = "MyOpenAIResource"
deployment_name = "pii-classifier"
fine_tuned_model_name = "<gpt-4o-mini-2024-07-18.ft-XXXXXXXXXXXX>"  # from fine-tune job

deploy_url = (
    f"https://management.azure.com/subscriptions/{subscription_id}"
    f"/resourceGroups/{resource_group}/providers/Microsoft.CognitiveServices"
    f"/accounts/{resource_name}/deployments/{deployment_name}"
    f"?api-version=2024-10-21"
)
deploy_payload = {
    "sku": {"name": "standard", "capacity": 1},
    "properties": {
        "model": {
            "format": "OpenAI",
            "name": fine_tuned_model_name,
            "version": "1"
        }
    }
}
headers = {
    "Authorization": f"Bearer {token}",
    "Content-Type": "application/json"
}
resp = requests.put(deploy_url, headers=headers, json=deploy_payload)
print("Deployment response:", resp.status_code, resp.text)
```

In the above, replace <gpt-4o-mini-2024-07-18.ft-XXXXXXXXXXXX> with your actual fine-tuned model ID from the training job. This follows Microsoft’s example payload for deploying a fine-tuned model. The key is to set "model.name" to the fine-tuned model name (e.g., gpt-4o-mini-2024-07-18.ft-<id>). Once deployed (Standard SKU), the model is ready for inference.

Alternatively, you can use the Azure CLI to create a deployment if it supports specifying the fine-tuned model version, or simply use the Azure Portal Deployments tab.

Note: After deployment, use the deployment name (e.g., pii-classifier) in your API calls, not the underlying model name.

8. Inference with Deployed Model

With the model deployed, you can call it via the Azure OpenAI API. For chat models:
```python
response = client.chat.completions.create(
    deployment_name="pii-classifier",
    messages=[{"role": "user", "content": "Text: 'Email me at example@example.com'. Classify as PII or Non-PII."}],
    temperature=0
)
print("Prediction:", response.choices[0].message.content)
```
For completion-based calls (if using client.completions), you must provide the deployment name as the engine or use model= and set api_type="azure" and api_version. The key detail is to reference the deployment name as noted above.

Summary

This notebook demonstrated end-to-end fine-tuning of an Azure OpenAI GPT-4 model for a PII classification task. We covered:
	•	Setting up Azure resources via CLI.
	•	Preparing a JSONL dataset in chat format.
	•	Uploading data to Azure Blob Storage.
	•	Initiating a fine-tuning job using Azure’s Python SDK.
	•	Monitoring job status.
	•	Deploying the custom model.
	•	Performing inference with the fine-tuned model.

Each step follows Azure’s best practices and documentation. Be sure to manage your resources and clean up unused deployments or resource groups to avoid incurring extra costs.
```bash
# (Optional) Cleanup resources
# az cognitiveservices account delete --name MyOpenAIResource --resource-group MyResourceGroup
# az group delete --name MyResourceGroup
```
Sources: Azure OpenAI fine-tuning and deployment guides ￼ ￼ ￼ ￼; Azure CLI documentation ￼ ￼ ￼.

