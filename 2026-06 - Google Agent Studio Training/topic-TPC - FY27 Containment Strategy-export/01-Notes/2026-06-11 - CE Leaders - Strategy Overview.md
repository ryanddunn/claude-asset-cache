---
fileClass: note
type: note
created_date: 2026-06-11T00:00:00.000Z
notes_status: Reviewed
meta:
  - Written
  - Formal
topics:
  - '[[TPC - FY27 Containment Strategy]]'
entities: []
---

# FY27 GenAI & Knowledge Strategy — Slide Deck Outline
*Text outline for presentation to Support Leaders & Client Success Leaders*

---

## Slide 1 — Title Slide

**Title:** FY27 GenAI & Knowledge Strategy
**Subtitle:** Partnering with Support & Client Success
**Presenter:** Ryan Dunn
**Date:** [Meeting Date]

> *Speaker notes: Set the tone — this is a partnership briefing, not a one-way status update. We're here to show how this work connects to your world.*

---

## Slide 2 — Why We're Here (The Problem)

**Header:** The Challenge We're Solving Together

- WellSky's support volume is growing — manual workflows don't scale
- Customers frequently call in just to check the status of open cases — a problem that can be automated
- Knowledge exists across WellSky, but it's locked in legacy formats that can't power modern AI
- Our customers expect intelligent, modern support experiences

> *Speaker notes: Open with empathy for the room. Acknowledge what support teams face every day — don't lead with technology. Lead with the problem.*

---

## Slide 3 — Our Team's Role

**Header:** Who We Are & What We Own

- Our team sits at the intersection of GenAI product, knowledge infrastructure, and customer-facing support channels
- We own the GECX voice & chat channels, the technical writing platform, and the knowledge pipeline that feeds AI
- **FY27 goal: Containment** — reduce inbound support load through automation and better self-service, without sacrificing quality or customer experience

> *Speaker notes: Position this as "we're here to make your lives easier." This is not work being done to you — it's work being done for you.*

---

## Slide 4 — How It All Fits Together

**Header:** The Big Picture — Our Content & AI Architecture

```
TW Authors (Markdown Editor)
        ↓
  Markdown Files
        ↓
  Relational Database
  (metadata-enriched)
       ↙             ↘
Knowledge Graph DB    Legacy Build Pipeline
  (powers GenAI)      (PDFs, HTML on CRC)
       ↓                      ↓
GenAI Channels             Human Consumers
(Chat, Voice,              (Support Teams,
 First Responder)           Customers)
       ↓
  Customers & Support Teams
```

- Every work stream has a home in this architecture
- Infrastructure work (pipeline, graph DB) is what makes the AI work possible
- Better authoring → better knowledge → smarter AI → fewer support contacts

> *Speaker notes: Use this diagram as the anchor for the entire presentation. When people ask "why does the TW editor matter?" — point back here.*

---

## Slide 5 — Meet the Work Streams

**Header:** The FY27 Work Streams — Your Reference Guide

When someone on your team asks about our work, use these names:

| # | Work Stream | When You Hear... | Priority | Lead |
|---|-------------|-----------------|----------|------|
| WS-1 | Chat v1 (Agent Studio) | "How is Chat going?" | 1 | M. Proffer |
| WS-2 | Voice Update v2 (Agent Studio) | "What's happening with Voice?" | 4 | M. Proffer |
| WS-3 | First Responder Agent | "The auto-response bot" | 2 | J. Weinzerl |
| WS-4 | Knowledge Pipeline | "The data pipeline" | 6 | A. Dash |
| WS-5 | TW Markdown Editor | "The new authoring tool" | 5 | J. Nicol |
| WS-6 | Legacy TW Artifact Build | "PDFs / CRC publishing" | 7 | A. Dash |
| WS-7 | Graph DB Migration | "Moving voice/chat to graph DB" | 8 | V. Pissay |
| WS-8 | External Content Publishing | "Non-TW content contribution" | 10 | J. Nicol |
| WS-9 | Solutions Integration | "Chat inside the app" | 9 | R. Dunn |
| WS-10 | Amazon Connect Migration | "Phone line migration" | 3 | M. Proffer |

