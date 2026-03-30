# AI Sales Coaching System (LLM-Based Call Auditing)

Built a production AI system that generates structured coaching reports from sales call transcripts by replicating an expert coach’s evaluation process.

The system is designed as a **two-stage LLM pipeline** deployed via serverless microservices.

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

* Designed the **two-stage LLM pipeline (notes → report)**
* Built logic for **call notes structure and generation flow**
* Worked on **context construction between stages**
* Contributed to **multi-call aggregation logic**
* Integrated AI services into a production workflow

---

## 11. Notes

This is a **sanitized system overview**.

* No proprietary code or prompts are included
* Implementation details are abstracted

---
