# Cloning a Sales Coach’s Decision-Making with Production GenAI

## TL;DR

Built a production AI system that replicates how an elite sales coach evaluates calls.

Not just summarizing transcripts, but:

* identifying high-signal moments
* judging rep behavior
* generating structured, tactical feedback
* aggregating patterns across multiple calls

Designed as a **multi-stage LLM system** deployed via serverless microservices.

---

## Problem

Elite sales coaches spend 45–90 minutes reviewing a single call and producing structured audit reports with:

* strengths
* areas of improvement
* exact tactical fixes

This process is:

* slow
* inconsistent
* impossible to scale

### Goal

Replicate a specific coach’s:

* reasoning process
* structure
* tone
* decision-making

…using LLMs in a production system.

---

## System Overview

This is not a “generate summary” problem.

It is a **multi-step reasoning system**:

```id="sys1"
Transcript → Observation → Interpretation → Judgment → Recommendation
```

A single LLM call fails at this.

So the system was decomposed.

---

## AI Pipeline

### Stage 1 — Call Notes (Local Reasoning)

**Input:** Transcript
**Output:** Structured, timestamped insights

* Extract what actually happened
* Tag by category (Discovery, Demo, etc.)
* Stay grounded in transcript

---

### Stage 2 — Report Generation (Global Reasoning)

**Input:** Notes (single or multiple calls)
**Output:** Structured audit report

* Identify patterns
* Prioritize issues
* Generate actionable fixes

---

### Key Insight

> Separate **“what happened”** from **“what it means”**

This significantly improved:

* reasoning quality
* structure consistency
* reliability

---

## Architecture

* Frontend: Next.js (SSE streaming)
* Backend: FastAPI microservices
* Deployment: AWS Lambda (serverless)
* Database: Supabase (Postgres + storage)
* AI Models:

  * GPT-4.1 → note generation
  * GPT-4o → report synthesis
  * Deepgram → transcription

---

## Context Engineering

### Problem

Raw transcripts are:

* noisy
* long
* inconsistent

### Solution

Use **structured notes as intermediate representation**

* compress signal
* reduce token usage
* improve reasoning quality

> Notes act as a reasoning scaffold for the report stage.

---

## Multi-Call Reasoning

Single-call insights are unreliable.

The system:

* aggregates notes across calls
* tracks frequency of patterns
* enforces consistency

Example:

> Issue must appear in multiple calls to be included

Prevents:

* overfitting to one call
* contradictory outputs

---

## Output Design

Reports are generated in a **strict structured format** to ensure:

* consistency
* parseability
* downstream analytics

Example:

```xml id="xml1"
<Fix>
  <Category>Discovery</Category>
  <Problem>Weak qualification</Problem>
  <Impact>Low relevance demo</Impact>
  <Fix>Ask targeted diagnostic questions</Fix>
</Fix>
```

---

## Prompting Strategy (Abstracted)

* Modular prompt components (persona, task, output schema)
* Few-shot examples to anchor style
* Structured output enforcement

> Exact prompt structures and templates are proprietary.

---

## Microservices

### 1. Transcription

* Converts audio/video → speaker-separated transcripts

### 2. Call Notes Service

* Generates structured coaching notes
* ~15–30s latency

### 3. Report Generation Service

* Produces full audit report + analytics
* ~60–120s latency

### 4. Feedback System (Conceptual Contribution)

* Uses user ratings to improve future outputs
* Designed as a knowledge-driven update loop

---

## Engineering Challenges

### 1. Matching Human Coaching Style

Generic prompts produced generic feedback.

Solution:

* structured reasoning pipeline
* example-driven alignment
* iterative refinement

---

### 2. Reliable Structured Outputs

LLMs frequently break schemas.

Solution:

* strict output specification
* validation + error handling
* decomposition into smaller tasks

---

### 3. Multi-Call Consistency

Risk of contradictions across calls.

Solution:

* aggregation logic
* frequency thresholds
* constrained reasoning

---

### 4. Long Context Handling

Full transcripts degrade performance.

Solution:

* intermediate note representation
* signal-first context design

---

## Tradeoffs

| Decision        | Choice        | Why                               |
| --------------- | ------------- | --------------------------------- |
| Pipeline design | Multi-stage   | Improves reasoning reliability    |
| Context         | Notes-focused | Better signal than raw transcript |
| Output format   | Structured    | Enables validation + analytics    |
| Infra           | Serverless    | Scalable, event-driven            |

---

## Results

* ~82% alignment with expert-written reports
* ~60% reduction in manual review time
* Significant improvement in consistency of feedback

---

## My Contribution

* Designed the **multi-stage LLM pipeline (notes → report)**
* Built core logic for **context construction and reasoning flow**
* Worked on **prompt design and structured output strategy**
* Contributed to **feedback loop design (conceptual)**
* Collaborated on integrating AI services into a production system

---

## Key Learnings

* LLM performance is driven more by **system design than prompts**
* Intermediate representations dramatically improve reasoning
* Structured outputs are essential for production reliability
* Multi-stage pipelines outperform single-pass generation

---

## Note

This is a **sanitized case study** of a production system.

* No proprietary code or data is included
* Prompt templates, schemas, and internal implementations are abstracted

---

## Final Thought

This project shifted my perspective from:

> “using LLMs”

to

> “designing systems that think before generating”

---