> *Speaker notes: This is your Rosetta Stone. When a support leader asks "how is chat going?" — that's WS-1. When Client Success asks "what are we doing with voice?" — that's WS-2. Please use these names when routing questions.*

---

## Slide 6 — Q1 Priorities: What Launches First

**Header:** Q1 FY27 — Immediate Impact (July–September 2026)

Three customer- and support-facing work streams launch in Q1:

**WS-1 — Chat v1 (Agent Studio)**
- Rebuilt customer chat experience powered by Agent Studio
- Deployed as an embedded widget on the Customer Resource Center (CRC)
- Integrates directly with Salesforce to read and write Case records
- *What it means for support:* Customers self-serve more effectively before opening a case; chat interactions create or update Cases automatically

**WS-3 — First Responder Agent**
- A backend GenAI agent — not customer-facing — integrated with your Salesforce case queue
- Automatically drafts responses to incoming support cases using the knowledge article base
- Designed to tackle the growing backlog of cases that human agents can't get to quickly
- *What it means for support:* Your team receives a ready-to-review draft on incoming cases, reducing effort and time-to-response

**WS-10 — Amazon Connect Migration**
- Consolidates all WellSky telephony endpoints onto the unified GECX voice platform
- Clean endpoint migration — no architectural change, no new capabilities required
- *What it means for support:* One platform, simpler operations, foundation for Voice v2

> *Speaker notes: These three have the most direct, near-term impact on support teams. If your leaders remember nothing else from this presentation, make sure they know WS-1, WS-3, and WS-10.*

---

## Slide 7 — Q1 Foundation: The Infrastructure Behind It All

**Header:** Q1 FY27 — The Work You Won't See (But That Powers Everything)

Also launching in Q1 and running into Q2:

**WS-4 — Knowledge Pipeline**
- Moves TW-authored content through a relational database into a knowledge graph database
- The graph DB becomes the authoritative, structured knowledge source for all GenAI models
- Replaces the current fragile process of JSON blobs stored in GCP buckets
- *Why it matters:* AI is only as smart as its knowledge. This is how we make responses accurate, current, and reliable

**WS-5 — TW Markdown Editor**
- Replaces MadCap Flare as the primary authoring tool for the Technical Writing team
- Output: structured Markdown enriched with metadata for information architecture and data taxonomy
- Integrates existing TW agents (GitHub release notes, JIRA work items) to speed content production
- *Why it matters:* Faster, higher-quality knowledge production upstream means smarter AI downstream — everything flows from here

> *Speaker notes: Neither of these work streams will be directly visible to support or client success teams. But without them, WS-3 and WS-7 don't work. Think of these as the engine — no one sees the engine, but everyone relies on it.*

---

## Slide 8 — Q2 Milestones

**Header:** Q2 FY27 — Completing the Architecture (October–December 2026)

**WS-2 — Voice Update v2 (Agent Studio)**
- Upgrades the GECX voice channel from legacy Dialogflow to Agent Studio
- Adds customer interrupt capability — a more natural, conversational IVR experience
- Potential: A unified voice + chat design under a single Agent Studio model
- *Impact:* Modernized voice experience, higher customer satisfaction, better containment

**WS-6 — Legacy TW Artifact Build**
- Formalizes the pipeline from the new relational database to published documentation deliverables
- Outputs include PDFs (Release Notes, User Guides, Knowledge Articles) and HTML content on CRC
- Format parity with today's deliverables — apples to apples
- *Impact:* TW publishing moves off a legacy process without disrupting downstream consumers

**WS-7 — Graph DB Migration (Voice + Chat)**
- Migrates both the voice and chat channels from JSON/GCP buckets to the graph database
- Both channels gain a richer, structured, and continuously-updated knowledge foundation
- *Impact:* AI responses become significantly more reliable; the full architecture is complete

> *Speaker notes: By end of Q2, the full architecture is live. Q3 is about extending what we've built into the solutions themselves.*

