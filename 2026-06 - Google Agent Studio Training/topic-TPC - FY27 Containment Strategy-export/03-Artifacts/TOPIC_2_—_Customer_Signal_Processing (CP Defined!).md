---
type: artifact
artifact_status: Active
topics:
  - '[[TPC - CE + IT - 3yr Execution Strategy Session]]'
  - '[[TPC - FY27 Containment Strategy]]'
created_date: 2026-05-01T00:00:00.000Z
---
# TOPIC 2 - Customer Signal Processing

> *Created: 2026-04-23T21:57:00.000Z*


![[Pasted image 20260518203357.png]]

# Topic Overview
Customer Signal Processing is CE's AI-powered pipeline that ingests raw support data - cases, transcripts, call trends - and transforms it into clean, structured, actionable work items for downstream engineering and product teams. It closes the loop between client-facing operations and the WellSky product and engineering backlog.
This topic sits under Pillar 1 - Enterprise Knowledge Data Architecture.
---
# What This Is
CE as a signal producer, not just a data consumer.
- CE operates at the highest volume of client interaction in WellSky
- That interaction generates a continuous stream of signals: bugs, friction points, feature gaps, recurring issues
- Today those signals are lost in case queues or surfaced inconsistently through manual escalation
- This initiative uses AI to systematically extract, classify, and deliver those signals as structured outputs
Example flow:
> Client calls about a recurring login issue â†’ CCAI captures transcript â†’ AI identifies pattern across 50+ similar cases â†’ CE produces structured bug report â†’ delivered to Solutions (ENG + Product) backlog
---
# Signal Sources
- CCAI call transcripts
- Salesforce support cases
- New Relic application telemetry
- Case trend data (volume, category, resolution time)
- Chat transcripts (future, as Chat v1.5 launches)
---
# Output Types
- Structured bug reports
- Feature gap summaries
- Automated Identification and communication regarding service degradation
- Trend reports (volume spikes, emerging issue categories)
- Backlog-ready work items formatted for Solutions team intake
---
# Dual Purpose of This Agenda Topic
This topic serves two simultaneous goals:
1. Inform Engineering Overall of CE's signal processing intent so they can guide the connection to Solutions teams - process, relationships, and leadership access
1. Align on data shape and delivery mechanism so when CE engages Solutions directly, the conversation is already grounded in agreed architecture
> Engineering Overall is CE's internal sponsor and navigator into the Solutions relationship - not a decision-maker on this topic itself. CE has not previously worked directly with Solutions teams; Engineering Overall is the bridge to Solutions leadership.
---
# Key Notes by IT Group
---
# Flagged Risks
- IT ownership boundary: GenAI CoE has explicitly flagged that IT will not serve as system admins for business-owned signal data. 
- Data governance: Service account management, permissioning, and audit trails for automated data extraction must be designed upfront.
- Impact of Salesforceâ€™s contract expiration could change underlying data. 
---
# Decision Needed
- This is currently be worked on, with recurring meetings with Vivek, Jolinda, and Joe Baker. 
- The correct intake format for Solutions teams (bugs, features, any other signal processing)
- A proposed timeline for a CE â†’ Solutions alignment session

---
# 
