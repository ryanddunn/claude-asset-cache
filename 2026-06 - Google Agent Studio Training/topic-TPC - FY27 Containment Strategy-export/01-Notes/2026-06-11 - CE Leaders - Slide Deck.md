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

# FY27 GenAI & Knowledge Strategy
## Draft Slide Content

*Full text draft for each slide — headings, subheadings, bullets, and speaker notes.*
*Source: [[2026-06-02 - Work streams]] · [[TPC - FY27 Containment Strategy]]*

---

---

# SLIDE 1

## FY27 GenAI & Knowledge Strategy

### Partnering for a Smarter Support Experience

Ryan Dunn · VP, [Title]
[Meeting Date] · [Location / Virtual]

---

*Speaker notes: Welcome the room. Acknowledge both audiences — support leaders and client success leaders. Frame the session as a partnership briefing: this is about how our team's work connects to theirs, not a technology demo.*

---

---

# SLIDE 2

## The Problem We're Solving Together

### Our customers and our teams deserve better than the status quo

- Support case volume is growing — manual processes can't keep up
- Customers call in just to check the status of an existing case — a routine task that shouldn't require a human
- Valuable knowledge exists across WellSky, but it's trapped in legacy formats that AI can't read or use
- Our competitors are investing in AI-powered support — our customers will expect the same from us

==RD FEEDBACK - WE LAUNCHED GECX (GOOGLE CONTACT CENTER AI) AND IT WENT WELL. WE ARE AT ~20% SUPPORT CONTAINMENT, THIS IS OUR PATH TO 50% CONTAINMENT. THE CONTEXT NEEDS TO REFLECT THAT WE HAVE A GENAI SOLUTION IN PLACE NOW AND THIS PLAN TO MAKE OUR GENAI MORE EFFECTIVE IN THE CLIENT EXPERIENCE SPACE. DON'T OVER INDEX ON THAT POINT, BUT THE CONTEXT IS THE POITNT. 
### The opportunity is real

> *If we can answer a customer's question before they pick up the phone, that's a win for them, for support, and for WellSky.*

---

*Speaker notes: Lead with the problem, not the technology. Make the room feel seen — acknowledge what support teams deal with every day. The case status call example is relatable and concrete. Use it.*

---

---

# SLIDE 3

## Who We Are & What We Own

### Ryan Dunn's team: GenAI, Knowledge, and Customer Channels

**We own three interconnected areas:**

- **GECX Voice & Chat** — the AI-powered channels customers use to reach support
- **Technical Writing Platform** — how WellSky knowledge gets created and structured
- **Knowledge Pipeline** — how that content flows into AI models

### Our FY27 mission: Containment

> Reduce inbound support load through automation and better self-service — without sacrificing quality or the customer relationship.

**What containment means in practice:**
- Customers find answers before they open a case
- Open cases get faster, more accurate responses
- Support teams spend time on complex work — not routine follow-ups

==RD FEEDBACK - OUR GOAL IS TO GO FROM ~20% CONTAINMENT TO 50% CONTAINMENT, 

---

*Speaker notes: Define "containment" clearly — it is a deliberate term. It does not mean reducing headcount. It means redirecting effort to where humans add the most value.*

---

---

# SLIDE 4

## How It All Fits Together

### One connected pipeline — from authoring to the customer

**The architecture in plain language:**

1. **Technical writers author content** using a new Markdown-based editor
2. **Content flows into a relational database** — enriched with metadata and structure
3. **Two outputs branch from there:**
   - A **knowledge graph database** that powers all GenAI models (voice, chat, auto-response)
   - A **legacy build pipeline** that produces PDFs, Release Notes, User Guides, and HTML on CRC
4. **GenAI channels** (chat, voice, First Responder Agent) draw from the knowledge graph to serve customers and support teams
5. **Customers and support teams** receive faster, more accurate answers

### Why this matters
- Every work stream we'll discuss today has a home in this pipeline
- The infrastructure work makes the AI work possible — they are not separate efforts
- Better authoring → better knowledge → smarter AI → fewer support contacts

