---
type: artifact
artifact_status: Active
topics:
  - '[[TPC - CE + IT - 3yr Execution Strategy Session]]'
  - '[[TPC - FY27 Containment Strategy]]'
created_date: 2026-05-01T00:00:00.000Z
---
# TOPIC 3 - CRC (Customer Resource Center)

> *Created: 2026-04-23T21:57:00.000Z*

# Topic Overview
The CRC (Customer Resource Center) is the primary self-service web destination for WellSky clients. This topic covers the consolidation, migration, and long-term evolution of the CRC as an AI-native resource layer.
This topic sits under Pillar 2 - GenAI Integration into CE Operations.
---
# Current State
- CRC is currently built on Salesforce and fragmented across multiple surfaces
- No unified AI layer for self-service resolution
---
# Phased Direction
## CRC v1.5 - Short Term (3 months)
- Consolidate existing Salesforce surfaces into a single, coherent CRC experience
- Clean up content structure to prepare for AI consumption
## CRC v2.0 - Long Term
- Evolve CRC into a combination of a structured knowledge layer and Chat (AI interaction layer)
- Relational Database serves as the structured content backend for documents, fed by the Markdown editor via the DPL/ETL process
- Chat provides the conversational interface for clients
- CRC v2.0 represents the AI-native, GenAI-first self-service model
---
# Key Notes by IT Group
---
# Decision Needed
- Confirm the CRC v1.5 timeline
- Agree on the CRC v2.0 north-star Architecture

---
# Google Next Pivots
> No direct GECX pivot for this topic. CRC v1.5 is a consolidation play on existing Salesforce infrastructure. CRC v2.0 Chat integration may be impacted - see Topic 3 (Chat Capability) for the GECX pivot that affects the Chat layer this topic depends on long-term.

# Risks
- Risk 1 - Salesforce Renewal Decision Horizon (Oct 2028)
- Risk 2 - IT Ownership Boundaries & RACI
- Risk 99 - Client Authentication
