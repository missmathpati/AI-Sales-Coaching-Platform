# AI Sales Coaching System (LLM-Based Call Auditing)

Built a production AI system to scale how elite sales coaches audit calls.

Sales coaches typically spend 45–90 minutes manually reviewing a single call and producing structured feedback covering strengths, gaps, and specific tactical fixes. This process is high-quality but does not scale.

To address this, I co-led the development of a two-stage LLM system that converts raw call transcripts into structured audit reports in under ~2 minutes, replicating a coach’s evaluation process across calls.

The system is designed as a **two-stage LLM pipeline** deployed via serverless microservices.

## System Architecture 
<p align="center">
  <img src="Architecture.png)" alt="System Architecture" width="700"/>
</p>

---

## System Flow

```id="flow1"
Call Input → Transcription → Call Notes → AI Report → Output
```

---

## 1. Data Ingestion

Calls enter the system in two ways:

* Audio / video upload
* External call platform links (abstracted ingestion layer)

For all inputs:

* transcripts are generated or provided
* transcripts are normalized into a consistent format

**Output:**

* timestamped transcript
* speaker-separated text

---

## 2. Transcription Layer

**Service:** Transcription microservice
**Model:** Deepgram

Responsibilities:

* convert audio/video into text
* perform speaker diarization
* generate timestamped transcript

**Output Example:**

```id="t1"
[Speaker 1] [00:02] How are you evaluating solutions today?
[Speaker 2] [00:05] We're looking at a few vendors...
```

---

## 3. Stage 1 — Call Notes Generation

**Service:** Call Notes microservice
**Model:** GPT-4.1
**Latency:** ~15–30 seconds

This stage converts the transcript into **structured coaching notes**.

Each note includes:

* timestamp
* transcript snippet
* coaching observation
* category tags

**Example:**

```id="n1"
02:15 → Asked generic question → weak discovery → [Discovery, AOI]
05:30 → Jumped into demo early → [Demo, AOI]
```

Characteristics:

* grounded in transcript
* no aggregation
* captures all relevant signals

**Output:**

* list of structured notes stored in database

---

## 4. Stage 2 — AI Report Generation

**Service:** AI Report microservice
**Model:** GPT-4o
**Latency:** ~60–120 seconds

This stage generates the final **structured audit report**.

**Input:**

* notes from Stage 1
* (optional) notes from multiple calls

**Processing:**

* prioritize key issues
* group related observations
* generate actionable recommendations

**Output:**

* structured report (XML-style schema)

**Example:**

```xml id="r1"
<Fix>
  <Category>Discovery</Category>
  <Problem>Insufficient qualification</Problem>
  <Impact>Low relevance demo</Impact>
  <Fix>Ask targeted diagnostic questions</Fix>
</Fix>
```

---

## 5. Multi-Call Aggregation

For representative-level reports:

* notes from multiple calls are combined
* patterns are identified across calls
* issues must appear consistently to be included

This enables:

* pattern detection
* rep-level evaluation instead of single-call feedback

---

## 6. Context Construction

Stage 2 operates primarily on:

* structured notes (not raw transcript)

This reduces:

* noise from conversation
* context size
* inconsistency in reasoning

---

## 7. Output Layer

Reports are:

* stored in database
* rendered in UI
* exported to external tools (e.g., Notion)

Additional outputs include:

* issue distribution (by category)
* common mistake patterns

---

## 8. Microservices

The system is composed of independent services:

### Transcription Service

* audio/video → transcript

### Call Notes Service

* transcript → structured notes

### AI Report Service

* notes → structured report

---

## 9. System Architecture

* **Frontend:** Next.js
* **Backend:** FastAPI
* **Deployment:** AWS Lambda
* **Database:** Supabase (Postgres + storage)

### AI Stack

* GPT-4.1 → notes
* GPT-4o → report
* Deepgram → transcription

---

## 10. My Contribution

* Co-led the design and development of the end-to-end AI system
* Designed the **two-stage LLM pipeline (call notes → report generation)** that separates signal extraction from judgment
* Built and iterated on the **Call Notes and AI Report services**, including prompt design and structured output generation
* Defined how **Stage 2 consumes structured notes instead of raw transcripts** to improve reasoning consistency and reduce noise
* Implemented logic for **multi-call aggregation**, enabling pattern detection across conversations
* Acted in a **forward-deployed capacity**, leading client discussions and translating real coaching requirements into system design decisions
* Worked closely with stakeholders to **align outputs with real coaching expectations**, iterating based on feedback
* Validated and refined outputs to ensure **consistency, actionability, and alignment with expert-written reports**


---

## 11. Notes

This is a **sanitized system overview**.

* No proprietary code or prompts are included
* Implementation details are abstracted

---
