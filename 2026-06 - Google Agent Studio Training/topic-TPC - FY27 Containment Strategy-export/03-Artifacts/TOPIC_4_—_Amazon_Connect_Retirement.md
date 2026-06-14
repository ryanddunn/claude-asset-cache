---
type: artifact
artifact_status: Active
topics:
  - '[[TPC - CE + IT - 3yr Execution Strategy Session]]'
  - '[[TPC - FY27 Containment Strategy]]'
created_date: 2026-05-01T00:00:00.000Z
---
# TOPIC 4 - Amazon Connect Retirement

> *Created: 2026-04-23T21:57:00.000Z*

# Topic Overview
WellSky currently operates telephony across two platforms: Google CCAI (actively deployed) and Amazon Connect (legacy, still active for certain lines of business). This topic establishes the business case, scope, and execution path for retiring Amazon Connect and fully consolidating on Google CCAI.
This topic sits under Pillar 2 - GenAI Integration into CE Operations.
---
# Current State
- Google CCAI is live in production across initial BUs
- Amazon Connect remains active for other lines of business - exact scope TBD
- Salesforce contract includes embedded Amazon Connect licensing ($1.29M committed spend over contract term)
- AWS dependency is contractually embedded inside Salesforce Voice
- Per-minute usage charges accrue on top of fixed licensing
---
# Financial Exposure (Salesforce Contract)
- Fixed Amazon Connect licensing over contract term: ~$1.29M
- Additional per-minute usage charges (billed monthly in arrears)
- Retirement eliminates: fixed subscription, usage exposure, and separate AWS indemnification risk
---
# Strategic Case for Retirement
- Removes duplicative telephony layer vs. Google CCAI
- Eliminates AWS dependency inside Salesforce
- Simplifies architecture and reduces operational surface area
- Aligns all voice infrastructure under a single GenAI-native platform
- Creates leverage at the 2028 Salesforce renewal
---
# Key Notes by IT Group

---
# Decision Needed
- Confirm target completion of 10/1/26
- Confirm Mollyâ€™s involvement
---
# Google Next Pivots
âš ï¸ Important GECX Context: At Google Next, intel from a Google confirmed that the Dialogflow CX designer tool is being deprecated and replaced by GECX (Gemini ENT for Customer Experience). Key implications for this topic:
- The Amazon Connect migration must continue on legacy Dialogflow CX due to current contract constraints - this path is not changing
-  The CCAI platform itself is not being deprecated - only the virtual agent designer tool is changing
- No official deprecation timeline was confirmed by Google
- New virtual agent builds should plan for GECX when it becomes available
- This does not block the Amazon Connect retirement - it informs the tooling strategy for what replaces it

# Risks
- Low, we have already done this before