---

## Slide 9 — Q3 Milestones

**Header:** Q3 FY27 — Extending the Platform (January–March 2027)

**WS-9 — Solutions Integration (Chat + Voice)**
- Creates solution-specific API integrations for the GenAI chat and voice channels
- Customers will be able to take direct actions via GenAI chat prompts (e.g., check case status, retrieve account information)
- Chat widget deployed *inside* WellSky solution applications — not just on CRC
- Priority candidates: **Home Health** (highest impact), Connected Networks, Personal Care
- *Impact:* Customers resolve issues without ever calling support — the most powerful containment lever in the portfolio

**WS-8 — External Content Publishing Process**
- A formal, governed process allowing non-TW staff (e.g., solution teams, subject matter experts) to contribute content to the knowledge graph
- Includes submission workflows, review gates, and integration into the TW Markdown publishing pipeline
- *Impact:* Domain expertise from across WellSky flows into the AI knowledge base; GenAI gets smarter faster

> *Speaker notes: WS-9 is the headline for Q3. In-app AI that lets customers check case status or take actions — before they ever pick up the phone — is the ultimate containment outcome.*

---

## Slide 10 — FY27 Timeline at a Glance

**Header:** When to Expect What

```
Q1 FY27 (Jul–Sep)      Q2 FY27 (Oct–Dec)      Q3 FY27 (Jan–Mar)
────────────────────────────────────────────────────────────────
WS-1  Chat v1          ▓▓▓▓▓▓▓▓
WS-3  First Responder  ▓▓▓▓▓▓▓▓
WS-10 Amazon Connect   ▓▓▓▓▓▓▓▓
WS-4  Knowledge Pipeline ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓
WS-5  TW Editor        ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓
                              WS-2  Voice v2  ▓▓▓▓▓▓▓▓
                              WS-6  Legacy    ▓▓▓▓▓▓▓▓
                              WS-7  Graph DB  ▓▓▓▓▓▓▓▓
                                              WS-9  Solutions ▓▓▓▓▓▓▓▓
                                              WS-8  Ext Content ▓▓▓▓▓▓▓▓
```

- **Q1:** Customer-facing channels + foundation infrastructure
- **Q2:** Architecture completion + voice modernization
- **Q3:** In-app integration + knowledge contribution at scale

> *Speaker notes: The sequencing is intentional — we can't build in-app chat (WS-9) until the chat channel is solid (WS-1) and the knowledge graph is live (WS-7). Everything builds on what comes before it.*

---

## Slide 11 — What This Means for Support Leaders

**Header:** The Impact on Your Teams

By end of FY27, here's what changes for support:

| What's Changing | What You'll See |
|----------------|----------------|
| Chat v1 on CRC | Customers self-serve before opening cases; Salesforce Cases created automatically |
| First Responder Agent | Auto-drafted responses on incoming cases; team focuses on review + complex issues |
| Amazon Connect Migration | Single voice platform; no more dual-system operations |
| Voice v2 | More natural IVR; customer interrupt capability; higher containment rate |
| Solutions Integration (Q3) | In-app AI deflects contacts before customers reach the phone or chat queue |
| Richer knowledge graph | AI responses more accurate; fewer escalations caused by AI errors |

**The bottom line:** Your teams handle fewer routine contacts, arrive at responses faster, and operate on a single unified modern platform — by the end of FY27.

> *Speaker notes: If you have current baseline metrics — average case volume, handle time, top contact reasons — reference them here. The more specific you can be, the more credible the promise.*

---

## Slide 12 — What This Means for Client Success Leaders

**Header:** How to Carry This Message to Your Clients

Client Success leaders don't manage these tools — but they manage the relationship. Here's how this work connects to your role:

**What WellSky is doing:**
- Investing significantly in GenAI-powered support infrastructure for FY27
- Rebuilding voice and chat on a modern AI platform (Google Agent Studio)
- Building a knowledge graph to make AI responses accurate, current, and trustworthy
- Delivering in-app AI capabilities inside solutions (starting with Home Health) in Q3

