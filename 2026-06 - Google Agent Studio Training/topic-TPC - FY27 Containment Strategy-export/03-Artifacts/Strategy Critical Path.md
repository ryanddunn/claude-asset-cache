---
type: artifact
functional_class: Strategic
artifact_status: Active
created_date: '2026-05-18'
topics:
  - '[[TPC - CE + IT - 3yr Execution Strategy Session]]'
  - '[[TPC - FY27 Containment Strategy]]'
---

# Knowledge Data
* Mark Down Editor
	* define tool, adhear to ETL requirements
	* signoff on design by CoE + work assignments to team
	* TW owns design, ops workflow alignment with solutions
	* Integration with TW Tooling
* Relational Database (Tech Write)
	* Ingest Markdown Files into Relational Data Structure
	* ==**Critical path work item, tech write presentation layer (CRC Website, Documents)**==
	* signoff on design by CoE + work assignments to team
* Knowledge Catalog
	* Integrate Relational Data Structure 
	* GraphDB 
	* ==Critical Path to chat ==
	* signoff on design by CoE + work assignments to team

# Tech Writing Presentation Layer
* CRC Website using Relational Data
	* ==Define Design, Navigation, does this include chat on v1? ==
	* ==DEPENDANT on Relational Database (Tech Write)
	* signoff on design by CoE + work assignments to team
	* signoff on design by Marketing? Stakeholders?
* Documents (RN, UG, KA, etc)
	* Create documents using Relational Data Structure
	* ==DEPENDANT on Relational Database (Tech Write)
	* signoff on design by CoE
	* signoff on design by Marketing? Stakeholders?

# Signal Processing
* Closed Loop Agent
	* This get information over to PRODUCT / ENGINEER
	* Work in progress
	* Abhirup
* Client Success Signals
	* JW - need to define this, it is a new agent, like "closed loop" but sends information to Client Success (mad customer, customer not using solution, etc)
	* goes to data set in BigQ
	* McCall own confirm output usable 
	* Abhirup
* Hybrid UI for Support
	* Need to design, implement, etc
	* Identify Support Champion + Leader
	* Scope feature set
	* start of this is 1st responder agent / Triage agent, start here with CE Command Center
	* Evolve into AI Tooling hub, goal to close cases using AI
	* Observability critical
	* negative trends imply outage, human in loop alerts here

# Chat — Two Distinct Workstreams

## Workstream A: Gemini for CX Chat (New Build)
* Actively scoping Gemini for CX chat inside Agent Studio technology
* This is a new channel being built on Agent Studio from the start — not a migration
* VA Design (Chat on Agent Studio)
* VA Implementation (Chat on Agent Studio)
* Annette / Corbin / Michael - define phases
* Integration into CRC
	* ==NOT DEPENDANT - Chat can go into legacy CRC or new version, works in either.==
	* Not a tech block, business would likely want launched together
* Integration into Home / PC
	* Multiple solutions interested in chat
	* Might be a quicker go to market than CRC chat integration
* Awareness on design by CoE
* CoE design VA to API Interface
* RD - Scale concern here, architecture sign off

## Workstream B: Gemini for CX Voice (Migration / Upgrade)
* Planning to upgrade the existing voice channel from Dialogflow CX designer to Agent Studio
* This is a migration/upgrade of an existing channel — not a new build
* VA Design (Voice — Agent Studio Migration)
* VA Implementation (Voice — Agent Studio Migration)
* Annette / Corbin / Michael - define phases; coordinate with Amazon Connect retirement track
* Requires Dialogflow deprecation timeline from Google
# Amazon Connect
* all lines on GE CX

# Tooling
* TW Authoring
* TW Publishing
* Both TW - continue at pace for Patrick? Build against this set of design specs
* Hybrid UI Layer mentioned above

## Future Roadmap — TW Operational Publishing Process for Non-Technical Writers
**Status: Future / Planned — not current scope**
* TW team creates an operational process enabling non-technical writers (e.g., support staff) to publish to the generative AI knowledge base
* TW owns the process and quality controls — non-technical staff do the actual publishing work
* Example use case: EVB code knowledge concepts related to personal care
* Pipeline: Non-technical writer → Markdown Editor (via TW-managed process) → Relational DB → Knowledge Catalog → Gemini for CX

---

# Critical Path Tracking Table

