# From Zero to AI Workflows

## A Complete Guide to Agent Skills & Multi-Agent Orchestration

*Everything you need to know to transform any process into a tested, scalable AI product — no programming required.*

---

## Welcome

You're about to learn something that will change how you think about work.

Not because the technology is complicated — it isn't. But because once you see the pattern, you'll start recognizing it everywhere: in your job, in your daily routines, in every repetitive process you've ever wished could just *happen* without you.

This guide will take you from knowing nothing about AI agents to understanding — deeply, practically, concretely — how to:

- **Teach** an AI agent any skill, using plain words
- **Test** that skill with scientific evidence, not guesswork
- **Improve** it automatically until it's excellent
- **Combine** multiple agents into teams that work together
- **Control** everything with safety limits and human oversight
- **Scale** from a single task to a full product

You don't need to be a programmer. You don't need a computer science degree. You don't need to understand how AI works internally.

You need to be able to explain what you want — clearly, step by step — in the same way you'd explain it to a talented new colleague on their first day.

If you can do that, you can do everything in this guide.

### How to Read This Guide

This guide has three parts that build on each other:

| Part | What You'll Learn | Analogy |
|------|-------------------|---------|
| **I. Agent Skills** | How to teach an AI agent to do one thing well | Writing a recipe |
| **II. Multi-Agent Workflows** | How to organize multiple agents into teams | Planning a kitchen |
| **III. The Integration** | How skills and workflows create products | Running a restaurant |

Each concept follows the same pattern: **What** it is → **Why** it matters → **How** it works. We'll use real-world analogies throughout, and every technical term gets explained the first time it appears.

Take your time. There's no test at the end. The goal is understanding, not memorization.

---

# Part I: The Foundation — Agent Skills

---

## Chapter 1: What Is an AI Agent?

### The Short Answer

An AI agent is a computer program that can understand instructions in plain language, make decisions, and take actions to complete tasks — like searching the internet, reading files, writing documents, or sending messages.

### The Longer Answer (With an Analogy)

Imagine you hired a brilliant new assistant. They're incredibly smart — they can read faster than any human, write in any style, analyze data in seconds, and work 24 hours a day without breaks.

But on their first day, they don't know *your* way of doing things.

They don't know that when you say "do a background check on this company," you mean a specific 8-step research process. They don't know that your reports always start with an executive summary. They don't know that you prefer bullet points over paragraphs.

They're capable of learning all of this — instantly — if someone just tells them.

That's what an AI agent is. The "someone who tells them" is you.

### What Makes an Agent Different from ChatGPT?

You might be thinking: "I already use ChatGPT / Claude / Copilot. How is an agent different?"

Here's the key distinction:

| | Chatbot | Agent |
|---|---------|-------|
| **You say** | "Write me a summary of this article" | "Research this company, check 8 sources, score them, and produce a Word document" |
| **It does** | One thing, right now, then waits | Multiple things, in sequence, making decisions along the way |
| **Memory** | Forgets everything after the conversation | Can remember instructions and use them every time |
| **Tools** | Can only chat | Can search the web, read files, run commands, send messages, create documents |
| **Scope** | Single response | Complete workflow |

A chatbot answers questions. An agent *does work*.

### Why This Matters to You

Every time you explain a process to a new team member — every time you write a how-to document — every time you think "I do this the same way every week" — you're describing something an agent could learn.

The question is: how do you teach it?

That's what skills are for.

---

## Chapter 2: What Are Agent Skills?

### The Recipe Analogy

Think about a recipe. A good recipe has:

- A **name** ("Chocolate Chip Cookies")
- A **description** of what it produces and when you'd use it
- A list of **ingredients** (what you need before starting)
- **Step-by-step instructions** (what to do, in what order)
- **Tips and warnings** ("Don't overmix the dough" / "If the cookies spread too much, chill the dough for 30 minutes")
- Expected **results** ("Makes 24 cookies, golden brown, slightly chewy in the center")

An **Agent Skill** is exactly this — but instead of teaching a human to bake, it teaches an AI agent to perform a task.

### What a Skill Actually Looks Like

