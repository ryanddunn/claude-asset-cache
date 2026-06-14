---
type: artifact
artifact_status: Active
topics:
  - '[[TPC - CE + IT - 3yr Execution Strategy Session]]'
  - '[[TPC - FY27 Containment Strategy]]'
created_date: 2026-05-01T00:00:00.000Z
---
# TOPIC 6 - CE Tooling (Command Center)

> *Created: 2026-04-23T21:57:00.000Z*

# Topic Overview
This topic covers the full CE operational tooling stack - from how Technical Writers author and publish content, to how human support agents interact with multiple simultaneous GenAI conversations. This is a labor interface and workflow design conversation, not just a platform selection.
This topic sits under Pillar 2 - GenAI Integration into CE Operations.
---
# Dimensions of CE Tooling
## 1. Technical Writing - Authoring Process
- Current state: MadCap Flare and Search Unify in use; both targeted for retirement
- Goal: AI-assisted authoring workflow where Technical Writers produce structured, GenAI-optimized content
- Target: 85%+ AI-assisted authoring (content generation, formatting, tagging)
## 2. Technical Writing - UI + Publishing Process
- The in-house Markdown editor is the authoring and publishing tool for TW output
- TW Agent writes structured content via the Markdown editor, which produces structured files ingested by the downstream pipeline
- The Relational DB serves as the authoritative knowledge layer feeding downstream consumers (such as Google's Knowledge Catalog)
- Downstream from the Relational DB: Release Notes, User Guides, Knowledge Articles - all served from the same data structure
## 2a. Technical Writing - Non-Technical Writer Publishing Process (Future / Planned)
**Status: Future roadmap item — not current scope**
- A future operational process owned and managed by the TW team that enables non-technical writers (e.g., support staff) to publish information to the generative AI knowledge base
- The TW team owns and manages the *process and quality controls* — but does NOT perform the publishing work itself; non-technical staff do the actual publishing
- Purpose: enables formal, curated contributions from non-technical writers in a managed, governed way
- Example use case: EVB code knowledge concepts related to personal care — authored and published by support staff through the TW-managed process
- Pipeline: Non-technical writer → Markdown Editor (via TW-managed process) → Relational DB → Knowledge Catalog → Gemini for CX
- This extends the authoring pipeline to a broader contributor base without compromising data quality or pipeline integrity
## 3. Hybrid Agent UI - Human + GenAI Operations
- As Chat and CCAI scale, human agents will manage multiple simultaneous AI-handled conversations
- A purpose-built hybrid UI is needed to support a single human agent supervising, intervening in, and handing off across multiple GenAI interactions
- Key design questions: What triggers human intervention? How does an agent see conversation state across multiple AI threads? What does escalation look like?
---
# Key Notes by IT Group
---
# Decisions
- **Resolved:** The in-house Markdown editor is the chosen authoring and publishing tool for TW. MadCap and Notion are both retired from consideration.
- Agree on the hybrid agent UI design scope and ownership.
- How does the Knowledge Catalog data object impact our build out of these tools?
---
# Google Next Pivots
> Integration of Google's Knowledge Catalog as a data structure fed by Tech Writing's daily work. The in-house Markdown editor is the authoring tool feeding this pipeline.
# Risks
- Tech Writing Data Structure
- Hybrid Interface - GenAI + Human
- Observability