**What you can tell clients:**
- *"WellSky is not just maintaining support — we are reinventing it."*
- *"The tools are getting smarter throughout the year — the experience will keep improving."*
- *"Coming in Q3, you'll be able to get case updates and answers directly inside the application."*

**Your advocacy role:**
- Encourage clients to engage with CRC chat when it launches — early adoption data matters
- Set realistic expectations: capabilities roll out Q1 → Q2 → Q3; it builds progressively
- Surface client concerns or confusion back to Ryan's team — those are knowledge gaps we can address

> *Speaker notes: Client Success is a force multiplier. If clients trust and adopt the tools, support volume drops further. CS leaders help us get there by being informed, confident advocates — not just reactive responders.*

---

## Slide 13 — How We Work Together

**Header:** Our Partnership Model

**Language alignment:**
- Use WS names (WS-1 through WS-10) when asking for updates — it keeps everyone aligned
- "How is Chat going?" = WS-1. "What's the status on Amazon Connect?" = WS-10.

**Feedback loops (this is critical):**
- **Support leaders:** Flag recurring case types that AI should be handling — these are knowledge gaps to fill
- **Client Success:** Surface client objections, confusion, or "I didn't know you could do that" moments — they reveal where to prioritize content
- **Both audiences:** We will invite participation in UAT for chat and voice before launch. Your input shapes the final product.

**Recommended cadence:**
- Monthly briefing with support leader leads
- Quarterly checkpoint with Client Success leadership
- Ad-hoc escalation path: [define]

**Key contacts by work stream:**
- Chat & Voice (WS-1, WS-2, WS-10): Michael Proffer
- First Responder Agent (WS-3): Jared Weinzerl
- Knowledge & Data Pipeline (WS-4, WS-6, WS-7): Abhirup Dash
- TW Platform & Content Ops (WS-5, WS-8): Jason Nicol
- Solutions Integration (WS-9): Ryan Dunn

> *Speaker notes: The feedback loop matters as much as the capability slides. Make the ask explicit — we need their observations to make the AI smarter and the work relevant.*

---

## Slide 14 — What Success Looks Like

**Header:** FY27 Goals — How We'll Know It's Working

**For Support Teams:**
- Measurable reduction in routine case contacts (deflection rate vs. FY26 baseline)
- First Responder Agent autonomously handling a defined percentage of incoming cases
- Amazon Connect fully migrated — zero dual-platform operations by end of Q1
- Support teams report improved accuracy in AI-generated responses (fewer escalations)

**For Client Success:**
- CS leaders can confidently articulate WellSky's GenAI roadmap to clients
- Reduction in client-initiated "what are you doing with AI?" escalations
- Measurable client adoption of CRC chat channel (Q1–Q2)
- At least two client advocates identified for early in-app chat (Q3)

**For the Platform:**
- All 10 work streams on track or completed by end of Q3 FY27
- Knowledge graph live and serving both voice and chat channels
- External content publishing process operational with active contributors

> *Speaker notes: Return to this slide at your next briefing. It's the accountability anchor for both audiences. If you can share numbers at that point — even early ones — it builds credibility and momentum.*

---

## Slide 15 — Next Steps & Questions

**Header:** Let's Talk — What We Need From You

**Today's ask — three things:**

1. **Align on language:** Agree that your teams will use WS names when referencing our work
2. **Identify your feedback lead:** Who on your team routes recurring case patterns or client concerns back to us?
3. **Client Success specific:** Identify 2–3 clients who are good candidates to be early CRC chat advocates at launch

**What happens next:**
- [Date TBD]: Chat v1 UAT begins — support leader participation requested
- [Date TBD]: Amazon Connect migration kickoff — scope review with affected teams
- [Date TBD]: Next all-up briefing checkpoint (recommend end of Q1)

---

*Questions, ideas, or concerns: reach Ryan Dunn at [contact / shared Slack channel]*

**Thank you.**

---

*Source: [[2026-06-02 - Work streams]]*
*Topic: [[TPC - FY27 Containment Strategy]]*