---

*Speaker notes: Use this as the anchor diagram for the whole presentation. Return to it whenever a work stream needs context. The key message: nothing is random — everything connects.*

---

---

# SLIDE 5

## The FY27 Work Streams

### Ten projects. One strategy. One shared language.

*When your team asks about our work, use these names.*

| # | Name | What It Is | Priority |
|---|------|-----------|----------|
| **WS-1** | Chat v1 (Agent Studio) | Rebuilt customer chat on CRC, integrated with Salesforce | 1 |
| **WS-2** | Voice Update v2 (Agent Studio) | Upgraded GECX voice — more natural, interruptible | 4 |
| **WS-3** | First Responder Agent | AI that auto-drafts responses to Salesforce support cases | 2 |
| **WS-4** | Knowledge Pipeline | Moves TW content from Markdown → relational DB → graph DB | 6 |
| **WS-5** | TW Markdown Editor | Replaces MadCap Flare; structured authoring with AI integration | 5 |
| **WS-6** | Legacy TW Artifact Build | PDFs, Release Notes, User Guides, CRC — published from the new pipeline | 7 |
| **WS-7** | Graph DB Migration | Moves voice + chat off JSON/GCP buckets onto the knowledge graph | 8 |
| **WS-8** | External Content Publishing | Governed process for non-TW teams to contribute knowledge | 10 |
| **WS-9** | Solutions Integration | AI chat embedded inside WellSky applications | 9 |
| **WS-10** | Amazon Connect Migration | All phone lines consolidated onto GECX voice | 3 |

---

*Speaker notes: This table is intentional. Keep it up for a moment. Ask the room: "When someone on your team says 'how is chat going?' — now you know that's WS-1." Help them build the habit of using these names. It will save everyone time throughout the year.*

---

---

# SLIDE 6

## Q1 FY27 — What Launches First

### July – September 2026 · Three work streams with direct impact on support

---

### WS-1 · Chat v1 (Agent Studio)

**What it is:** A fully rebuilt customer chat experience embedded on the Customer Resource Center

**Key details:**
- Powered by Google Agent Studio — modern, AI-native platform
- Reads and writes Salesforce Case records via API integration
- Customers can initiate or follow up on cases directly through chat

**What it means for support:** Fewer calls for routine questions; Salesforce Cases created and updated automatically through the conversation

---

### WS-3 · First Responder Agent

**What it is:** A backend GenAI agent that auto-drafts responses to incoming Salesforce support cases

**Key details:**
- Not customer-facing — operates inside the case queue
- Draws on the existing knowledge article base to generate a draft response
- Designed to address the backlog of cases the team cannot respond to quickly

**What it means for support:** Every incoming case arrives with a ready-to-review draft — your team edits and sends instead of starting from scratch

---

### WS-10 · Amazon Connect Migration

**What it is:** Migration of all WellSky telephony endpoints from Amazon Connect to the unified GECX voice platform

**Key details:**
- Clean endpoint migration — no architectural change required
- Consolidates all public phone lines onto one platform
- Foundation for Voice v2 (WS-2) later in the year

**What it means for support:** One platform to manage, one place to route calls, simpler operations

---

*Speaker notes: These three are the most tangible for support leaders in the near term. If you have to prioritize what the room takes home from Q1, it's these three — especially the First Responder Agent.*

---

---

# SLIDE 7

## Q1 FY27 — The Foundation

### July – September 2026 · The infrastructure that makes everything else possible

---

### WS-4 · Knowledge Pipeline

**What it is:** An end-to-end data pipeline moving TW-authored content from Markdown files through a relational database into a graph database

**Key details:**
- The graph database becomes the authoritative knowledge source for all GenAI models
- Replaces the current fragile process: JSON blobs stored in GCP buckets
- Feeds the knowledge base for WS-3 (First Responder), WS-7 (Graph DB Migration), and future AI work

