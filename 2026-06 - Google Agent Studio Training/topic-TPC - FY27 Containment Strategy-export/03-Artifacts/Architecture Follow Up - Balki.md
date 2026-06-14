---
type: artifact
functional_class: Technical
artifact_status: Needs Review
created_date: 2026-06-10T00:00:00.000Z
topics:
  - '[[00-Topics/TPC - FY27 Containment Strategy]]'
entities:
  - '[[05-Entities/Balki Nakshatrala]]'
  - '[[05-Entities/Vivek Pissay]]'
  - '[[05-Entities/Abhirup Dash]]'
file: ''
notion_url: ''
---

# Architecture Brief: Knowledge Data Pipeline for Containment Strategy

## Purpose

This document provides the pre-work requested before architecture validation can proceed. It covers the current state content process, the challenges we are trying to resolve, the specific use cases the knowledge architecture must serve, and the future state vision. 

Ryan Dunn + Abhirup Dash represent technical authority from the CE space on this topic. Please send any questions or feedback to them. 

---

## Current State

### Content Creation Process

WellSky's Technical Writing (TW) team authors all product documentation. Today, authors work in MadCap Flare (Desktop App, not SaaS) as the primary authoring tool. Documents are produced as individual content units... user guides, release notes, knowledge articles, and the CRC Website (Customer Resource Center) help site. The authoring workflow is roughly:

1. Engineering completes a feature or fix and documents it in JIRA (two required fields: "Release notes needed" toggle and a release notes entry field for bugs/fixes).
2. TW pulls the JIRA data via an AI agent that is already in production, auto-drafts release notes, and the writer reviews and edits.
3. TW authors publish to two destinations: Salesforce Knowledge (knowledge articles surfaced to support agents via Salesforce Service Cloud) and the CRC web portal.

An AI release notes agent has been in production for some time. It reduced release note production time by approximately 60%, meaning TW can turn around a draft in under one business day once all upstream JIRA fields are complete. The constraint on speed is not TW - it is upstream data completeness from Solutions and Engineering.

### Content Types and Volume

| Content Type | Format | Update Frequency |
|---|---|---|
| User Guides | HTML (CRC) + PDF | Per product release cycle |
| Release Notes | PDF + HTML | Bi-weekly (sprint cadence) |
| Knowledge Articles | HTML (Salesforce) | As needed, release-driven |
| CRC Help Site | HTML | Per release |

Document size is not trivial. Files can reach into the hundreds of megabytes when the full guide is consolidated.

### Current Systems and Storage

| System | Role |
|---|---|
| MadCap Flare | Primary TW authoring tool (being replaced with in-house Markdown Editor) |
| JIRA | Source of release content metadata and triggers |
| Salesforce Knowledge | Repository for knowledge articles surfaced to support agents |
| CRC Web Portal | Customer-facing static documentation |
| GCP Bucket (JSON) | Storage layer for CCAI knowledge — TW documentation is extracted into JSON format and uploaded here |
| Google Contact Center AI (GECX) | Consumes the GCP JSON bucket as its foundational knowledge layer to generate answers to customer questions |

**How the current CCAI knowledge pipeline works — and why it matters for this engagement:**

TW authors produce documentation in MadCap Flare. That documentation is extracted into JSON format and the resulting JSON files are placed in a GCP bucket. The Google Contact Center AI platform references that GCP bucket directly as its foundational knowledge structure when generating answers to customer questions.

There is no material tuning of this content. The JSON files are documents written for human readers — extracted and uploaded as-is. There is no metadata enrichment, no authority weighting, no topic tagging, no chunking strategy, and no structural signaling of any kind that would make the generative AI models in the Contact Center AI platform more effective at surfacing the right answer. The model is working with human-oriented documentation with no AI-specific optimization applied.

This is the core problem this initiative is designed to solve. The current approach is a functional baseline, but it does not leverage the capabilities of the CCAI platform. Everything in this document — the metadata enrichment layer, the graph DB, the structured Markdown pipeline — is oriented toward replacing this with an architecture designed for generative AI consumption from the ground up.

### Current Consumers

| Consumer | Internal / External | Access Point |
|---|---|---|
| WellSky Support Agents | Internal | Salesforce Service Cloud (knowledge articles) |
| WellSky Customers | External | CRC web portal (HTML documentation) + PDF release notes |
| GECX / Gemini for CX (Voice) | Public-facing AI channel | Gemini Agent Studio — migration from existing Dialogflow-based voice |
| GECX / Gemini for CX (Chat) | Public-facing AI channel | Net-new channel, embedded in CRC web portal — not yet live |
| TW Authors (internal tooling) | Internal | Release notes agent, document editing tools |

