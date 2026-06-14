---
type: artifact
functional_class: Strategic
artifact_status: Active
created_date: '2026-05-18'
topics:
  - '[[TPC - CE + IT - 3yr Execution Strategy Session]]'
  - '[[TPC - FY27 Containment Strategy]]'
---

# Critical Path — CE + IT 3yr Execution Strategy

This artifact tracks the critical path for each workstream in the CE + IT 3-year execution strategy. Workstreams are added incrementally as critical paths are defined.

---

## Workstream — Tech Writing

### Target Flow

```
Markdown Editor  →  Markdown Files (GitHub)  →  ETL  →  Relational DB  →  Knowledge Catalog  →  GenAI Agents
```

---

### Gate 0 — Blocking Decisions (Must Close Before Any Build Work)

These are prerequisites. Everything downstream is shaped by them.

**Decision 1: DB Type — Relational vs. Document DB**
Currently unresolved. Adam reframed it as "a path, not a hard requirement." Vivek wants to evaluate document DBs, smart storage, and Knowledge Catalog-native options before committing. Schema design and ETL cannot be defined until this is settled.
- **Owner:** Abeerup (research) → Vivek (decision)
- **Input:** Google scoping meeting via Josh H should inform this

**Decision 2: RACI — Business vs. IT ownership of the pipeline**
Flagged in Topic 1 as a formal prerequisite to execution. Without it, Vivek's team becomes de facto admins of TW content — the primary governance risk. Who builds? Who maintains? Who owns quality?
- **Owner:** Ryan + Brad + Vivek
- **Output:** Written RACI document — not just verbal alignment

**Decision 3: Authoring Tool — In-House Editor Scope**
Patrick's TW agent is ~60–70% built (Jira pull, draft, diff, editor review). The last 30% — publishing layer and version control — is unbuilt and undefined. Phil McKenzie feedback (closest to the actual process) is the critical input before the publishing layer can be scoped.
- **Owner:** Jason N (product owner) + Patrick (dev)
- **Action:** Phil McKenzie feedback session is the immediate blocker

---

### Phase 1 — Schema & Structure Definition
*Unblocked once Decision 1 (DB type) is made. Runs parallel to Phase 2.*

**Step 1 — Define content schema + metadata taxonomy**
Define the object structure for every content type: Release Notes, User Guides, Knowledge Articles, etc. Includes field definitions, object relationships, required vs. optional metadata, and how the schema maps to the downstream Knowledge Catalog glossary.
- **Owner:** Jason N + John McCall
- **Input:** DB type (Decision 1), inventory of existing MadCap content types
- **Output:** Schema document — object types, required fields, metadata rules

**Step 2 — Design the ETL specification**
Map the full data flow technically: markdown file structure → DB tables/collections → Knowledge Catalog ingestion format. This is a real data engineering problem — schema design, change-data-capture, error handling — not a one-time export.
- **Owner:** Vivek
- **Input:** Schema (Step 1), DB type (Decision 1)
- **Output:** ETL technical spec covering all three hops in the pipeline

---

### Phase 2 — Complete the Authoring Tool
*Runs parallel to Phase 1. Does not depend on DB type decision.*

**Step 3 — Collect user feedback and define publishing layer requirements**
Before Patrick builds the last 30%, Jason N needs to sit down with Phil McKenzie to define exactly what the publishing layer needs to do: How does a tech writer approve a PR? What does the version control workflow look like? What does "published" mean operationally?
- **Owner:** Jason N
- **Action:** Schedule Phil McKenzie session — this is the blocker for Step 4

**Step 4 — Build publishing layer + version control**
Complete the TW agent: PR-based publishing to GitHub, version history, and the editor review → approve → publish flow. The output of this tool is the markdown files that feed the entire downstream pipeline.
- **Owner:** Patrick (dev) / Jason N (product owner)
- **Input:** Publishing layer requirements (Step 3)
- **Output:** Working markdown editor producing structured files in GitHub

**Step 5 — Formalize the publishing operations process**
Document how tech writers use the tool day-to-day: authoring workflow, PR review standards, quality gates before a file is considered pipeline-ready. Jason N owns this as knowledge curator — this is the operational integrity layer.
- **Owner:** Jason N
- **Input:** Working tool (Step 4), RACI (Decision 2)

---

### Phase 3 — Build the Storage Layer & ETL
*Requires Phase 1 complete + Decision 2 (RACI) closed.*

**Step 6 — Provision and configure the Relational DB**
Stand up the database and implement the schema from Step 1. RACI must be in place before build begins so there is a formal infrastructure owner from day one.
- **Owner:** Vivek / Engineering (IT build); Jason N (business content owner)
- **Input:** Schema (Step 1), RACI (Decision 2)