**Why it matters:** AI is only as good as its knowledge. This is how we make responses reliable, current, and accurate — not just fast.

---

### WS-5 · TW Markdown Editor

**What it is:** A replacement for MadCap Flare as the primary authoring tool for the Technical Writing team

**Key details:**
- Output: structured Markdown files enriched with metadata for information architecture and data taxonomy
- Integrated with existing TW agents — GitHub release notes, JIRA work items — to auto-draft content
- Preserves TW team workflows while dramatically improving output quality and speed

**Why it matters:** The knowledge pipeline (WS-4) is only as good as what flows into it. WS-5 is the upstream source — better authoring means smarter AI downstream.

---

> *You won't see WS-4 or WS-5 directly. But without them, WS-3 doesn't draft accurately, and WS-7 doesn't have reliable knowledge to migrate. They are the engine.*

---

*Speaker notes: Expect questions like "why does the authoring tool matter to us?" Use the engine analogy — nobody sees it, but everyone depends on it running well.*

---

---

# SLIDE 8

## Q2 FY27 — Completing the Architecture

### October – December 2026 · The platform comes together

---

### WS-2 · Voice Update v2 (Agent Studio)

**What it is:** An upgrade of the GECX voice channel from legacy Dialogflow to Agent Studio

**Key details:**
- Delivers a more natural, conversational IVR experience
- Adds **customer interrupt capability** — customers can redirect the conversation mid-flow
- Google has indicated Agent Studio can support a single unified design for both voice and chat

**What it means:** The voice experience customers have used for years gets a significant upgrade — more intelligent, more responsive, higher satisfaction

---

### WS-6 · Legacy TW Artifact Build

**What it is:** A formalized pipeline from the relational database to published documentation deliverables

**Key details:**
- Outputs: Release Notes (PDF), User Guides (PDF), Knowledge Articles, CRC HTML content
- Format parity with today's deliverables — apples to apples for downstream consumers
- Replaces the legacy MadCap Flare-based publishing process

**What it means:** TW modernizes its publishing process without disrupting the documentation formats that support teams and customers rely on

---

### WS-7 · Voice + Chat — Graph DB Migration

**What it is:** Migration of the knowledge source for both voice and chat from JSON files in GCP buckets to the knowledge graph database

**Key details:**
- Both channels gain a richer, structured, continuously updated knowledge foundation
- Decommissions the current fragile JSON extract process
- Connects WS-1 (Chat) and WS-2 (Voice) to the graph DB as their authoritative source

**What it means:** By end of Q2, every AI-powered customer interaction draws from a reliable, well-maintained knowledge graph — not static JSON files

---

*Speaker notes: By the end of Q2, the full architecture is live. Every layer — authoring, pipeline, graph DB, voice, chat — is in place. Q3 is about extending the reach of what we've built.*

---

---

# SLIDE 9

## Q3 FY27 — Extending the Platform

### January – March 2027 · AI inside the application

---

### WS-9 · Solutions Integration (Chat + Voice)

**What it is:** Solution-specific API integrations that allow customers to take actions through the GenAI chat and voice channels

**Key details:**
- Solutions expose API endpoints; customers interact with them via natural language in chat or voice
- The chat widget is deployed *inside* WellSky applications — not just on CRC
- **Priority solutions:** Home Health (highest impact), Connected Networks, Personal Care

**Example:** A customer asks in chat: *"What's the status of my open case?"* — the AI queries Salesforce via API and responds instantly, without a support agent involved

**What it means for support:** Customers resolve routine requests inside the application before they ever reach the phone or case queue — the most powerful containment outcome in the entire strategy

---

### WS-8 · External Content Publishing Process

**What it is:** A formal, governed process for non-TW teams to contribute content to the knowledge graph

**Key details:**
- Includes submission workflows, review and approval gates, and integration into the TW Markdown publishing pipeline
- Enables solution teams and subject matter experts to contribute domain-specific knowledge
- Content flows through the same quality controls as TW-authored content

**What it means:** The AI knowledge base grows faster and gets smarter because the people closest to each solution can contribute what they know