The GECX chat and voice channels are the primary high-volume, public-facing consumers. Chat is a new build on Agent Studio. Voice is a migration of an existing capability. Both channels are grounded by the same knowledge layer. Volume is high — this is customer-facing support at WellSky scale, not an internal low-frequency use case.

---

## Current State Challenges

| Problem | Current State | Target State |
|---|---|---|
| No structured knowledge layer | TW documentation is extracted to JSON and placed in a GCP bucket — the CCAI platform consumes these raw, human-oriented documents with no graph structure, no metadata, and no AI-optimized organization | A structured Knowledge Catalog (graph DB) that CCAI queries against enriched, AI-optimized content |
| No metadata enrichment layer | Documents have no authority weighting, topic tagging, or structured metadata beyond file name | Each document has a structured metadata block that carries weight, product, and audience signals into the graph |
| Web + PDF publishing | TW documentation is published to a PDF + web destination for customer access | Preserved in the future state; the architecture must continue to support PDF + web-published documentation alongside AI consumption |
| Containment rate gap | Current measured containment rate is 22%, against an FY27 KPI of 50% | 50% containment by end of FY27; primary lever is grounding quality |

---

## Use Cases

The architecture needs to serve the following use cases, in priority order:

**Use Case 1: GECX Tier-0 Containment — Improve GenAI Answer Accuracy**

The primary outcome. Gemini for CX (chat and voice) needs to ground responses in WellSky product documentation. Today, grounding is based on untuned JSON documents in a GCP bucket — human-oriented content with no AI-specific structure, metadata, or authority signals applied. Better grounding directly increases the containment rate. The target is 50% containment by end of FY27 — up from 22% today. This is a direct KPI for WellSky CE leadership with visibility to the President, COO, and CFO.

**Use Case 2: Metadata-Weighted Content Authority for AI Tuning**

Tom (Problem Management) and Gage (knowledge content team) need the ability to adjust which documents carry more weight in the model's responses — without requiring an engineering deployment. The vision is a metadata section on each document in the authoring editor where Tom and Gage can set a priority or authority weight on strategic content. That metadata carries through the pipeline into the graph, giving the AI a signal to favor high-authority content in grounding. This is a human-in-the-loop tuning mechanism that does not require prompt changes or retraining.

**Use Case 3: 1st Responder Agent — Case-Triggered Knowledge Retrieval**

When a support agent opens a Salesforce case, an automated agent retrieves the most relevant knowledge articles from the graph and surfaces them in the Salesforce UI. The current implementation is a human-triggered lookup; the goal is automation on case view or case creation. The Salesforce team (Patrick) is building the agent integration; the knowledge graph is the retrieval layer this agent queries. This is an internal use case, but it directly affects handle time and first-contact resolution.

**Use Case 4: Legacy Output Parity — CRC HTML Rebuild and PDF Generation**

TW today produces PDFs (release notes, user guides) and HTML as their primary deliverables to clients. The architecture must preserve this output. Clients expect PDF release notes; not all customer contacts log into the application. The relational DB is the mechanism Ryan proposed to enable rebuilding these formats from the same Markdown source — this is not a GenAI use case, but it is a hard requirement for the architecture to be viable. If Balki and Vivek can propose an alternative path that fulfills this requirement without a relational DB, that is welcome.

---

## Future State

### Desired Architecture

The end-state pipeline runs top to bottom as follows:

```
TW Editor (Markdown + Metadata UI)
  → Markdown file (with frontmatter metadata block)
    → ETL / DPL ingestion
      → Relational Database
        → [Branch A] Knowledge Catalog (Google Graph DB) → Gemini for CX Agents (chat + voice)
        → [Branch B] Build Pipeline → CRC HTML rebuild + PDF (release notes, user guides)
```