**Step 7 — Build Markdown → Relational DB ETL**
Ingest pipeline that reads markdown files from GitHub and writes structured records into the DB. Requires knowing both what the files look like (authoring tool output, Step 4) and what the DB expects (Step 6).
- **Owner:** Vivek / Engineering
- **Input:** ETL spec (Step 2), DB live (Step 6), file format from publishing tool (Step 4)

---

### Phase 4 — Knowledge Catalog Integration
*Step 8 can start immediately, in parallel with all other phases. Steps 9–10 require pipeline to be live.*

**Step 8 — Scope Knowledge Catalog capabilities with Google** *(start now)*
The "Google scientists" meeting Ryan already requested via Josh H. Must answer: How does ingestion work — push or pull? What format does KC expect? How do agents query it? How does auth work? What's the indexing latency SLA? This scoping drives the KC integration design.
- **Owner:** Ryan / Josh H
- **Status:** Meeting already requested — in motion

**Step 9 — Build Relational DB → Knowledge Catalog pipeline**
The sync layer from DB to KC. Covers cadence (real-time vs. batch), error handling, and governance/IAM scoping.
- **Owner:** Vivek / IT GenAI CoE
- **Input:** KC scoping (Step 8), DB live (Step 6)

**Step 10 — Configure Knowledge Catalog for agent-ready consumption**
Semantic curation, glossary configuration, access control, retrieval tuning. KC is not automatic — it must be configured to surface the right content to agents. TW team owns editorial rules; IT owns platform configuration.
- **Owner:** IT (platform config) + Jason N (editorial rules / content governance)
- **Input:** Data flowing into KC (Step 9)

---

### Phase 5 — Agent Connection
*Only this phase is blocked by GECX availability.*

**Step 11 — Connect Knowledge Catalog to GenAI agents**
Configure GECX / Virtual Agents to use Knowledge Catalog as the grounding source. This is the payoff step and is **gated on Google confirming GECX availability**. All of Phases 1–4 are executable today without it.
- **Owner:** Vivek / Engineering + Ryan's team
- **Hard blocker:** GECX availability — no timeline confirmed; Josh H + Amit meeting must happen first

---

---

### Future Roadmap — TW Operational Publishing Process for Non-Technical Writers
*Status: Future / Planned — not current scope. Formally tracked here for roadmap visibility.*

**What it is:** A future operational process, owned and managed by the TW team, that allows non-technical writers (e.g., support staff) to publish information to the generative AI knowledge base through a TW-governed workflow.

**Ownership model:** TW team owns and manages the *process and quality controls*. Non-technical staff perform the actual publishing work. TW does not own the content — they own the pipe.

**Purpose:** Enables formal, curated contributions from non-technical contributors in a managed, governed way — extending the authoring pipeline without compromising data quality.

**Example use case:** EVB code knowledge concepts related to personal care — authored and published by support staff through the TW-managed process.

**Pipeline:**
`
Non-technical writer → Markdown Editor (via TW-managed process) → Relational DB → Knowledge Catalog → Gemini for CX
`

**Dependencies:** Requires Phase 2 (Authoring Tool complete), Phase 3 (Relational DB live), and Phase 5 (Ops process formalized) before this process can be defined and rolled out.

---

### Dependency Map

| Step | Blocked By |
|---|---|
| Step 1 — Schema | Decision 1 (DB type) |
| Step 2 — ETL spec | Decision 1 + Step 1 |
| Step 3 — Phil feedback | Nothing — do this week |
| Step 4 — Publishing tool | Step 3 |
| Step 5 — Ops process | Step 4 + Decision 2 |
| Step 6 — DB provision | Decision 1 + Decision 2 + Step 1 |
| Step 7 — Markdown→DB ETL | Steps 2, 4, 6 |
| Step 8 — KC scoping | Nothing — do this week |
| Step 9 — DB→KC pipeline | Steps 6, 8 |
| Step 10 — KC config | Step 9 |
| Step 11 — Agent connection | Step 10 + GECX availability |

---

### Immediate Actions (No Dependencies)

Three items unblock the entire path and have nothing waiting on them:

1. **Schedule Phil McKenzie** — Jason N's user feedback session. Defines publishing layer requirements for Patrick's build. (Decision 3 / Step 3)
2. **Google scoping meeting** — Josh H + Amit call on KC ingestion, agent integration, and auth. Already requested. (Step 8)
3. **RACI alignment session** — Ryan, Brad, Vivek. ~60 minutes. Formal prerequisite to any pipeline build work. (Decision 2)
