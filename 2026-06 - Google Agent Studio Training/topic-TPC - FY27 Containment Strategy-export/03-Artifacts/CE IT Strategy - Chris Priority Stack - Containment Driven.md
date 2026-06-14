---
type: artifact
functional_class: Design
artifact_status: Active
created_date: '2026-05-25'
topics:
  - '[[TPC - CE + IT - 3yr Execution Strategy Session]]'
  - '[[TPC - FY27 Containment Strategy]]'
entities: []
file: ''
---
``
# Strategic Priority Stack — CE + IT Containment-Driven Workstreams

**Source:** Conversation with Chris Coffey
**Date Captured:** 2026-05-25
**Owner:** Ryan Dunn

---

## Priority Order (Chris-Confirmed)

The following represents the priority sequence for CE + IT execution work as driven by containment rate impact. This is the authoritative ordering for resource allocation, sequencing decisions, and leader delegation.

| # | Workstream | Primary Owner | Notes |
|---|-----------|--------------|-------|
| 1 | **1st Responder Agent** | Michael Proffer | First step in the hybrid support layer — Command Center Phase 1 |
| 2 | **Chat Support — CRC Launch** | Michael Proffer / Vivek (CoE builds) | Either Dialogflow (legacy) or Agent Studio (GECX) — legacy path is approved |
| 3 | **Voice Channel → Agent Studio Migration** | Michael Proffer | Customer-facing improvement; interruptibility and context-awareness |
| 4 | **Tech Writing → Publishing → Relational DB → Knowledge Catalog** | Jason Nicol / Abhirup Dash / Vivek | Full knowledge data pipeline — authoring through grounding |
| 5 | **Knowledge Catalog Tuning Operations** | Vivek / Jason Nicol | Ongoing once KC is live — curation, editorial rules, quality |
| 6 | **BigQuery + Gemini — ENT Deep Integration (Solutions)** | Abhirup Dash / John McCall | Enterprise data strategy — AOS data integration |
| 7 | **Command Center Maturation — CE Org** | Michael Proffer / Vivek | Phase 2 AI Tooling Hub — proactive, multi-agent supervision |

---

## Key Decision Embedded in This Priority Stack

**Chat on Dialogflow (legacy) is approved as a valid launch path.**

This removes the GECX blocker. Chat no longer waits on Google's Agent Studio documentation or the Amit meeting. The legacy GCP JSON storage bucket (same data store Voice uses today) is a viable integration point. Tech debt is accepted in exchange for speed-to-market.

This is the single most significant change from pre-Chris-conversation sequencing.

---

## What This Does NOT Change

- **Amazon Connect retirement (Oct 1, 2026)** remains a hard date — it is a financial/contract obligation, not a containment workstream, and sits outside this priority stack. It must execute in parallel.
- The Tech Writing → Knowledge Catalog pipeline (#4) remains the foundational architecture for long-term containment. Its lower priority ranking reflects sequencing, not strategic importance.

---

## Sequencing Implications

| Phase | Window | Focus |
|-------|--------|-------|
| **Now → Oct 1** | May – Sep 2026 | Amazon Connect (hard date) + 1st Responder Agent (priority #1) in parallel |
| **Q4 FY26** | Oct – Dec 2026 | Chat on CRC (Dialogflow legacy) — now unblocked |
| **Q1–Q2 FY27** | Jan – Jun 2027 | Voice → Agent Studio migration; Knowledge Catalog pipeline progressing |
| **FY27 ongoing** | 2027 | KC Tuning (#5), BigQuery/Gemini ENT (#6) |
| **FY27–FY28** | 2027–2028 | Command Center maturation (#7) |