---

*Speaker notes: WS-9 is the headline for Q3. If a client asks "what's the most exciting thing coming this year?" — this is the answer. In-app AI that handles case status, account questions, and common actions without a human in the loop.*

---

---

# SLIDE 10

## FY27 Timeline

### What launches when — the full picture

| Work Stream | Q1 (Jul–Sep) | Q2 (Oct–Dec) | Q3 (Jan–Mar) |
|-------------|:------------:|:------------:|:------------:|
| WS-1 · Chat v1 | ████ | | |
| WS-3 · First Responder Agent | ████ | | |
| WS-10 · Amazon Connect Migration | ████ | | |
| WS-4 · Knowledge Pipeline | ████ | ████ | |
| WS-5 · TW Markdown Editor | ████ | ████ | |
| WS-2 · Voice Update v2 | | ████ | |
| WS-6 · Legacy TW Artifact Build | | ████ | |
| WS-7 · Graph DB Migration | | ████ | |
| WS-9 · Solutions Integration | | | ████ |
| WS-8 · External Content Publishing | | | ████ |

**Q1** — Customer-facing channels + foundational infrastructure
**Q2** — Architecture completion + voice modernization
**Q3** — In-app AI integration + knowledge contribution at scale

> *The sequencing is intentional. Each quarter builds on the last.*

---

*Speaker notes: Point out the dependency logic — WS-9 (in-app chat) can't ship until WS-1 (chat) is stable and WS-7 (graph DB) is live. The sequencing is not arbitrary; it's architectural.*

---

---

# SLIDE 11

## What This Means for Support Leaders

### The FY27 impact on your teams — specifically

| Work Stream | Change | What Your Team Experiences |
|-------------|--------|---------------------------|
| WS-1 · Chat v1 | CRC chat rebuilt on Agent Studio | Customers self-serve routine questions; fewer inbound contacts for common issues |
| WS-3 · First Responder | AI drafts case responses automatically | Team reviews and sends drafts instead of writing from scratch; backlog addressed faster |
| WS-10 · Amazon Connect | All phone lines on GECX | Single platform; simplified routing; no dual-system management |
| WS-2 · Voice v2 | Upgraded IVR experience | Higher containment on voice; more customers resolved before reaching an agent |
| WS-7 · Graph DB | Richer AI knowledge source | AI responses more accurate; fewer escalations caused by outdated or incomplete answers |
| WS-9 · Solutions Integration | AI inside the application | Customers resolve issues in-app before they call or chat — highest-volume deflection |

### The bottom line

Your teams handle fewer routine contacts.
Agents spend their time on complex, high-value work.
The platform is unified, modern, and continuously improving.

---

*Speaker notes: If you have baseline metrics — current case volume, average handle time, top contact reasons — name them here. The more specific the before/after, the more credible this commitment feels to the room.*

---

---

# SLIDE 12

## What This Means for Client Success Leaders

### Your role: informed advocate, not technical expert

---

### What WellSky is doing — in terms you can share

- Rebuilding voice and chat on a modern AI platform (Google Agent Studio) — not just patching what exists
- Building a structured knowledge graph so AI responses are accurate, current, and trustworthy
- Investing in in-app AI capabilities so customers can get answers and take action inside WellSky solutions
- Creating a governed process so domain knowledge from across WellSky flows into AI — keeping it relevant

---

### What you can say to clients

> *"WellSky is not just maintaining support — we're reinventing it."*

> *"The experience will keep getting better throughout FY27. What launches in Q1 is the beginning, not the finished product."*

> *"By Q3, you'll be able to get answers and take action directly inside the application — without calling support."*

---

### Your advocacy role

- **Encourage clients** to use CRC chat when it launches — early adoption data helps us improve it faster
- **Set expectations** that capabilities roll out across Q1, Q2, and Q3 — it builds progressively
- **Surface friction** — if clients push back or are confused, tell us. Those are knowledge gaps we need to close.
- **Be a bridge** — clients who understand and trust the tools reduce support friction for everyone