| Area              | Work Item                                         | Detail                                                                                                       |      Critical Path      | Owner / Role                                  | Dependencies                      | Open Questions                                                   | Status      |
| ----------------- | ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ | :---------------------: | --------------------------------------------- | --------------------------------- | ---------------------------------------------------------------- | ----------- |
| Knowledge Data    | Markdown Editor — Define Tool                     | Adhere to ETL requirements; integration with TW Tooling                                                      |                         | TW (lead), CoE (signoff)                      |                                   | What tool? What are ETL requirements?                            |             |
| Knowledge Data    | Markdown Editor — Design Signoff                  | CoE signoff + work assignments to team                                                                       |                         | CoE, TW                                       | Markdown Editor tool defined      |                                                                  |             |
| Knowledge Data    | Relational Database — Ingest Markdown             | Ingest Markdown files into relational data structure                                                         |            ✅            | TW (design), Solutions (ops workflow)         | Markdown Editor                   |                                                                  |             |
| Knowledge Data    | Relational Database — Design Signoff              | CoE signoff + work assignments to team                                                                       |                         | CoE                                           | Relational DB design complete     |                                                                  |             |
| Knowledge Data    | Knowledge Catalog — Integration                   | Integrate relational data structure; GraphDB                                                                 | ✅ Critical path to Chat | CoE                                           | Relational Database               |                                                                  |             |
| Knowledge Data    | Knowledge Catalog — Design Signoff                | CoE signoff + work assignments to team                                                                       |                         | CoE                                           | Knowledge Catalog design complete |                                                                  |             |
| Tech Writing      | CRC Website — Design & Navigation                 | Define design, navigation, feature scope                                                                     |                         | CoE, Marketing, Stakeholders                  | Relational Database               | Does v1 include chat? Who are stakeholder signoff owners?        |             |
| Tech Writing      | CRC Website — Design Signoff                      | CoE signoff + Marketing/Stakeholder signoff                                                                  |                         | CoE, Marketing                                | CRC Website design complete       | Who owns Marketing signoff?                                      |             |
| Tech Writing      | Documents (RN, UG, KA, etc) — Build               | Create all document types using relational data structure                                                    |                         | TW, CoE                                       | Relational Database               |                                                                  |             |
| Tech Writing      | Documents — Design Signoff                        | CoE signoff + Marketing/Stakeholder signoff                                                                  |                         | CoE, Marketing                                | Documents design complete         |                                                                  |             |
| Signal Processing | Closed Loop Agent                                 | Routes signals to Product / Engineering                                                                      |                         | Abhirup                                       |                                   |                                                                  | In Progress |
| Signal Processing | Client Success Signals Agent                      | New agent — routes signals to Client Success (at-risk customers, low usage, etc); output to BigQuery dataset |                         | Abhirup, JW (define), McCall (confirm output) | BigQuery dataset                  | Define agent scope with JW; confirm BigQuery output is usable    |             |
| Signal Processing | Hybrid UI for Support — Design                    | Design hybrid UI; identify Support Champion + Leader; scope feature set                                      |                         | TBD — Support Champion needed                 |                                   | Who owns / leads Support tooling? What is the feature set?       |             |
| Signal Processing | Hybrid UI — Phase 1: 1st Responder / Triage Agent | Start with CE Command Center triage agent                                                                    |            ✅            | TBD<br>JW -> Cassie                           | Hybrid UI design                  |                                                                  |             |
| Signal Processing | Hybrid UI — Phase 2: AI Tooling Hub               | Evolve into AI Tooling Hub; goal to close cases using AI; observability critical; negative trend alerting    |                         | TBD                                           | Phase 1 complete                  | What does observability look like? Human-in-loop alert design?   |             |
| Chat — New Build  | Gemini for CX Chat — Scoping                      | Actively scoping Gemini for CX chat inside Agent Studio technology; new channel, not a migration             |                         | Annette, Corbin, Michael                      |                                   | Agent Studio availability confirmation                           | In Scoping  |
| Chat — New Build  | VA Design (Chat)                                  | Define virtual assistant design for Chat on Agent Studio; phases TBD                                         |                         | Annette, Corbin, Michael                      | Agent Studio available             | Define phases with Annette / Corbin / Michael                    |             |
| Chat — New Build  | VA Implementation (Chat)                          | Implement Chat virtual assistant on Agent Studio                                                             |                         | Annette, Corbin, Michael                      | VA Design (Chat)                   |                                                                  |             |
| Chat — New Build  | VA to API Interface — CoE Design                  | CoE designs the VA-to-API interface layer                                                                    |                         | CoE, RD (architecture + scale signoff)        | VA Design (Chat)                   | Scale architecture review required — RD signoff                  |             |
| Chat — New Build  | Integration into CRC                              | Chat can launch into legacy CRC or new CRC — not a tech blocker                                              |                         |                                               | CRC Website (business preference) | Business preference: launch together with new CRC or separately? |             |
| Chat — New Build  | Integration into Home / PC                        | Multiple solutions interested; potentially faster go-to-market than CRC                                      |                         |                                               |                                   | Which solutions teams? Who drives this track?                    |             |
| Voice — Migration | Gemini for CX Voice — Migration from Dialogflow   | Upgrade existing voice channel from Dialogflow CX designer to Agent Studio; existing channel, not new build  |                         | Annette, Corbin, Michael                      | Amazon Connect retirement (TOPIC 4) | Dialogflow deprecation timeline from Google needed               |             |
| Voice — Migration | VA Design (Voice — Agent Studio Migration)        | Redesign existing voice VA for Agent Studio environment                                                       |                         | Annette, Corbin, Michael                      | Agent Studio available             |                                                                  |             |
| Voice — Migration | VA Implementation (Voice — Agent Studio Migration) | Migrate and reimplement voice VA in Agent Studio                                                              |                         | Annette, Corbin, Michael                      | VA Design (Voice)                  |                                                                  |             || Amazon Connect    | Migrate All Lines to GE CX                        | All lines off Amazon Connect onto GE CX                                                                      |                         |                                               |                                   | Timeline? Who owns migration?                                    |             |
| Tooling           | TW Authoring Tool                                 | Continue at pace; build against defined design specs                                                         |                         | Patrick                                       | TW design specs defined           | Confirm design specs are locked before Patrick proceeds          |             |
| Tooling           | TW Publishing Tool                                | Continue at pace; build against defined design specs                                                         |                         | Patrick                                       | TW design specs defined           |                                                                  |             |
| Tooling           | Hybrid UI Layer                                   | See Signal Processing — Hybrid UI for Support above                                                          |                         |                                               | Hybrid UI design                  |                                                                  |             |
