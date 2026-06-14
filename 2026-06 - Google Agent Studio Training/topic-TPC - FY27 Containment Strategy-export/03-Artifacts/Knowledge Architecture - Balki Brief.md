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

# Knowledge Architecture Brief
*Prepared for: Balki Nakshatrala (GenAI Architect) + Vivek Pissay*
*Prepared by: Ryan Dunn*

---

## 1. Purpose

> *One paragraph: why this document exists, what decision or alignment it is meant to enable, and what Ryan is asking Balki and Vivek to do with it.*

---

## 2. Current State

### Content Creation Process
> *Who creates content today? What tools do they use? What is the authoring workflow from start to finish?*

### Content Types & Volume
> *What types of documents are produced (HTML, PDF, release notes, user guides, knowledge articles, etc.)? Approximate volume and average file size.*

| Content Type | Format | Approx. Volume | Avg. Size | Update Frequency |
|---|---|---|---|---|
| | | | | |
| | | | | |
| | | | | |

### Current Systems & Storage
> *Where does content live today? What systems store it, serve it, or index it?*

### Current Consumers
> *Who uses this content? Internal support staff only, or also external customers? Through what interface (Salesforce, CCAI/GECX, web, PDF download, etc.)?*

| Consumer | Internal / External | Access Point | Volume / Frequency |
|---|---|---|---|
| | | | |
| | | | |

---

## 3. Current State Challenges

> *What is not working well today? Balki asked for specific metrics — fill in what's measurable.*

| Problem | Current Metric | Target / Desired State |
|---|---|---|
| | | |
| | | |
| | | |

---

## 4. Use Cases to Address (3–5)

> *Vivek and Balki asked: what is the primary outcome of this metadata and graph? List the 3–5 specific use cases you are trying to enable, in priority order.*

**Use Case 1:** *(e.g., Better GenAI answer accuracy for GECX / Tier-0 containment)*
> Description, who benefits, what success looks like

**Use Case 2:** *(e.g., Metadata-weighted content authority for AI tuning)*
> Description, who benefits, what success looks like

**Use Case 3:** *(e.g., Agent routing / document discovery)*
> Description, who benefits, what success looks like

**Use Case 4 (optional):**
> Description, who benefits, what success looks like

**Use Case 5 (optional):**
> Description, who benefits, what success looks like

---

## 5. Future State Vision

### Desired Architecture (High-Level)
> *Describe the end-state in plain language. What does the content pipeline look like from authoring to consumption? Reference the Mermaid diagram in TPC - FY27 Containment Strategy if helpful.*

### Metadata Enrichment
> *What metadata fields are envisioned? Who populates them (TW authors, Tom & Gage, automated)? When in the workflow?*

### Dual-Output Requirement
> *Describe the requirement to support both GenAI consumption (Graph DB) AND legacy human-readable outputs (PDFs, CRC website, release notes) from the same source content.*

### Integration Points
> *List key systems this architecture must integrate with (GECX / CCAI, Salesforce, BigQuery, GCS, 1st Responder agent, etc.).*

---

## 6. Open Architecture Questions (For Balki + Vivek)

> *These are the questions Ryan needs the architects to resolve. Do not fill these in — these are the decisions Ryan is handing to the team.*

1. **Single source of truth** — Which layer is authoritative: the Markdown file, a relational DB, Graph DB, or BigQuery? What are the tradeoffs?

2. **Relational DB necessity** — Is a relational database required to support legacy output (PDF, CRC), or is there a more optimized path that still fulfills that requirement?

3. **Graph update / incremental sync** — When a document is updated, how does the graph reflect that change incrementally without full re-ingestion?

4. **Custom app vs. Gemini Enterprise** — For the agent consumption layer, which approach is recommended given the scale (high-volume, public-facing GECX + internal use cases)?

5. **Volume & cost implications** — Given expected usage volume, what model and infrastructure choices are appropriate?

---

## 7. Next Steps

| Action | Owner | Target Date |
|---|---|---|
| Ryan sends this document to Balki + Vivek for review | Ryan Dunn | |
| Balki / Vivek provide architecture recommendations | Balki + Vivek | |
| Abhirup aligns with Balki + Vivek on enterprise design | Abhirup Dash | |
| Architecture review meeting | All | |