---

*Speaker notes: CS leaders don't need to know how a graph database works. They need three things: what we're doing, why it matters to clients, and what to say when a client asks. This slide gives them all three.*

---

---

# SLIDE 13

## How We Work Together

### A partnership model for FY27

---

### Use the work stream names

When your team has a question about our work, use the WS number and name.

- *"How is Chat going?"* → **WS-1**
- *"When does Voice update?"* → **WS-2**
- *"What's the status on Amazon Connect?"* → **WS-10**

This keeps communication fast, unambiguous, and easy to route.

---

### How we need your feedback

| Audience | What to Send Us | Why It Matters |
|----------|----------------|----------------|
| Support Leaders | Recurring case types AI should be handling | These are knowledge gaps — we prioritize content to address them |
| Support Leaders | Pain points in the new tools as they launch | UAT input shapes the final product before it reaches customers |
| Client Success | Client objections or confusion about AI | Tells us where messaging and content need work |
| Client Success | Clients ready to be early adopters | Early data helps us prove value and improve faster |

---

### Key contacts

| Work Stream | Owner |
|-------------|-------|
| WS-1, WS-2, WS-10 · Chat, Voice, Amazon Connect | Michael Proffer |
| WS-3 · First Responder Agent | Jared Weinzerl |
| WS-4, WS-6, WS-7 · Knowledge Pipeline & Graph DB | Abhirup Dash |
| WS-5, WS-8 · TW Editor & Content Publishing | Jason Nicol |
| WS-9 · Solutions Integration | Ryan Dunn |

---

*Speaker notes: Make the feedback loop ask explicit and specific. "If you see a recurring case type that AI should handle, send it to Jared" is more actionable than "let us know your feedback."*

---

---

# SLIDE 14

## What Success Looks Like

### How we'll know FY27 is working — by the numbers

---

### For Support Teams

- Measurable reduction in routine inbound case contacts compared to FY26 baseline
- First Responder Agent handling a meaningful percentage of incoming cases autonomously by end of Q2
- Amazon Connect fully decommissioned — zero dual-platform operations by end of Q1
- Support teams report improved accuracy and reliability in AI-generated draft responses

---

### For Client Success

- CS leaders can answer *"what is WellSky doing with AI?"* with confidence
- Reduction in escalations driven by client uncertainty about WellSky's AI direction
- Measurable CRC chat adoption by clients in Q1–Q2
- At least two client advocates identified and engaged for in-app AI pilot in Q3

---

### For the Platform

- All 10 work streams delivered on schedule or with communicated adjustments by end of Q3
- Knowledge graph live and serving both voice and chat by end of Q2
- External content publishing process operational with active contributors from solution teams

---

> *We will bring these metrics back to this group at the end of Q1. Hold us to it.*

---

*Speaker notes: That last line matters — say it out loud. It signals accountability and builds trust with both audiences.*

---

---

# SLIDE 15

## Next Steps

### Three things we need from you today

---

**1. Align on language**
Agree that your teams will use WS names when asking about our work.
*Action: Share the work stream table (Slide 5) with your direct reports this week.*

**2. Name your feedback lead**
Who on your team will route recurring case patterns or client concerns back to us?
*Action: Tell us before we leave this room, or follow up by [Date].*

**3. Client Success: Identify early advocates**
Which 2–3 clients are good candidates to be early users of CRC chat when it launches?
*Action: Connect Ryan with those account owners by end of Q1.*

---

### What happens next

- **[Date TBD]** — Chat v1 (WS-1) UAT begins · Support leader participation requested
- **[Date TBD]** — Amazon Connect migration kickoff · Scope review with affected team leads
- **[Date TBD]** — End of Q1 briefing · Progress update + first metrics check-in

---

### Questions?

*Reach Ryan Dunn at [email / Slack channel]*

**Thank you.**

---

*Source: [[2026-06-02 - Work streams]] · [[TPC - FY27 Containment Strategy]]*
