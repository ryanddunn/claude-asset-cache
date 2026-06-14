---
type: artifact
artifact_status: Active
topics:
  - '[[TPC - CE + IT - 3yr Execution Strategy Session]]'
  - '[[TPC - FY27 Containment Strategy]]'
created_date: 2026-05-01T00:00:00.000Z
---
# TOPIC 5 - Chat Capability

> *Created: 2026-04-23T21:57:00.000Z*

# Topic Overview
This topic covers the scoping and design of GenAI-driven client-facing interaction channels within CE. There are two distinct workstreams under this topic: Chat (new build) and Voice (migration/upgrade). These are tracked separately because they differ in channel type, build approach, and current state.
This topic sits under Pillar 2 - GenAI Integration into CE Operations.
---
# Workstream 1 — Gemini for CX Chat (New Build)
## Current State
- No Chat capability exists today in CE's client-facing stack
- Chat scoping is actively in progress — Gemini for CX chat is being scoped inside Agent Studio technology
- This is a new channel being built on Agent Studio from the start — not a migration

## Phased Direction
### Chat v1.5 - Initial Scope (tied to CRC v1.5)
- Launch Chat on CRC surface via Agent Studio
- Launch Chat in-app for Personal Care (PC)
- Core functions: authentication (Auth), API integration, basic case interaction
### Chat v2.0 - Workflow Automation
- API write-back integrations between GenAI agents and Salesforce
- Case state interactions: status queries, customer follow-up, workflow triggers
- Agent action on workflow inside Salesforce
- Full Salesforce integration and session management
---
# Workstream 2 — Gemini for CX Voice (Migration / Upgrade)
## Current State
- Voice channel currently runs on Dialogflow CX designer
- Planning to upgrade the existing voice channel from Dialogflow to Agent Studio
- This is a migration and upgrade of an existing channel — not a new build

## Direction
- Migrate existing Dialogflow-based voice channel to Agent Studio
- Agent Studio replaces the Dialogflow CX designer as the virtual agent authoring environment
- The CCAI platform infrastructure remains intact — only the virtual agent designer tool is changing
- Migration must be coordinated with the Amazon Connect retirement workstream (TOPIC 4)
---
# Core Functional Requirements — Chat Workstream (to define in session)
- Auth: SSO, identity, and user session management for the chat surface
- API access: Read and write access to Salesforce case data
- Key flows: Case submission, status lookup, knowledge retrieval, escalation
- Channel surfaces: CRC, In-App (PC), future: additional BU surfaces
---
# Key Notes by IT Group
---
# Decisions Needed
- Chat: Confirm launch timeline for v1.5 and v2.0 on Agent Studio
- Voice: Confirm migration timeline from Dialogflow to Agent Studio; align with Amazon Connect retirement track
---
# Google Next Pivot — Agent Studio / GECX (Critical)
This topic has two distinct workstreams, each differently impacted by the Agent Studio (GECX) transition announced at Google Next.

**Impact on Chat (new build):**
- New Chat capability must be built on Agent Studio (GECX) — not the deprecated Dialogflow CX designer
- Chat scoping on Gemini for CX inside Agent Studio is actively in progress
- Build timeline is gated on Agent Studio availability confirmation
- This creates a deliberate sequencing dependency: scope now, build when Agent Studio is ready

**Impact on Voice (migration/upgrade):**
- Existing voice channel runs on Dialogflow CX designer and must be migrated to Agent Studio
- This is an upgrade of an existing channel — not a net-new build
- The CCAI platform itself remains intact — only the virtual agent designer tool is changing
- Migration timeline depends on Google's Dialogflow deprecation schedule

GenAI CoE should be prepared to present what is known about Agent Studio availability and the Dialogflow deprecation timeline for both workstreams.

# Risks
- Client Authentication
- Google - Dialogflow Deprecation & Google Product Evolution
- Security - GenAI Chat Hardening