A skill is a text file called `SKILL.md` — a simple document written in Markdown (a lightweight formatting language, like what you'd use in a chat message with *bold* and **italic**).

Here's a simplified example:

```
Name: competitor-analysis
Description: Produce a structured competitive analysis report 
on any market or industry. Use when asked to research competitors,
evaluate market positioning, or analyze competitive landscape.

# Instructions

When asked to analyze a market, follow this process:

1. Research the landscape across 6 tracks:
   - Market overview (size, growth rate, key trends)
   - Key players (top 5-10 competitors, market share)
   - Product comparison (features, pricing, positioning)
   - Strengths and weaknesses (per competitor)
   - Market gaps (underserved segments, opportunities)
   - Strategic recommendations (based on findings)

2. Score each competitor on 5 dimensions (1–5)

3. Produce a competitive positioning map

4. Deliver a strategic summary with actionable insights
```

That's it. Plain words. No code. No programming language. Just clear instructions that tell the agent exactly what to do.

### The Three Parts of Every Skill

Every skill has three essential components:

**1. The Header (What & When)**

This tells the agent what the skill does and when to use it:

- **Name**: A short, unique identifier (like `competitor-analysis`)
- **Description**: What the skill does, when it should be activated, and when it should *not* be activated

The description is crucial. It's like the sign on a specialist's office door. It helps the agent know: "This patient needs a cardiologist, not a dermatologist."

> **💡 Key Insight:** A good description includes both *triggers* (when TO use the skill) and *anti-triggers* (when NOT to use it). For example: "Use when asked to analyze a company for investment. Do NOT use for stock trading advice or portfolio allocation."

**2. The Instructions (How)**

This is the step-by-step process the agent follows. Write it exactly as you'd explain it to a smart colleague:

- Be specific ("Search at least 3 sources") not vague ("Do some research")
- Include decision points ("If revenue data is unavailable, note this as a risk")
- Describe the expected output ("Produce a report with executive summary, risk matrix, and verdict")

**3. The References (Supporting Material)**

For complex skills, you can include additional reference documents:

- Scoring rubrics ("How to rate product quality from 1 to 5")
- Methodology guides ("Which sources to trust and why")
- Templates ("What the final report should look like")
- Examples ("Here's what a good output looks like")

These live alongside the SKILL.md file in a `references/` folder, and the skill's instructions point to them when needed.

### Why Skills Matter

Here's what makes skills powerful:

**1. They're reusable.** Write a skill once, use it forever. Every time you ask the agent to do that task, it follows the same proven instructions.

**2. They're shareable.** A skill that works for you can work for anyone. You can share it with colleagues, publish it to a registry, or use it across different AI platforms.

**3. They're improvable.** Because a skill is just a text file, you can refine it over time. Found a gap? Add a step. Got better results with a different approach? Update the instructions.

**4. They're testable.** This is the game-changer. Unlike "I told the AI what to do and it seemed to work," skills can be scientifically tested with real data. More on this in Chapter 4.

**5. They're written in human language.** You don't need to learn a programming language. You need to be clear, specific, and thorough — skills that transfer directly from good management and good communication.

> **🎯 Try This (Thought Exercise):** Think about a task you do regularly at work. Something you've explained to others before. Now imagine writing it down as a skill: What would the name be? What triggers it? What are the steps? What does good output look like? You've just designed your first skill — in your head.

---

## Chapter 3: The Skill Lifecycle

### From Idea to Product: The Four Stages

Every skill goes through a lifecycle, much like any product:

```
Create → Test → Improve → Distribute
  ↑                          |
  └──────── Feedback ────────┘
```

Let's walk through each stage.

### Stage 1: Create

**What happens:** You write the SKILL.md file — the instructions that teach the agent what to do.

**How to do it well:**

1. **Start with the outcome.** What does "done" look like? Describe the finished product before describing the steps.

2. **Write for a smart stranger.** Your reader is intelligent but has never done this specific task. Don't assume knowledge — but don't over-explain universal concepts.

3. **Be directive, not descriptive.** Say "Search for the company's funding history on Crunchbase" — not "You might want to look into the company's funding."

4. **Include edge cases.** What should the agent do when information isn't available? When sources conflict? When the task is ambiguous?

5. **Specify the format.** "Produce a bullet-point summary" is clearer than "write a summary."

> **💡 Key Insight:** The single most common mistake in skill creation is being too vague. "Do thorough research" means nothing. "Search at least 3 independent sources, cross-reference founding dates, and flag any discrepancies" means everything.

### Stage 2: Test

**What happens:** You verify that the skill actually works — not with gut feeling, but with measurable evidence.

This is where most people stop. They write instructions, try them once, and say "seems fine." That's like taste-testing one cookie and declaring the entire recipe perfect.

Real testing means:

- Does the agent *understand* when to use this skill? (Trigger accuracy)
- Does the agent *follow* the instructions correctly? (Execution quality)
- Is the *output* actually good? (Result quality)
- Does it work *consistently*? (Reliability)

Chapter 4 covers this in full detail.

### Stage 3: Improve

**What happens:** Based on test results, you refine the skill — then test again.

This creates a virtuous cycle:

```
Test → Identify gaps → Fix instructions → Test again → Measure improvement
```

The key word is *measure*. You don't guess whether the skill got better. You compare scores: "Version 1 scored 64 out of 100. Version 2 scored 100 out of 100. Here's exactly what changed and why."

This is the difference between "I think it's better" and "the data proves it's better."

### Stage 4: Distribute

**What happens:** Your tested, proven skill is ready for the world.

Distribution can mean:

- **Personal use** — The skill lives in your workspace, and your agent uses it every day
- **Team sharing** — You share the skill file with colleagues who have their own agents
- **Public publishing** — You publish to a skill registry like github/awesome-copilot or your organization's repository, where others can discover and install your skill
- **Product integration** — The skill becomes a component in a larger automated workflow (more on this in Part II)

> **🎯 The Big Picture:** A skill is not a one-time prompt. It's a *living asset* — created, tested, improved, distributed, and maintained over time. Treat it like a product, because that's exactly what it can become.

---

## Chapter 4: Testing Skills with Evidence

This is where everything becomes real. Testing transforms a skill from "instructions I hope work" into "a proven capability backed by data."

### Why Testing Matters

Imagine a pharmaceutical company that creates a new medicine. Would you trust them if they said: "We gave it to one person and they felt better. Ship it!"?

Of course not. You'd expect clinical trials, control groups, measurable outcomes, peer review.

Skills deserve the same rigor — on a proportional scale. Not because they're life-or-death, but because *quality that isn't measured is quality that isn't real.*

### The Testing Tool: Waza

**What it is:** Waza (技 — a Japanese word meaning "technique" or "skill") is a command-line tool built by Microsoft for testing AI agent skills. Its tagline: *"The way of technique — measure, refine, master."*

**Why it exists:** Before Waza, testing a skill meant manually trying it and eyeballing the results. Waza makes testing scientific, repeatable, and automated.

**How it works:** You define tests in a simple configuration file (YAML), and Waza runs them through an actual AI agent, then evaluates the results against your criteria.

Think of Waza as a **quality assurance lab for AI skills**.

### Waza's Capabilities: The Complete Toolkit

#### 1. Compliance Checking (`waza check`)

**What it does:** Verifies that your skill file is properly structured — all required sections present, correct format, no broken links.

**Why it matters:** Just like a legal contract that's missing a signature page is invalid regardless of content, a skill missing key structural elements won't work properly.

**How it works:**
```
You run: waza check my-skill/
Waza reports: "9/9 spec compliance checks passed. Compliance: High."
```

**Real-world analogy:** A building inspector checking that your house has all required components (foundation, wiring, plumbing) before evaluating how nice the kitchen looks.

#### 2. Trigger Testing (`waza dev --scaffold-triggers`)

**What it does:** Verifies that the agent correctly identifies WHEN to use your skill — and when NOT to.

**Why it matters:** The best skill in the world is useless if the agent doesn't know when to activate it. If someone asks "analyze this company for investment" and the agent activates the recipe-writing skill instead, nothing else matters.

**How it works:** Waza generates test prompts based on your skill's description:
- **Positive triggers** (should activate): "Should I invest in this startup?" → ✅ Skill activates
- **Negative triggers** (should NOT activate): "Should I buy Tesla stock based on RSI?" → ✅ Skill stays silent

**Real-world analogy:** Testing a smoke detector. You want it to go off when there's smoke (true positive) and stay silent when someone's just cooking (true negative). A detector that goes off every time you make toast is as bad as one that doesn't go off during a fire.

**Real-world result:** A competitor analysis skill went from 75% trigger accuracy (missing valid analysis requests) to 100% after adding explicit trigger phrases to the description.

#### 3. Quality Evaluation with AI Judge (`prompt` grader)

**What it does:** Runs a real task through the agent, then has a *separate, independent* AI evaluate the output against specific criteria.

**Why it matters:** This is the "clinical trial" of skill testing. Instead of you deciding "that looks good," an impartial judge scores the output on defined dimensions.

**How it works:**
1. You define criteria: "Does the output include sourced evidence? Does it present pros and cons? Does it include a numerical score?"
2. Waza sends a real task to the agent (e.g., "Do a competitive analysis of the CRM market")
3. The agent produces real output using your skill
4. A separate AI judge evaluates the output against your criteria
5. You get a score: "4 out of 5 criteria met"

**Real-world analogy:** A mystery shopper. The restaurant doesn't know they're being tested. The shopper evaluates the experience against a rubric (greeting within 30 seconds, food served within 15 minutes, etc.) and produces an objective score.

**Real-world result:** A competitive analysis skill scored 5/5 on criteria including sourced evidence, balanced assessment, numerical scoring, gap identification, and actionable recommendations.

#### 4. Before/After Comparison (`waza compare`)

**What it does:** Runs the exact same tests on two versions of a skill and shows you precisely what improved, what regressed, and by how much.

**Why it matters:** Without comparison, "improvement" is subjective. With comparison, it's mathematical.

**How it works:**
```
You run: waza compare results-v1.json results-v2.json
Waza reports:
  Score:        0.64 → 1.00  (+0.36)
  Success Rate: 66.7% → 100% (+33.3%)
```

**Real-world analogy:** A sports coach reviewing game tape. "Last game you completed 64% of passes. This game, 100%. Here's what changed in your technique."

**Real-world result:** Version 1 of the skill scored 0.64 overall. Version 2 (with two small frontmatter changes) scored 1.00. The improvement was entirely attributable to better trigger phrases — proof that small, targeted changes can have large effects.

#### 5. Cross-Model Comparison

**What it does:** Runs the same skill with different AI "brains" (Claude, GPT, Gemini) and compares which performs best.

**Why it matters:** Not all AI models are equal at all tasks. One might be better at analytical work, another at creative writing. Testing across models finds the best fit.

**How it works:** Same test, same skill, different models. Waza produces a comparison table showing scores, success rates, and cost per model.

**Real-world analogy:** A taste test. Same recipe, different chefs. Which chef's version scores highest on the rubric?

#### 6. Automated Improvement (`waza dev`)

**What it does:** Analyzes your skill, identifies specific weaknesses, suggests improvements, and can automatically apply them.

**Why it matters:** Manual improvement requires expertise. Automated improvement democratizes quality — the tool knows the best practices and applies them for you.

**How it works:**
```
You run: waza dev my-skill/ --target high --auto
Waza reports: 
  Before: Compliance Low, 0 triggers, 0 anti-triggers
  After:  Compliance High, 5 triggers, 3 anti-triggers
  Changes: Added USE FOR phrases, added routing clarity, 
           fixed broken reference link
```

**Real-world analogy:** Grammarly for skill files. It doesn't just check spelling — it improves clarity, completeness, and structure.

**Real-world result:** A competitive analysis skill went from "Low" compliance to "High" compliance in a single automated pass, with only 58 additional tokens (words) added.

### The Testing Hierarchy

Here's how all the testing capabilities stack together, from fastest to most thorough:

| Level | Tool | What It Tests | Time | When to Use |
|-------|------|--------------|------|-------------|
| 1 | `waza check` | Structure & format | 1 second | Every edit |
| 2 | `waza dev --scaffold-triggers` | Trigger accuracy | 10 seconds | After changing description |
| 3 | `waza run` (mock) | Test configuration | 5 seconds | When writing new tests |
| 4 | `waza run` (copilot-sdk) | Real agent output | 1-15 minutes | Before declaring "done" |
| 5 | `waza compare` | Version improvement | After test run | After every improvement |

> **💡 Key Insight:** You don't need to run all levels every time. Quick structural checks (Level 1-2) happen with every edit. Full quality testing (Level 4-5) happens at milestones. This mirrors how software teams work: quick checks constantly, thorough testing before releases.

---

## Chapter 5: The AgentSkills Ecosystem

### You're Not Alone

Everything we've discussed so far — creating skills, testing them, improving them — you can do on your own. But you don't have to.

A thriving ecosystem already exists. Think of it as the difference between cooking every meal from scratch versus having access to a well-stocked grocery store AND the ability to cook from scratch. You want both.

### What Is agentskills.io?

**agentskills.io** is the official website for the **Agent Skills open format** — the specification that defines how skills are structured so that any compatible AI agent can use them. Think of it as the "rulebook" that ensures skills work the same way across different tools.

The site provides:

- **The specification** — the complete format definition for how skills must be structured
- **Best practices** — guidance for writing effective skills
- **Client implementation guides** — instructions for tool makers who want to support the format
- **The quickstart** — how to create your first skill

agentskills.io is *not* a marketplace or store. It's the open standard itself — supported by over 20 tools including GitHub Copilot, Claude Code, OpenAI Codex, Cursor, Gemini CLI, and many more.

### Skill Registries

In addition to the format specification, major technology companies maintain their own curated registries — collections of skills built by their teams and communities:

**Major registries:**

| Registry | Maintained By | Description |
|----------|--------------|-------------|
| agentskills.io | Community | The open format specification website |
| github/awesome-copilot | GitHub | Community-contributed skills, agents, and configurations for GitHub Copilot |
| microsoft/skills | Microsoft | Skills, MCP servers, and agents for grounding coding agents |
| anthropic/skills | Anthropic | Public repository for Agent Skills (Claude-focused) |
| openai/skills | OpenAI | Skills catalog for Codex |

### Choosing Skills Wisely

Not all published skills are worth installing. Here's a framework for evaluating them:

1. **Does it solve a real problem for you?** A skill for Kubernetes deployment is useless if you don't use Kubernetes.
2. **Is it well-structured?** Run `waza check` on it. Does it pass compliance?
3. **Does it have tests?** Skills with eval suites have been verified. Skills without them are unproven.
4. **Is it actively maintained?** Check the last update date and issue tracker.
5. **Does it conflict with your existing skills?** Two skills that both try to handle "analyze this company" will compete with each other.

### Publishing Your Own Skills

When you've created, tested, and proven a skill, you can give it back to the community:

1. Ensure it passes `waza check` with "High" compliance
2. Include an eval suite (even basic trigger tests)
3. Write a clear description with triggers and anti-triggers
4. Publish to a skill registry (like github/awesome-copilot) or your organization's internal repository

> **🎯 The Virtuous Cycle:** The more people create and share skills, the more everyone benefits. A skill you publish today might be the starting point for someone else's breakthrough tomorrow. And a skill someone else published might save you days of work.

### How Do Agents Actually "Use" Skills?

You might be wondering: if a skill is just a text file, how does the agent actually find and follow it?

The answer is elegantly simple. When an agent starts up, it scans a `skills/` directory on the system it runs on. It reads the **description** of every skill available. Then, when you give the agent a task, it matches your request against those descriptions and loads the relevant skill's full instructions.

It's like a doctor's reference library. The doctor doesn't memorize every medical textbook. But when a patient describes symptoms, the doctor knows which reference book to pull off the shelf and follow.

This is why the **description** field matters so much — it's the doctor's bookshelf label. A vague label means the agent grabs the wrong book. A precise label means the right book, every time.

### The Execution Engine: Copilot SDK

One more piece of the puzzle before we move on. We've talked about skills (instructions) and agents (the workers). But what actually *powers* the agents?

**The Copilot SDK** (Software Development Kit) is the engine under the hood. Built by GitHub, it's what connects the written instructions to an actual AI model (like GPT, Claude, or Gemini) and gives the agent the ability to take actions — search the web, read files, run commands.

Think of it this way:
- **Skill** = the recipe (what to do)
- **Agent** = the chef (who does it)
- **Copilot SDK** = the kitchen equipment (what makes it physically possible)

You don't need to interact with the SDK directly. It works behind the scenes. But knowing it exists helps you understand how everything connects.

---

# Part II: The Power Layer — Multi-Agent Workflows

---

## Chapter 6: Why One Agent Isn't Enough

### The Limits of a Solo Performer

In Part I, we taught a single agent to do a single task well. That's powerful — but it has limits.

Think about how real work actually happens. When a company evaluates a potential acquisition, does one person do everything alone? No. There's a research team, a financial analyst, a legal reviewer, a technical assessor, and an executive who makes the final call. Each person specializes. Each person checks the others' work.

A single AI agent doing everything alone has the same limitations as a single employee doing everything alone:

- **No checks and balances.** Nobody reviews their work
- **No specialization.** One agent trying to be an expert at everything is an expert at nothing
- **No parallelism.** Tasks that could happen simultaneously happen one after another
- **No human oversight.** The agent either does everything autonomously or nothing at all

Multi-agent workflows solve all of these problems.

### The Team Analogy

Instead of one overworked generalist, imagine an AI team:

| Role | What They Do | Human Equivalent |
|------|-------------|-----------------|
| Researcher | Gathers information from multiple sources | Research analyst |
| Reviewer | Checks quality against defined criteria | Quality assurance |
| Writer | Produces the final document | Technical writer |
| Approver | Makes go/no-go decisions | Manager |

Each "team member" is an AI agent with a focused role. They pass work between each other in a defined order. They can send work back for revision. And at critical decision points, a human steps in.

That's a multi-agent workflow.

---

## Chapter 7: What Are Multi-Agent Workflows?

### Definition

A **multi-agent workflow** is a structured sequence of steps where multiple AI agents collaborate to complete a complex task, with defined rules for how work flows between them.

Let's break that down:

- **Structured sequence** — The steps happen in a defined order, not randomly
- **Multiple AI agents** — Each step can be handled by a different agent with a different role
- **Collaborate** — Agents pass their output to the next agent as input
- **Complex task** — Something too big or too important for one agent alone
- **Defined rules** — Clear logic for what happens next: "If the quality score is above 90, proceed. If below 90, go back and revise."

### The Orchestrator: Conductor

**What it is:** Conductor is a CLI tool (built by Microsoft) that reads workflow definitions written in a simple text format called YAML, and executes them — managing the agents, passing data between them, enforcing limits, and tracking progress. It supports multiple AI providers including GitHub Copilot SDK and Anthropic's Agents SDK.

**Why the name:** Think of an orchestra conductor. The conductor doesn't play any instrument. But they know the entire score — who plays what, when they come in, how loud, how fast. Without the conductor, talented musicians produce noise. With the conductor, they produce music.

Conductor does the same thing for AI agents.

**How it works (simplified):**

1. You write a YAML file that describes your workflow:
   - Which agents exist and what each one does
   - What order they work in
   - What conditions determine the next step
   - What safety limits apply

2. You run: `conductor run my-workflow.yaml --input topic="whatever"`

3. Conductor executes the workflow, managing everything automatically

4. You get structured output — the final result in a clean format

### YAML: The Workflow Language

YAML (rhymes with "camel") is a simple text format for describing structured information. You already understand it intuitively:

```yaml
# This is a comment — Conductor ignores it

workflow:
  name: simple-research
  entry_point: researcher      # Which agent goes first

agents:
  - name: researcher
    prompt: "Research this topic: {{ workflow.input.topic }}"
    routes:
      - to: reviewer           # After researching, go to reviewer

  - name: reviewer
    prompt: "Review this research and score it 0-100"
    routes:
      - to: $end               # When done, end the workflow
```

That's a complete workflow. Two agents. One researches, the other reviews. When the reviewer is done, the workflow ends.

The `{{ workflow.input.topic }}` part is a **template** — it gets replaced with whatever topic you provide when you run the workflow. Like a form with a blank that gets filled in.

> **💡 Key Insight:** YAML is designed to be human-readable. If you can read the example above and roughly understand what it does, you can read (and write) workflows. The format is intentionally simple.

---

## Chapter 8: Workflow Patterns — The Complete Toolkit

This is the most important chapter in Part II. It covers every type of workflow pattern available, with real-world examples for each.

Think of these patterns as building blocks. Most real workflows combine two or more patterns. But understanding each one individually is essential before combining them.

### Pattern 1: Linear (Step by Step) ➡️

**What it is:** Agent A finishes → passes results to Agent B → passes results to Agent C → done.

**When to use it:** When each step depends on the output of the previous step, and you want a straightforward pipeline.

**Real-world analogy:** An assembly line. Station 1 welds the frame. Station 2 installs the engine. Station 3 paints the body. Each station needs the previous station's output before it can start.

**Example: Article Writing Pipeline**

```yaml
agents:
  - name: researcher
    prompt: "Research the topic: {{ workflow.input.topic }}"
    routes:
      - to: writer

  - name: writer
    prompt: |
      Write an article based on this research:
      {{ researcher.output.findings }}
    routes:
      - to: editor

  - name: editor
    prompt: |
      Edit this article for clarity and grammar:
      {{ writer.output.draft }}
    routes:
      - to: $end
```

**Flow:** Researcher → Writer → Editor → Done

**Why this pattern:** Simple, predictable, easy to debug. You know exactly where work is at any moment.

---

### Pattern 2: Loop (Iterative Refinement) 🔄

**What it is:** Agent A produces something. Agent B evaluates it. If it's not good enough, Agent B sends it back to Agent A with feedback. Repeat until the quality bar is met.

**When to use it:** When you need *guaranteed quality*, not just "first attempt" quality. This is the most powerful pattern for producing excellent output.

**Real-world analogy:** An editor reviewing a manuscript. The author writes a draft, the editor marks it up, the author revises, the editor reviews again — until both are satisfied.

**Example: Design Document with Quality Gate**

```yaml
workflow:
  limits:
    max_iterations: 10         # Safety limit: don't loop forever

agents:
  - name: architect
    prompt: |
      Write a technical design for: {{ workflow.input.requirement }}
      
      {% if reviewer is defined and reviewer.output %}
      Previous score: {{ reviewer.output.score }}/100
      Feedback: {{ reviewer.output.feedback }}
      Incorporate this feedback and improve.
      {% endif %}
    routes:
      - to: reviewer

  - name: reviewer
    prompt: |
      Score this design 0-100 on completeness, feasibility, 
      and clarity. Be strict.
      {{ architect.output.design }}
    routes:
      - to: $end
        when: "{{ output.score >= 90 }}"    # Exit when quality is high
      - to: architect                        # Otherwise, loop back
```

**Flow:** Architect → Reviewer → (score ≥ 90? → Done) or (score < 90? → back to Architect with feedback)

**Why this pattern:** It guarantees a quality threshold. The output isn't "done" until it *provably* meets your standard. The safety limit (`max_iterations: 10`) prevents infinite loops.

> **💡 Key Insight:** This is the same principle behind Waza's automated improvement — generate, evaluate, improve, repeat. The loop pattern makes this principle a first-class feature of workflows.

---

### Pattern 3: Conditional (Branching) 🔀

**What it is:** Based on the result of one agent's work, the workflow takes different paths. Like a "choose your own adventure" book.

**When to use it:** When different situations require different handling. Not every input should follow the same path.

**Real-world analogy:** A hospital triage desk. Based on symptoms, patients are routed to the emergency room, a specialist, or general care. Same entry point, different paths based on assessment.

**Example: Support Ticket Router**

```yaml
agents:
  - name: classifier
    prompt: |
      Classify this support ticket:
      {{ workflow.input.ticket }}
      
      Categories: billing, technical, feature_request
    routes:
      - to: billing_agent
        when: "{{ output.category == 'billing' }}"
      - to: tech_agent
        when: "{{ output.category == 'technical' }}"
      - to: product_agent

  - name: billing_agent
    prompt: "Resolve this billing issue..."
    routes:
      - to: $end

  - name: tech_agent
    prompt: "Diagnose this technical problem..."
    routes:
      - to: $end

  - name: product_agent
    prompt: "Log this feature request..."
    routes:
      - to: $end
```

**Flow:** Classifier → (billing? / technical? / feature request?) → Specialized Agent → Done

**Why this pattern:** Different problems need different expertise. Routing ensures the right agent handles the right work.

---

### Pattern 4: Parallel (Simultaneous Execution) ⚡

**What it is:** Multiple agents work at the same time, each on their own piece of the task. When all finish, their results are combined.

**When to use it:** When parts of a task are independent and can happen simultaneously. This makes workflows faster and often more thorough.

**Real-world analogy:** A research team where one person searches academic papers, another searches news articles, and a third searches industry reports — all at the same time. Then they meet to combine findings.

**Example: Multi-Source Research**

```yaml
parallel:
  - name: research_team
    agents:
      - web_researcher
      - academic_researcher
      - news_researcher
    failure_mode: continue_on_error  # If one fails, others continue
    routes:
      - to: synthesizer

agents:
  - name: web_researcher
    prompt: "Search the web for: {{ workflow.input.topic }}"

  - name: academic_researcher
    prompt: "Find academic sources on: {{ workflow.input.topic }}"

  - name: news_researcher
    prompt: "Find recent news about: {{ workflow.input.topic }}"

  - name: synthesizer
    prompt: |
      Combine these research findings into one coherent summary:
      Web: {{ research_team.outputs.web_researcher.findings }}
      Academic: {{ research_team.outputs.academic_researcher.findings }}
      News: {{ research_team.outputs.news_researcher.findings }}
    routes:
      - to: $end
```

**Flow:** [Web + Academic + News researchers simultaneously] → Synthesizer → Done

**Why this pattern:** Three researchers working in parallel take the same time as one researcher — but produce three times the coverage. Speed AND thoroughness.

**Failure modes explained:**

| Mode | What Happens If One Agent Fails |
|------|-------------------------------|
| `fail_fast` | Stop everything immediately |
| `continue_on_error` | Let the others finish; proceed with partial results |
| `all_or_nothing` | Let all finish; but fail the whole group if any failed |

---

### Pattern 5: For-Each (Dynamic Parallel Processing) 🔁

**What it is:** You have a list of items. The workflow automatically creates one agent per item and processes them all in parallel.

**When to use it:** When the number of items isn't known in advance. The list could have 3 items or 300 — the workflow adapts.

**Real-world analogy:** A teacher grading exams. They don't know in advance how many students will submit. But for each submission, the same grading process applies. With enough graders, they can all be scored simultaneously.

**Example: Analyze a Portfolio of Companies**

```yaml
for_each:
  - name: company_analyzers
    source: portfolio_loader.output.companies   # Dynamic list
    as: company                                  # Variable name for each item
    max_concurrent: 5                            # Process 5 at a time
    
    agent:
      name: analyzer
      prompt: |
        Analyze company #{{ _index + 1 }}: {{ company.name }}
        Website: {{ company.url }}
        Provide a brief assessment.
    
    routes:
      - to: aggregator

agents:
  - name: portfolio_loader
    prompt: "List all companies in this portfolio: {{ workflow.input.portfolio }}"
    routes:
      - to: company_analyzers

  - name: aggregator
    prompt: |
      Combine these individual analyses into a portfolio summary:
      {% for result in company_analyzers.outputs %}
      - {{ result.assessment }}
      {% endfor %}
    routes:
      - to: $end
```

**Flow:** Portfolio Loader → [N analyzers in parallel, one per company] → Aggregator → Done

**Why this pattern:** You write the logic once. Whether the portfolio has 3 companies or 30, the workflow handles it. The `max_concurrent: 5` setting prevents overloading by processing in batches.

---

### Pattern 6: Human Gate (Human-in-the-Loop) 🚪

**What it is:** The workflow pauses and waits for a human to make a decision. The human sees the current results and chooses what happens next.

**When to use it:** When you need human judgment, approval, or oversight at critical points. This is the "human-in-the-loop" pattern that ensures AI proposes but humans decide.

**Real-world analogy:** A purchase approval workflow. An employee submits a request, their manager reviews it, and chooses: approve, reject, or send back for revision.

**Example: Design Review with Human Approval**

```yaml
agents:
  - name: designer
    prompt: "Create a solution design for: {{ workflow.input.requirements }}"
    routes:
      - to: review_gate

  - name: review_gate
    type: human_gate
    prompt: |
      Review this design:
      {{ designer.output.design }}
    options:
      - label: "✅ Approve"
        value: approved
        route: $end
      - label: "✏️ Request Changes"
        value: changes
        route: designer
        prompt_for: feedback      # Collects text input from the human
      - label: "❌ Reject"
        value: rejected
        route: $end
```

**Flow:** Designer → Human Review → (Approve → Done) or (Request Changes → back to Designer with feedback) or (Reject → Done)

**Why this pattern:** Not everything should be fully automated. For important decisions — spending money, publishing content, making commitments — a human should be in the loop. This pattern makes that seamless.

> **⚠️ Important:** Human gates are the primary safety mechanism for high-stakes workflows. Any workflow that produces public-facing output, makes financial decisions, or takes irreversible actions should include at least one human gate.

---

### Pattern 7: Script Step (System Commands) 📜

**What it is:** Instead of asking an AI agent to do something, this step runs an actual computer command — checking a file, running a test, verifying a service.

**When to use it:** When you need concrete, deterministic verification. Not everything requires AI judgment. Sometimes you just need to check: does this file exist? Is this service running? Did this command succeed?

**Real-world analogy:** A pre-flight checklist. Before takeoff, pilots don't *discuss* whether the landing gear is extended — they *check an instrument* that gives a definitive yes/no answer.

**Example: Verify Before Proceeding**

```yaml
agents:
  - name: check_prerequisites
    type: script
    command: python3
    args: ["--version"]
    routes:
      - to: code_generator
        when: "exit_code == 0"        # Python is installed
      - to: error_handler              # Python is NOT installed

  - name: code_generator
    prompt: "Generate a Python script that..."
    routes:
      - to: $end

  - name: error_handler
    prompt: "Python is not available. Suggest alternatives..."
    routes:
      - to: $end
```

**Flow:** Check Python → (installed? → Generate Code) or (not installed? → Handle Error)

**Why this pattern:** AI agents are great at reasoning and creativity. They're unnecessary for binary checks. Script steps are faster, cheaper, and deterministic.

---

### Combining Patterns

Real workflows rarely use just one pattern. Here's how they combine:

**Example: Full Research Pipeline**

```
[Script: Check internet access]
    ↓
[Researcher agent]
    ↓
[Parallel: Web + Academic + News research]
    ↓
[Synthesizer agent]
    ↓
[Quality Reviewer agent] ←── Loop back if score < 90
    ↓
[Human Gate: Approve / Revise / Reject]
    ↓
[Report Writer agent]
    ↓
Done
```

This single workflow uses: Script Step + Linear + Parallel + Loop + Human Gate + Linear. Seven steps, five patterns, one seamless flow.

---

## Chapter 9: Safety & Control

### Why Safety Is Built In

Power without control is just chaos. Every workflow pattern in Chapter 8 could theoretically run forever, consume unlimited resources, or produce output nobody wanted. Safety mechanisms prevent all of this.

### The Safety Toolkit

#### 1. Iteration Limits

**What:** A maximum number of times any agent can execute within a workflow.

**Why:** Prevents infinite loops. If the reviewer never gives a score above 90 and the workflow keeps sending work back, the iteration limit stops it.

**How:** Set in the workflow configuration:
```yaml
limits:
  max_iterations: 50     # Maximum 50 agent executions total
```

**Default:** 10 iterations. Maximum: 500. Customize based on your workflow's needs.

#### 2. Timeout

**What:** A wall-clock time limit for the entire workflow.

**Why:** Even without infinite loops, a workflow could simply take too long — a network issue, a slow model, an unexpectedly large dataset.

**How:**
```yaml
limits:
  timeout_seconds: 600   # Stop after 10 minutes
```

#### 3. Checkpoint & Resume

**What:** If a workflow fails at step 7 of 10, it automatically saves everything that completed successfully. You can resume from step 7 instead of starting over.

**Why:** Long workflows shouldn't lose all progress because of a transient error. This is the "save game" feature.

**How:**
```bash
# Workflow fails at some point — checkpoint saved automatically
# Later, resume from where it stopped:
conductor resume my-workflow.yaml
```

#### 4. Pre-Execution Validation

**What:** Before running anything, Conductor checks the workflow for structural problems.

**Why:** Better to find issues before execution than during. This catches:
- Agents referenced in routes but never defined
- Agents defined but never reachable from the starting point
- Workflows with no path to completion
- Invalid template syntax

**How:**
```bash
conductor validate my-workflow.yaml
# Reports: "Validation Successful. 2 agents, conditional routing, loop-back."
```

#### 5. Cost Tracking

**What:** Real-time tracking of how many tokens (units of AI processing) each agent consumes, and the estimated cost.

**Why:** AI processing costs money (or subscription quota). Without visibility, a poorly designed workflow could consume far more resources than expected.

**How:** Built in by default. After every run:
```
Token Usage Summary
  Input:  29,146 tokens
  Output: 321 tokens
  Total:  29,467 tokens
```

#### 6. Web Dashboard

**What:** A visual interface that shows workflow execution in real time — which agent is working, which completed, the data flowing between them.

**Why:** Visibility builds confidence. When you can *see* what's happening, you trust the system more — and you can intervene if something looks wrong.

**How:**
```bash
conductor run my-workflow.yaml --web --input topic="AI safety"
# Opens a browser dashboard with a live workflow visualization
```

> **💡 Key Insight:** Safety is not about limiting what you can do. It's about making what you do *predictable and controllable*. Every safety mechanism exists to give you confidence that the workflow will behave as expected — or stop gracefully if it doesn't.

---

## Chapter 10: Running Your First Workflow

This is a hands-on chapter. If you have access to the tools, follow along. If not, read through the steps — the concepts matter more than the commands.

### Step 1: Install Conductor

**macOS / Linux:**
```bash
curl -sSfL https://aka.ms/conductor/install.sh | sh
```

**Windows (PowerShell):**
```powershell
irm https://aka.ms/conductor/install.ps1 | iex
```

**Verify:**
```bash
conductor --version
# → Conductor v0.1.5
```

### Step 2: Create Your Workflow

Create a file called `my-first-workflow.yaml`:

```yaml
workflow:
  name: my-first-workflow
  description: A simple Q&A with quality check
  entry_point: answerer

  input:
    question:
      type: string
      required: true

  limits:
    max_iterations: 5
    timeout_seconds: 120

agents:
  - name: answerer
    prompt: |
      Answer this question concisely and accurately:
      {{ workflow.input.question }}
    output:
      answer:
        type: string
    routes:
      - to: $end

output:
  answer: "{{ answerer.output.answer }}"
```

### Step 3: Validate

```bash
conductor validate my-first-workflow.yaml
```

You should see: "Validation Successful."

### Step 4: Run

```bash
conductor run my-first-workflow.yaml --input question="What is Rust?"
```

You'll see the agent process the question and return a structured JSON answer.

### Step 5: Celebrate 🎉

You just ran your first Conductor workflow. It was simple — one agent, one step. But the infrastructure is now in place for everything in Chapter 8.

Try modifying it: add a second agent that reviews the answer. Add a quality score. Add a loop-back condition. Each modification exercises a new pattern — and none requires more than a few lines of YAML.

---

Now comes the part where everything clicks together.

In Part I, you learned how to teach a single agent to do one thing well (skills). In Part II, you learned how to organize multiple agents into teams (workflows). Part III shows what happens when you combine them — and why the combination is greater than the sum of its parts.

---

# Part III: The Integration — Skills + Workflows Together

---

## Chapter 11: How Skills and Workflows Connect

### The Missing Piece

If you've read Parts I and II, you might be wondering: "Skills and workflows both sound great individually. But how do they work *together*?"

This is the key insight — the moment where two powerful ideas become one transformative system.

### Skills Are the "What." Workflows Are the "How."

| | Skills | Workflows |
|---|--------|-----------|
| **Teach** | One agent to do one thing well | Multiple agents to collaborate |
| **Define** | The capability | The process |
| **Answer** | "What should the agent know?" | "Who does what, in what order?" |
| **Analogy** | A recipe | A kitchen management plan |

A recipe for chocolate chip cookies is useless without a kitchen. A kitchen is useless without recipes. Together, they produce cookies.

Skills without workflows produce isolated capabilities. Workflows without skills produce generic, unspecialized work. Together, they produce professional-grade output.

### Concrete Example: The Market Research Pipeline

Let's trace how skills and workflows integrate in a real scenario:

**The Skills (What Each Agent Knows):**

1. **competitor-analysis** skill — Teaches the research agent how to investigate a market across 6 dimensions, score competitors, and produce strategic insights
2. **docx** skill — Teaches the report agent how to create professional Word documents with proper formatting, tables, and page layout

**The Workflow (How Agents Collaborate):**

```yaml
workflow:
  name: market-research
  entry_point: researcher
  limits:
    max_iterations: 20

agents:
  - name: researcher
    # Uses the competitor-analysis skill
    prompt: |
      Perform competitive analysis for {{ workflow.input.market }}.
      Follow the 6-track research methodology.
      {% if quality_checker is defined and quality_checker.output %}
      Address this feedback: {{ quality_checker.output.feedback }}
      {% endif %}
    routes:
      - to: quality_checker

  - name: quality_checker
    prompt: |
      Verify this analysis covers all 6 research tracks.
      Score completeness 0-100.
      {{ researcher.output.report }}
    routes:
      - to: report_writer
        when: "{{ output.score >= 85 }}"
      - to: researcher

  - name: report_writer
    # Uses the docx skill
    prompt: |
      Create a professional Word document from this analysis:
      {{ researcher.output.report }}
      Include executive summary, competitive map, and recommendations.
    routes:
      - to: approval_gate

  - name: approval_gate
    type: human_gate
    prompt: "Review the market research report"
    options:
      - label: "Approve & Send"
        value: approved
        route: $end
      - label: "Request Revisions"
        value: revise
        route: researcher
        prompt_for: feedback
      - label: "Reject"
        value: rejected
        route: $end
```

**What happens when you run this:**

1. The **researcher** agent activates the competitor analysis skill, investigating the market across 6 tracks
2. The **quality checker** verifies all tracks are covered; if not, sends it back with feedback (loop pattern)
3. Once quality passes (score ≥ 85), the **report writer** creates a formatted Word document (using the docx skill)
4. The **approval gate** pauses for human review — you see the report and choose: approve, revise, or reject

Two skills. Four agents. Three patterns (linear, loop, human gate). One integrated pipeline.

> **💡 Key Insight:** Each agent doesn't need to know about the others. The researcher doesn't know a quality checker exists. The report writer doesn't know about the approval gate. Each agent focuses on its job. The workflow handles coordination. This separation is what makes the system maintainable and scalable.

---

## Chapter 12: The Complete Pipeline

### Eight Steps from Process to Product

Here's the complete lifecycle — from identifying something you want to automate, to having a tested, scalable product:

#### Step 1: Identify 🔍

Find a process that's:
- **Repeatable** — You do it the same way (roughly) each time
- **Describable** — You can explain it in words to another person
- **Valuable** — It takes meaningful time or produces meaningful output

Examples: Researching a company, writing a weekly report, processing customer inquiries, generating meeting summaries, creating project proposals.

#### Step 2: Write ✍️

Turn your process into a skill:
- Describe what it does and when to use it
- Write step-by-step instructions
- Include edge cases and decision points
- Specify what good output looks like

Use the same language you'd use to train a new team member.

#### Step 3: Test 🧪

Measure the skill scientifically:
- Run `waza check` for structural compliance
- Run trigger tests to verify activation accuracy
- Run real agent tests with quality rubrics
- Get a baseline score

#### Step 4: Improve 🔄

Use test results to refine:
- Identify which criteria failed
- Adjust the skill instructions
- Re-test and compare: did the score improve?
- Repeat until the quality bar is met

This can happen manually (you review and edit) or automatically (`waza dev` makes improvements for you).

#### Step 5: Combine 🔗

Connect skills into workflows:
- Which skills need to work together?
- What's the sequence?
- Where are the quality checkpoints?
- Where should humans be in the loop?

Write a Conductor workflow YAML that orchestrates the skills.

#### Step 6: Validate ✅

Test the workflow end-to-end:
- `conductor validate` for structural correctness
- `conductor run --dry-run` for execution preview
- Full test run with real inputs
- Verify output quality, timing, and cost

#### Step 7: Human-in-the-Loop 🚪

Add oversight where it matters:
- Human gates at critical decision points
- Review mechanisms for high-stakes output
- Override capabilities for edge cases

The goal: AI does the heavy lifting, humans make the important decisions.

#### Step 8: Scale 📈

From one execution to many:
- Run the workflow on demand for individual cases
- Schedule regular runs for periodic tasks
- Share with team members who need the same capability
- Publish skills to registries for wider adoption
- Build products on top of proven workflows

### The Pipeline Visualized

```
 Identify          Write           Test           Improve
 a process    →   a skill    →   with data   →   with evidence
    🔍               ✍️              🧪              🔄
                                                     |
                                                     ↓
   Scale          Human Gate      Validate        Combine
   the product ← add oversight ← the workflow ← into workflow
    📈               🚪              ✅              🔗
```

> **🎯 The Transformative Idea:** Any process that a human can explain in words can become a tested, validated, scalable AI product through this pipeline. No programming required at any step. The barrier is not technical skill — it's clarity of thinking.

---

## Chapter 13: From Process to Product

### Three Transformation Examples

The first two examples below are realistic scenarios that illustrate common patterns. The third is a real case — actually built, tested, and measured with the tools described in this guide.

#### Example 1: Weekly Competitor Analysis (Illustrative)

**The process (before):** Every Monday, a market analyst spends 4 hours searching for competitor news, reading articles, summarizing findings, and emailing the team.

**The transformation:**
- **Skill created:** `competitor-analysis` — Instructions for searching 5 news sources, extracting key updates, categorizing by impact level
- **Skill tested:** Trigger accuracy 100%, quality score 92/100
- **Workflow built:** Parallel research (5 agents, one per source) → Synthesizer → Quality Reviewer (loop until score ≥ 85) → Report Writer → Email Delivery
- **Result:** 45 minutes instead of 4 hours. Higher coverage (5 simultaneous sources). Consistent format every week.

#### Example 2: Customer Onboarding Documentation (Illustrative)

**The process (before):** When a new enterprise client signs up, a team member manually creates their onboarding package — welcome doc, API setup guide, configuration checklist, support contacts.

**The transformation:**
- **Skills created:** `welcome-doc`, `api-setup-guide`, `config-checklist` — Each produces one section of the onboarding package
- **Skills tested:** All pass compliance, quality scored independently
- **Workflow built:** For-each pattern (one agent per document section) → Assembler → Human Review Gate → Delivery
- **Result:** Onboarding package generated in 10 minutes. Previously: 2 days. Human reviews before delivery, ensuring quality.

#### Example 3: Market Research Report (Real — Built and Tested)

**This one is real.** It was built, tested, and validated with the actual tools described in this guide.

**The process (before):** Manually researching markets across multiple dimensions — a process that takes days and produces inconsistent results depending on time pressure.

**The transformation:**
- **Skill created:** `competitor-analysis` — Comprehensive 6-track research methodology with scoring rubric
- **Skill tested:** Waza evaluation — trigger accuracy 100%, quality 5/5 criteria, compliance High
- **Workflow built:** Researcher → Quality Checker (loop) → Report Writer → Human Approval Gate
- **Result:** Complete market analysis in under an hour. Consistent methodology every time. Human approval before any decisions.

### The Pattern

Notice what's common across all three examples:

1. A **human process** that was already working, but slow and inconsistent
2. **Skills** that capture the methodology in precise instructions
3. **Testing** that proves the skills work correctly
4. **Workflows** that orchestrate the skills with quality checks and human oversight
5. **Better outcomes**: faster, more consistent, more thorough — and still human-controlled

That's the pattern. It works for any process you can describe.

---

# Part IV: Reference

---

## Appendix A: Glossary of Terms

| Term | Definition |
|------|-----------|
| **Agent** | An AI program that understands instructions, makes decisions, and takes actions to complete tasks |
| **Agent Skill** | A text file (SKILL.md) containing instructions that teach an agent how to perform a specific task |
| **Anti-trigger** | A description of when a skill should NOT be activated |
| **Checkpoint** | A saved snapshot of workflow progress, enabling resume after failure |
| **Compliance** | How well a skill follows the structural standards (measured by `waza check`) |
| **Conductor** | A CLI tool by Microsoft for defining and running multi-agent workflows in YAML |
| **Copilot SDK** | The execution engine that powers real agent turns during testing and workflow execution |
| **Entry point** | The first agent or group that executes when a workflow starts |
| **Eval suite** | A collection of test cases for evaluating a skill's quality |
| **Failure mode** | How a parallel group handles individual agent failures (fail_fast, continue_on_error, all_or_nothing) |
| **For-each** | A workflow pattern that dynamically creates one agent per item in a list |
| **Grader** | A component in Waza that evaluates agent output against criteria |
| **Human gate** | A workflow step that pauses for human decision-making |
| **Iteration** | One execution of one agent within a workflow |
| **Jinja2 template** | A placeholder syntax ({{ variable }}) that gets replaced with actual values at runtime |
| **Loop-back** | A routing pattern where an agent's output is sent back to a previous agent for revision |
| **Markdown** | A simple text formatting language used for skill files |
| **MCP (Model Context Protocol)** | A standard for connecting AI agents to external tools and services |
| **Mock executor** | A testing mode that simulates agent responses without calling a real AI model |
| **Parallel group** | A set of agents that execute simultaneously |
| **Progressive disclosure** | A design technique that introduces complexity gradually |
| **Prompt** | The instructions given to an AI agent for a specific task |
| **Route** | A rule defining where work goes next in a workflow |
| **Script step** | A workflow step that runs a computer command instead of an AI agent |
| **Trigger** | A description of when a skill should be activated |
| **Waza** | A CLI tool by Microsoft for testing and evaluating agent skills |
| **Workflow** | A structured sequence of steps where agents collaborate to complete a task |
| **YAML** | A human-readable text format for describing structured data (used for workflows and tests) |

---

## Appendix B: Waza Command Reference

| Command | What It Does | Example |
|---------|-------------|---------|
| `waza check <skill>` | Verify skill structural compliance | `waza check skills/my-skill/` |
| `waza dev <skill>` | Auto-improve skill compliance | `waza dev skills/my-skill/ --target high --auto` |
| `waza dev <skill> --scaffold-triggers` | Generate trigger test prompts from description | `waza dev skills/my-skill/ --scaffold-triggers` |
| `waza new skill <name>` | Create a new skill from template | `waza new skill my-new-skill` |
| `waza new eval <skill>` | Generate an eval suite scaffold | `waza new eval my-skill` |
| `waza run <eval.yaml>` | Execute an evaluation | `waza run evals/eval.yaml -v` |
| `waza run <eval> --task <id>` | Run a specific test only | `waza run eval.yaml --task "quality-test"` |
| `waza compare <a> <b>` | Compare two evaluation results | `waza compare v1.json v2.json` |
| `waza tokens count <skill>` | Count tokens in a skill | `waza tokens count skills/my-skill/` |
| `waza tokens suggest <skill>` | Suggest token optimizations | `waza tokens suggest skills/my-skill/` |
| `waza suggest <skill> --apply` | LLM-generated eval artifacts | `waza suggest skills/my-skill/ --apply` |

**Executor options:** `mock` (simulated, fast), `copilot-sdk` (real agent, thorough)

---

## Appendix C: Conductor YAML Quick Reference

### Minimal Workflow

```yaml
workflow:
  name: my-workflow
  entry_point: my_agent
  input:
    question: { type: string }

agents:
  - name: my_agent
    prompt: "{{ workflow.input.question }}"
    output:
      answer: { type: string }
    routes:
      - to: $end

output:
  answer: "{{ my_agent.output.answer }}"
```

### Key Configuration Options

```yaml
workflow:
  runtime:
    provider: copilot          # or: claude
    default_model: gpt-5.2    # model for all agents
    temperature: 0.7           # randomness (0=deterministic, 1=creative)
    max_tokens: 4096           # max output length per response
    timeout: 600               # per-request timeout (seconds)
  
  context:
    mode: accumulate           # accumulate | last_only | explicit
  
  limits:
    max_iterations: 10         # max agent executions (1-500)
    timeout_seconds: 600       # total workflow timeout
  
  cost:
    show_per_agent: true       # show cost per agent
    show_summary: true         # show total cost
```

### CLI Commands

| Command | Description |
|---------|-------------|
| `conductor run <file>` | Execute a workflow |
| `conductor run <file> --web` | Execute with visual dashboard |
| `conductor run <file> --dry-run` | Preview without executing |
| `conductor validate <file>` | Check for errors |
| `conductor init <name>` | Create from template |
| `conductor resume <file>` | Resume from checkpoint |
| `conductor checkpoints` | List saved checkpoints |
| `conductor stop` | Stop background workflows |
| `conductor update` | Check for updates |

### Common Flags

| Flag | Effect |
|------|--------|
| `--input key=value` | Pass input parameters |
| `-q` / `--quiet` | Minimal output (lifecycle only) |
| `-s` / `--silent` | JSON result only |
| `--log-file auto` | Save full debug log |
| `--skip-gates` | Auto-select at human gates |
| `-p copilot` or `-p claude` | Override provider |

### Output Types

```yaml
output:
  text:    { type: string }
  count:   { type: number }
  flag:    { type: boolean }
  items:   { type: array, items: { type: string } }
  result:  { type: object, properties: { name: { type: string } } }
```

### Route Conditions

```yaml
routes:
  - to: agent_b
    when: "{{ output.score >= 90 }}"           # comparison
  - to: agent_c
    when: "{{ output.status == 'approved' }}"   # equality
  - to: agent_d
    when: "{{ output.retry and not output.failed }}"  # logic
  - to: agent_e                                 # default (no condition)
```

---

## Appendix D: Further Reading & Resources

### Official Documentation

- **Conductor GitHub:** https://github.com/microsoft/conductor
- **Waza GitHub:** https://github.com/microsoft/waza
- **AgentSkills Open Format:** https://agentskills.io
- **AgentSkills Specification:** https://agentskills.io/specification

### Skill Registries

- **GitHub Awesome Copilot Skills:** https://github.com/github/awesome-copilot
- **Microsoft Skills:** https://github.com/microsoft/skills
- **Anthropic Skills:** https://github.com/anthropics/skills
- **OpenAI Skills:** https://github.com/openai/skills

### Frameworks Referenced in This Guide

- **Diátaxis Documentation Framework:** https://diataxis.fr — The four-quadrant model (tutorials, how-to guides, reference, explanation) that informed this guide's structure
- **Dale Carnegie's Principles:** Reader-centric communication techniques used throughout this guide's tone and approach

### Concepts for Further Exploration

- **LLM-as-Judge Pattern:** Using one AI to evaluate another AI's output — the technique behind Waza's prompt grader
- **Evaluator-Optimizer Loops:** Iterative improvement patterns where evaluation drives optimization
- **Progressive Disclosure in UX:** The design principle of revealing complexity gradually, applied throughout this guide
- **Cognitive Load Theory:** Understanding why chunked, layered information is easier to absorb than information dumps

---

## Closing

You started this guide knowing nothing about AI agent skills or multi-agent workflows.

Now you understand:

- **What agent skills are** — instruction sets that teach AI agents specific capabilities, written in plain language
- **How to test them** — scientifically, with measurable evidence, using Waza
- **How to improve them** — iteratively, with before/after comparison proving each improvement
- **What multi-agent workflows are** — structured collaboration between specialized AI agents
- **The seven workflow patterns** — linear, loop, conditional, parallel, for-each, human gate, script step
- **How to keep everything safe** — limits, timeouts, checkpoints, validation, human oversight
- **How skills and workflows integrate** — skills provide capability, workflows provide orchestration, together they produce products
- **The complete pipeline** — from identifying a process to scaling it as a product

The most important thing you've learned isn't any single concept. It's this:

***Any process that a human can explain clearly in words can become a tested, validated, scalable AI product.***

The barrier was never programming ability. It was never AI expertise. It was always clarity — the ability to say exactly what you want, step by step, with precision.

You already have that ability. You've been doing it every time you've trained a colleague, written a how-to guide, or explained your work to someone new.

Now you have the tools to turn that clarity into something that works tirelessly, consistently, and at any scale — while keeping you firmly in control.

Welcome to the future of work. It's yours to build.

---

*Author: Alex Hutanu (alex@hutanu.net) — March 2026*
*Built with evidence from real testing: 1,728 unit tests, 11 validated workflows, live Copilot SDK execution, Waza eval suites with data-driven A/B comparisons.*