Authors write in a custom Markdown editor (being built by Phil Raynes and Mackenzie). The editor has a metadata section per document — title, product, audience, and an authority weight field that Tom and Gage can edit on strategic content. On save, the editor writes a Markdown file with the metadata embedded in frontmatter. An ETL/DPL process ingests the Markdown file into a relational database, preserving structure (paragraph-level sequencing) and metadata. The relational DB then feeds two consumers: the Knowledge Catalog (Google's graph database) for AI grounding, and a build pipeline for legacy HTML/PDF outputs.

The Knowledge Catalog is the authoritative grounding layer for both Gemini for CX chat and voice. Both channels run on Google Agent Studio. Chat is a net-new channel embedded in the rebuilt CRC web portal. Voice is a migration from the existing Dialogflow-based IVR.

Notion and MadCap Flare have both been ruled out as part of this pipeline.

### Metadata Enrichment

The metadata block is authored in the same TW editor. Fields are expected to include: document title, product(s) covered, content type (user guide, release note, knowledge article), audience (internal/external, role-based), and authority weight (a numeric or ordinal value set by Tom or Gage). Metadata entry is voluntary per document — not every document needs enrichment, but strategic high-traffic documents should be enriched. The metadata must survive the full pipeline: Markdown file → relational DB → graph — without being stripped or lost in the ETL process.

A future extension of the metadata layer is terminology normalization. WellSky currently uses terms such as "solution," "platform," and "application" interchangeably across documentation, creating inconsistency in what the AI model learns and surfaces. A controlled vocabulary or taxonomy field — applied by TW authors at the document level — could normalize terminology across the knowledge layer and is a prerequisite for the longer-term legal alignment consideration noted at the end of this document.

### Dual-Output Requirement

The same source content must serve both GenAI consumption and human-readable legacy formats. This is not optional — clients expect PDFs and the CRC web site. The relational DB approach was proposed as the mechanism to enable both: paragraph-level storage allows document reconstruction for PDF/HTML, while also feeding the graph. If there is a more optimized architecture that satisfies both requirements without a relational DB, that is a design decision for Balki and Vivek to propose.

---

## Open Questions

These are the decisions Ryan is asking Balki and Vivek to resolve. Ryan's team will not proceed on these without architectural guidance.

**1. Single Source of Truth**
Which layer is authoritative: the Markdown file, the relational DB, the Knowledge Catalog (graph DB), or BigQuery? When a document is updated and the author hits save, what constitutes the canonical version? If the relational DB is the source of truth, what happens to the Markdown file? If the Markdown file is authoritative, how does the pipeline guarantee the graph stays in sync?

**2. Relational Database Necessity**
Ryan proposed the relational DB specifically to enable legacy output (PDF, CRC rebuild) from the same source as GenAI content. Vivek and Balki raised the question in the meeting of whether a relational DB is necessary given that this is unstructured content. If there is an alternative architecture — for example, driving legacy output directly from the Markdown files with a separate build process — that eliminates the relational DB while still fulfilling the dual-output requirement, what does that look like, what are the tradeoffs, and how do we continue to produce the legacy artifacts (CRC website + PDFs)?

**3. Graph Update / Incremental Sync**
Content is updated on a release cadence plus ad hoc updates as products change. When a document is updated, what is the mechanism to reflect that change in the graph incrementally, without re-ingesting the full content catalog? What are the constraints and recommended approach for graph maintenance at this update frequency?

**4. Custom App vs. Gemini Enterprise**
There are both internal use cases (1st Responder, case auditor, TW tooling) and a high-volume public-facing use case (GECX chat and voice for client-facing support). The public-facing channel is not low-volume. For the agent consumption layer, which approach is recommended — a custom application, Gemini Enterprise, or some combination — and what drives that decision given the scale and the dual internal/external use requirement?

**5. Volume, Cost, and Model Selection**
Given that GECX is a high-volume public-facing channel alongside lower-volume internal use cases, what model and infrastructure choices are appropriate? Are there cost or quota considerations that impact the architecture decision between approaches?

---

## Long-Term Architectural Consideration: Terminology & Legal Alignment

*This is not a Phase 1 requirement and is not a blocker for the architecture being validated here. It is flagged as a design consideration to ensure the architecture does not make it harder to address later.*

WellSky's Head of Legal has identified a gap between the terminology used in contractual language and the terminology used in product documentation. Because documentation is the foundational knowledge source for the AI models in this architecture, that misalignment propagates directly into AI-generated responses. As a simple example, WellSky uses "solution," "platform," and "application" interchangeably across documentation, but these terms may carry distinct meaning in a contractual context. This issue is not limited to this project; marketing and other functions operate with the same inconsistency.

The long-term goal is alignment between contractual language, documentation terminology, and AI outputs. Achieving this has two components: (1) TW authors adhering to a controlled vocabulary when writing content, and (2) terminology or taxonomy metadata fields in the enrichment layer that can tag and normalize terms at the document level. The metadata architecture being proposed here is the natural place for this to land over time. No immediate action is required, but the architecture should not foreclose this capability.
