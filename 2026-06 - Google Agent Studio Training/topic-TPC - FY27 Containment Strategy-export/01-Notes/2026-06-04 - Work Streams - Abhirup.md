---
fileClass: note
type: note
created_date: 2026-06-04T00:00:00.000Z
notes_status: Reviewed
meta: []
topics:
  - '[[TPC - FY27 Containment Strategy]]'
entities:
  - '[[Abhirup Dash]]'
---

Here's a briefing you can hand to Abhirup:

---

## FY27 Containment Strategy — Abhirup Dash Ownership Brief

**Prepared by:** Ryan Dunn
**Context:** FY27 Containment Strategy — GenAI-driven reduction of human-handled support volume across WellSky's customer base

---

### Strategy Overview

The FY27 Containment Strategy is a set of 10 coordinated work streams designed to modernize how WellSky delivers customer support through generative AI. The north star: customers get answers faster, human agents handle fewer routine inquiries, and WellSky's documentation and knowledge architecture evolves to support both goals simultaneously.

The backbone of this strategy is a modern **knowledge pipeline** — a data architecture that takes Technical Writing content, runs it through a structured relational database, and feeds it into a graph database that powers our GenAI voice and chat channels. You own the core of that pipeline.

---

### Your Ownership Areas

#### **WS-4 — Knowledge Pipeline** *(Primary Ownership)*
You own the architecture and development oversight of the end-to-end pipeline that moves content from Technical Writing's Markdown files → relational database (with metadata enrichment) → graph database. This pipeline is the foundation everything else builds on.

**Key alignments:**
- **WS-5 (TW Markdown Editor, Jason Nicol)** — Jason's team defines the Markdown output format and metadata schema. Your pipeline consumes their output. Close alignment here is critical — the metadata taxonomy coming out of WS-5 determines what your relational DB can query and enrich.
- **WS-7 (Graph DB, Vivek Pissay)** — Your pipeline populates the graph DB that Vivek's team manages. Coordinate on data structure, ingestion timing, and schema design.

---

#### **WS-6 — Legacy TW Artifact Build** *(Primary Ownership)*
Once the relational database is built, you own the extraction layer that produces WellSky's existing documentation deliverables — maintaining full parity with how customers consume content today.

**Two output types:**
1. **Website (CRC)** — Query the relational DB and publish documentation to the Customer Resource Center as HTML. Replaces the current MadCap Flare-driven publish process.
2. **PDF Generation** — A scheduled process (e.g., daily Cron job) that identifies new or updated documents in the relational DB and builds the corresponding PDFs — Release Notes, Knowledge Articles, User Guides. Same formats, new pipeline.

This work stream is about continuity — customers and internal teams should experience no change in how they consume documentation while we modernize the infrastructure underneath.

---

#### **WS-7 — Graph DB Migration** *(Partner Role — Vivek Pissay leads)*
Vivek and the GenAI Center of Excellence own this work stream. Your role is to partner closely on the architectural handoff — ensuring the knowledge pipeline (WS-4) feeds the graph DB with the right structure and metadata for GenAI consumption. You'll also be involved in the metadata tuning work that comes out of WS-5, which directly affects how the graph DB is configured for voice and chat retrieval.

---

#### **WS-9 — Solutions Integration** *(Awareness + Long-Term Support)*
Not an immediate priority, but one you should understand. This work stream creates API integration paths between WellSky's solution platforms (Home Health, Connected Networks, Personal Care, etc.) and GECX — the Gemini-powered voice and chat channels. The concept: a customer interacts with our GenAI agent, which executes an action against a solution's API in real time.

Partners in this work include enterprise platform owners like **Katie Rogers (Salesforce)** and individual solution teams. When WS-1 (Chat v1) and WS-2 (Voice v2) are stable and WS-7 is mature, this is the natural next frontier.

---

### How Your Work Fits the Timeline

Your most critical work lands in **Q1–Q2 FY27**. WS-4 begins immediately and must deliver by Q2 to unblock WS-6 and WS-7. WS-6 follows in Q2. WS-9 is a Q3+ conversation.

The sequencing makes you a critical path dependency — WS-6, WS-7, and WS-8 (External Content Publishing) all flow from your pipeline being healthy.

---

Want me to adjust the tone, add anything about the team structure, or trim it down?