---
fileClass: note
type: note
created_date: 2026-06-01T00:00:00.000Z
notes_status: Reviewed
meta:
  - Whiteboard
topics:
  - '[[TPC - FY27 Containment Strategy]]'
entities:
  - '[[Michael Proffer]]'
---
# My Notes
## Token Limit Issue
* hit up Josh
* we are repairing something that we believe should have been caught
* MP is working on options, but only catching it. we need to retool articles ingest due to size
* Article size is the issue here
* this will impact CHAT which we are doing now!
	* chat can't push to a human, so this is a block to chat

## Josh feedback
* the spped jade says for GECX makes it hard on michael and I

## Critical Path - Chat
* Tommy Knuckles Training
	* 6/11 + 6/12, get it on the books
	* Recorded for Annette
		* michael.proffer@wellsky.com
		* corbin.calvert@wellsky.com
		* gage.riker@wellsky.com
		* gage.bradley@wellsky.com
		* tom.lemon@wellsky.com
		* ryan.dunn@wellsky.com
		* abhirup.dash@wellsky.com
		* annette.villareal@wellsky.com
		* Vivek
* Google Training
	* ASAP
	* cost? 
	* do we need to knock this otu before Tommy? 
* 6/19 - internal deadline (not to Chris)
	* MP team has high level LOE
* 6/23 - Ryan is back, review plan with MP
* 6/26 - we will have a timeline for Chat for PC and estimate for the remaining under the assumption our PC implementation estimate is correct. 
* MP - work will start by 6/19 in DRAFT forms, like in DEV

==Action Items==
* Token Issue - follow up with Josh
* Chat
	* Training with Tommy Knckles
	* Training from Google
	* meeting with SF Team - Katie and Brad
		* Katie -> SF integration API for cases
		* Brad - CRC consolidation or not, date from Brad?
	* Vivek - after Tommy Knuckles, align on architecture
	* McCall - define metrics

![[Pasted image 20260601112332.png]]
## Key Details in this meeting
* requirements for Tommy for GECX architecture
* formalizing what is and is not in scope for this version of chat

# Summary ******

## Token Limit Issue — Current Production Blocker

### What Happened
- Articles in the current knowledge store are exceeding the Gemini voice agent's token limit
- Root cause: article size was never constrained in the original build — no guidance to cap articles at a character/token limit
  - *"At no point did they say, and also make sure your articles are below X number of characters... I could have made that a part of the upload process"*
- Should have been handled in the ETL/export script at the chunking stage — *"It should have been part of the ETL script, the export script. That's where they should have chunked it"*
- Attributed partly to the original implementation moving fast; Jelloret did a good job under the circumstances but the miss was in the ETL design

### Current Frequency
- ~15 occurrences in a single day out of ~500 non-payer calls (very low rate)
- Tom has a query to pull the historical count — Ryan will ask Tom to run it (low effort, adds weight to Josh conversation)

### Short-Term Resolution (In Progress)
- Corbin implementing an **event handler** to catch token failures and route to human queue with a message
  - *"We catch the event, when it happens, we'll error handle and basically fail to a human queue"*
- Token limit is also being increased — Corbin confirmed easy, just a cost question; Ryan approved
- Google Gemini resource (primary contact) currently out of office; backup contact should be asked to prioritize error handling assistance

### Why This Blocks Chat
- Chat has no human handoff — a token failure in chat leaves the user stranded with no context
  - *"The nuance with chat is there's nowhere to send them"*
- Long-term fix: build a native if-statement error handler into the chat design from day one

### ⚡ Action: Follow Up with Josh (MP meeting Thursday)
- MP will draft message first and share with Ryan before sending
- Framing: partners aligning, not blame — but direct about the miss
  - *"I'm going to be kind of direct with him... Michael's team has got to do all this stuff. And instead we're band-aiding misses from you guys"*
- Secondary message to Josh: Jade's "it's fast and easy" comments in front of Chris set unrealistic expectations
  - *"When you guys are saying that stuff in front of Chris... Chris, who's a non-technical leader, walked out of there going two weeks"*

---

## Chat v1 Scope — Decisions Made

### Scope: Personal Care Only
- Chat v1 = **CRC chat for Personal Care only** — agreed, no exceptions for this version
  - *"This is CRC chat for personal care only. Yes, that's it"*
- Personal care chosen as a "target-rich environment"

### CRC Surface
- **No change to CRC** for v1 — chat embedded as a URL drop-in only
  - *"We're just embedding a URL in there"*
- CRC consolidation (Brad's initiative) is a separate conversation; may actually complicate chat auth

### Knowledge Architecture
- **GCP bucket (existing knowledge)** — NOT the Knowledge Catalog / graph DB
  - *"We've got the existing knowledge... GCP bucket... not graph, not knowledge cloud"*
- Graph DB / Knowledge Catalog deferred to a future chat version
  - *"Why jack with it? Just we got to do this first"*

### Authentication
- Auth required — **Vivek owns the approach**
- Likely v1 path: **Salesforce session passthrough** — infer user identity via CRC's native Salesforce architecture, avoiding explicit Okta for v1
  - *"If we tie back to Salesforce, we know their user, we've assumed authentication, then we don't have to do any of it in the tooling itself"*
- Okta as explicit auth deferred to v2 / solution in-app scenario

### Salesforce Integration
- **Vivek owns** — minimum viable: 2 APIs
  1. Get list of cases for the authenticated user
  2. Get case details per case
- Case write-back (update) = **v2**, not v1
- ⚡ **Action: Meeting with Katie (SF team) and Brad** — MP to schedule
  - Katie: confirm SF integration API support for cases
  - Brad: CRC consolidation timeline + implications for chat auth

### Agent Studio Design (Not a Migration)
- Google offered no formal Dialogflow → Agent Studio migration path
  - *"Google never offered us any kind of migration, formal migration pathway"*
- Best case: BLOB export of existing Dialogflow agent imported as starting point, then layered with chat requirements
- Single Agent Studio flow for both chat and voice (per Jade) — customized at channel level
  - Voice: concise / Chat: verbose, can include links

### Solution Customization Requirement
- Key architecture requirement: **ability to customize per solution / knowledge source**
- **EVV is the driving example**: sub-categorized knowledge within Personal Care for EVB/EVV code topics
  - *"I think what I want is a knowledge source specific to a use case... I go back to EVV"*
  - Multiple stakeholders have requested this pattern after Steve raised it
- This aligns naturally with the future metadata-tagged Knowledge Catalog architecture
- Vague today — to be clarified with Tommy Knuckles; team should push back if not achievable

### Chat Directory Skill
- Small skill to handle cross-solution questions in chat
  - If user in Personal Care asks a Home Health question → knowledge article/skill redirects them
  - *"We need a little skill that'll link them to the other... that's an article"*

### Chat Containment Metric
- Defining what counts as "contained" in chat = **McCall's responsibility**
- Ryan to provide data points from the chat system so McCall/Gage Riker can build the metric
- ⚡ **Action: McCall — define metrics**

### CCAI / Case Logging (Tommy Question)
- Open: does chat require a CCAI module if there's no human behind it?
- Risk: logging a SF case for every chat interaction (including non-cases) pollutes data
  - *"Out of every 10 chats, you get 3 cases. Are we actually gonna have 10 cases... I'm hoping not"*
- Goal: **good cases only** — only log when a real support need exists
- This is a Tommy Knuckles architecture question

### v2 Scope (Deferred)
- Solution in-app deployment
- New auth model (Okta)
- Additional solution APIs (TBD)
- Knowledge Catalog / graph DB integration

---

## Training Schedule & Sequence

### Step 1 — 8-Hour Online Training (ASAP)
- Full team must complete the **8-hour Google Agent Studio online training** before Tommy Knuckles
  - *"It's an eight-hour training"*
- Ryan formally communicated this in writing; will reinforce verbally at team meeting this week
- Zaid must grant access to the learning platform
- ⚡ **Action: Training with Tommy Knuckles** — get June 11/12 on the books

### Step 2 — Tommy Knuckles Architecture Session (Target: June 11 or 12)
- Requested dates: **June 11 or 12** — must be before MP's June 15 vacation
- Session will be **recorded for Annette** (out until June 15)
- Attendees: Michael Proffer, Corbin Calvert, Gage Riker, Gage Bradley, Tom Lemon, Ryan Dunn, Abhirup Dash, Annette Villareal (async), Vivek
- Not every team member needs to have finished training — Ryan and MP just need to hold the conversation
  - *"As long as you and I can hold the conversation with Tommy, and I think Vivek will be there, I think we're fine"*
- **MP will prepare a design doc for Tommy** before the session covering:
  - Existing conditions (GCP bucket, no KC for v1)
  - Per-solution customization requirement
  - Architecture open questions (see below)
  - Go-live function clarification

### Step 3 — Google Training (Separate, Cost TBD)
- Josh offered a Google training resource — MP will ask if required or optional before booking
- Cost may be involved
- ⚡ **Action: Training from Google** — confirm cost and necessity with Josh

### Step 4 — Vivek Alignment (After Tommy)
- After Tommy Knuckles session: Ryan + MP + Vivek align on architecture
- Vivek to confirm ownership of auth + SF integration approach
- ⚡ **Action: Vivek — after Tommy Knuckles, align on architecture**

---

## Key Dates & Milestones

| Date | Milestone |
|---|---|
| **June 11–12** | Tommy Knuckles architecture session (target) |
| **June 15** | MP out of office |
| **June 15** | Annette returns from leave |
| **June 19** | Internal deadline (not to Chris) — MP's team has high-level LOE for chat |
| **June 23** | Ryan back — review plan with MP |
| **June 26** | Deliver to Chris: Personal Care chat timeline + estimate for remaining solutions |

- No go-live date commitments to Chris until all training is done and Annette is back and caught up
  - *"I am not going to ask my team to commit to a date until... we need to get through almost all this"*
- MP's framing to Chris during his week out: *"Work has begun... hands are on keyboard, we just haven't put dates to it"*
- If Chris pushes for a date: commit to providing a go-live date by June 26, not sooner

---

## CRC Consolidation — Brad

### Context
- Brad wants to consolidate CRCs from 25 to 1
- His motivation: outdated Salesforce library packages creating Salesforce liability for his team
  - *"His packages are out of date in the CRC, they're barking at him"*

### Ryan + MP Position
- **Preference: kick the can** — CRC is going away anyway when tech writing moves to the new data store pipeline
  - *"Why consolidate if we're telling him it's gonna go away anyway?"*
- Consolidation may actually **complicate chat**: a unified CRC loses solution-level context (which solution is the user in?) — needed for chat routing and auth
  - *"He's gonna look at authentication generically and we need to know which solution the person is coming into"*
- MP to schedule a meeting with Brad, Katie, Ryan — surface the implications for chat before Brad commits to a timeline

---

## Amazon Connect — Critical Path

### Molly Wild Card
- Molly (Corp IT) needs to provide Annette/Corbin with info to rebuild the 855 WellSky phone tree (including voicemail destinations)
- Cases are logged for her work; some items still waiting (e.g., full mapping of existing tree)
- History of falling behind — *"Our wild card here is Molly"*

### Plan
- Ryan to create a parallel Amazon Connect critical path with dates and owner assignments
- Use Jared as PM to bird-dog Molly's commitments
- Goal: clear paper trail — if Molly misses, the accountability is documented

---

## Team Ownership

| Role | Owner | Scope |
|---|---|---|
| Technical lead / Agent Studio | Michael Proffer (Tier 0) | Architecture, design, overall delivery |
| Auth + SF integration + APIs | Vivek (GenAI CoE) | All Vivek-dependent integration work |
| VA build / development | Corbin + Annette (CE Ops DEV) | Right of first refusal on all VA work |
| Delegate / overflow dev | Abhirup | Safety valve when Corbin/Annette are at capacity |
| PM / timeline coordination | Jared | Bird-dog dates, cross-team commitments, accountability |

- MP's direction on Jared: *"I need him to be the PM... He's not technical enough to know what they are, but he'll say it in the meeting and someone's gonna go, oh crap"*
- Annette is the lead — she returns June 15; give her a week to get caught up before hitting her with scope details
  - *"I don't want her reacting in the rear"*

---

## Open Questions for Tommy Knuckles

- Can Agent Studio flows be customized per solution/BU without building separate flows?
- Should chat and voice share a **single Agent Studio flow** (Jade's recommendation) or separate flows?
- Can the BLOB export of the existing Dialogflow agent be used as a starting point for Agent Studio?
- Do we need a CCAI module enabled for chat if there's no human behind it? How do we avoid logging junk Salesforce cases?
- What API key model does Agent Studio use — shared GCP cloud keys, or new keys required?
- How does Agent Studio handle solution-specific knowledge sources within a shared flow architecture?

# Transcript

speaker1：[00:00:00 - 00:00:06]

I'm surprised they didn't offer you more into my office. Oh yeah, alright.

speaker1：[00:00:13 - 00:00:13]

Okay.

speaker1：[00:00:22 - 00:00:28]

Okay. Alright, that's what we'll do.

speaker1：[00:00:29 - 00:00:31]

Alright, thank you very much. Alright, I gotta go.

speaker1：[00:00:31 - 00:00:39]

Alright, love you. The damn cat got in a fight the day we left for Milwaukee, so we took him to get cleaned up.

speaker2：[00:00:39 - 00:00:40]

Oh, no.

speaker1：[00:00:40 - 00:00:43]

Bum from where the puncture was. And we're like,   it, so we've come back in.

speaker1：[00:00:43 - 00:00:47]

And of course, the vet was like, I don't love it, but he already had antibiotics.

speaker1：[00:00:47 - 00:00:56]

So it's either do nothing, see if it goes away, or get a needle in there or take an extra. And it's funny, too.

speaker2：[00:00:57 - 00:01:00]

We got 2 cats. What do you have for pets?

speaker1：[00:01:00 - 00:01:02]

They're just a cat and three chickens.

speaker2：[00:01:02 - 00:01:04]

Oh, 3 chickens? Oh, that's super cool.

speaker2：[00:01:05 - 00:01:12]

I was always a big dog person. And then once the kids got old enough, I didn't feel like I could give the dog like a good, you know what I mean?

speaker2：[00:01:12 - 00:01:18]

Like I wasn't running it as much as I wanted to and all that jazz. So once that dog passed away, we just got some cats.

speaker2：[00:01:18 - 00:01:22]

But I mean, my daughter, especially, like, I mean, It loves the damn cat.

speaker2：[00:01:23 - 00:01:26]

Like, it's been a great pet. So we got 2 cats.

speaker1：[00:01:26 - 00:01:31]

Yeah, and I know you, because I remember you told me about you, rescue because of the vet situation.

speaker2：[00:01:32 - 00:01:36]

Yes, I have an unlimited supply of unlimited animals, so let me know.

speaker1：[00:01:38 - 00:01:41]

But anyway, it was just kind of one of those things. I was like, we found them.

speaker1：[00:01:41 - 00:01:43]

I was like, it's not normal. I was kind of, we'll see though.

speaker1：[00:01:43 - 00:01:45]

We'll see. It's not a big deal.

speaker1：[00:01:45 - 00:01:48]

But it's also, his Bibles are good, which is the main thing. So it'll just go away.

speaker1：[00:01:49 - 00:01:50]

Good. Hello, sir.

speaker2：[00:01:50 - 00:01:52]

Yeah, cool, man. Did you have a good weekend?

speaker1：[00:01:52 - 00:01:53]

Happy Monday. Yeah, it was good.

speaker1：[00:01:53 - 00:01:53]

It was fun. Good.

speaker1：[00:01:53 - 00:01:55]

I did a good game of soccer yesterday. Can't complain.

speaker2：[00:01:56 - 00:02:00]

Nice. I'm I think I'm another probably 4.

speaker2：[00:02:00 - 00:02:05]

I'm 4 weeks from Friday. So I partially tore the stupid piece of my foot.

speaker2：[00:02:05 - 00:02:15]

But well, I thought I thought on, let's see, on Wednesday evening, I'm like, I think the tendon's detached and it might have pulled something off the bone.

speaker2：[00:02:15 - 00:02:21]

So you're like, I was like, I need to go in and check because it was just too painful. Like I'm sitting here walking around and I'm like, yeah, you were not good.

speaker1：[00:02:22 - 00:02:22]

Yeah.

speaker2：[00:02:22 - 00:02:26]

Oh man, it was so frustrating. Soon I went, I got an x-ray and everything.

speaker2：[00:02:26 - 00:02:31]

So the point is, I'm jealous that you got the play and I'm very, I don't know what the word is.

speaker2：[00:02:31 - 00:02:35]

Annoyed, embarrassed, something of the group.

speaker1：[00:02:36 - 00:02:44]

We keep talking about like one, me or Diana, one of us is gonna do something at some point. It's just, Matt, you keep doing it, you're gonna just, you know, that's what happens though.

speaker2：[00:02:44 - 00:02:51]

It is, it is, but I feel like it's very motivating to like the normal workouts. Then I feel like I could be okay.

speaker1：[00:02:51 - 00:02:53]

Yeah, that's true, yeah, Staying forward.

speaker2：[00:02:54 - 00:02:54]

Cool, man.

speaker1：[00:02:54 - 00:02:57]

Cool. Well, yeah, let's jump in.

speaker1：[00:02:57 - 00:02:57]

Let's chop it up.

speaker2：[00:02:57 - 00:03:02]

Yeah, so here's where my head was at to just kind of like high level this thing.

speaker2：[00:03:03 - 00:03:21]

Like I think what we need to do is kind of land the near term, which I think is, and when I say that, what I mean is kind of like with the team, like, hey, let's figure out some dates on when we can commit to having training done, so then we can engage Tommy Knuckles. Vivek needs to be part of that.

speaker2：[00:03:21 - 00:03:27]

And then I think ultimately after Tommy goes through and says, hey, here's how I do it.

speaker2：[00:03:27 - 00:03:32]

I think we, meaning me, you, and Vivek, need to kind of like say, okay, we hear Tommy, do we agree?

speaker2：[00:03:34 - 00:03:38]

And so I think that's kind of in my head, like the near-term couple weeks.

speaker2：[00:03:39 - 00:03:46]

In there somewhere is that training resource, Josh said, so we can land that. So I think that's like the near-term stuff.

speaker2：[00:03:46 - 00:03:55]

And then the longer-term stuff, I think is like, Just figuring out like how do we want to go about implementing it, right?

speaker2：[00:03:55 - 00:04:01]

Like, I mean, just breaking down the work. I think we've got some integration stuff.

speaker2：[00:04:01 - 00:04:08]

I think we should land on like, I think you and I should determine like who's doing what, kind of saying like you have right of first refusal for any work.

speaker2：[00:04:09 - 00:04:14]

But I think we got delegates on Avirup and Vivek. And I think, you know what I mean?

speaker2：[00:04:14 - 00:04:18]

Like, I think So I think there's that.

speaker2：[00:04:18 - 00:04:29]

I think the underpinning, just so the anxiety I'm worried about is making sure we can do, we aren't basically killing Corbin in the net because are we still in the Amazon Connect stuff?

speaker2：[00:04:29 - 00:04:38]

So I think when I was noodling on, you had told me, you said, hey, I said, hey, critical path for Amazon Connect. And you're like, well, here's what I got.

speaker2：[00:04:38 - 00:04:40]

Is that good enough? And I was like, sounds like it.

speaker2：[00:04:40 - 00:04:51]

I was sitting there noodling on it. And I think for me, I think probably for both projects, we need to define the key milestones that tell us if we're on track or not.

speaker2：[00:04:52 - 00:05:04]

And then, I think from there, it's probably at least saying, who's owning those milestones? Kind of trying to avoid it to be you or I.

speaker2：[00:05:06 - 00:05:19]

But I don't know, that may not be reality. So I don't know, that's just where my head's at because My thought is, like, and before we do all this, I want to talk about the token thing, but that token thing is actually very timely. Because this is going to continue to happen the whole time through the project.

speaker2：[00:05:19 - 00:05:33]

So it's also like, I think just being organized, because when this crap happens, if we've got the critical path, well, we lost four weeks because of the token BS, the whole thing just shifted, right? We don't all just magically work all night.

speaker1：[00:05:33 - 00:05:38]

Right, yeah, exactly. And I think I appreciate that and just being aware of it and knowing we know that more will come up.

speaker1：[00:05:38 - 00:05:42]

Now granted, It seems like we have a handle on this.

speaker1：[00:05:42 - 00:05:47]

I mean, Corbin's responding appropriately now and I've kind of laid out, you know, here's who's doing what.

speaker1：[00:05:48 - 00:05:53]

But that doesn't change our, yeah, I mean, it's a commitment time.

speaker2：[00:05:53 - 00:05:56]

So let's talk about that. Let's figure out what you and I want to do about that.

speaker2：[00:05:56 - 00:06:05]

If I need to bark at Google, if we want to go back. So I was just, I read through that and then was like, okay, I'll hold off on going too deep until you get here.

speaker1：[00:06:06 - 00:06:09]

So let me. Because I spun this up.

speaker2：[00:06:09 - 00:06:10]

You're all good, man.

speaker1：[00:06:10 - 00:06:11]

And now I'm getting chats, which is great.

speaker2：[00:06:14 - 00:06:16]

Where did I put this? There we go.

speaker2：[00:06:16 - 00:06:19]

Okay. That's weird.

speaker2：[00:06:19 - 00:06:20]

Why didn't I see you?

speaker1：[00:06:24 - 00:06:25]

Yeah, okay.

speaker2：[00:06:25 - 00:06:27]

I see what I got. I got the thing messed up.

speaker2：[00:06:27 - 00:06:31]

Okay. so.

speaker2：[00:06:41 - 00:06:43]

Okay, so they're doing the event handler.

speaker1：[00:06:44 - 00:06:47]

So we should be good. So Corbin is increasing.

speaker1：[00:06:47 - 00:06:51]

He did put in, he said it was easy to increase the token.

speaker2：[00:06:51 - 00:06:53]

Good. Okay, I was going to say I can do it if you didn't.

speaker1：[00:06:53 - 00:06:57]

No, yeah, so he just said it's a matter of cost. Obviously I was like, yeah, we can.

speaker2：[00:06:57 - 00:07:00]

No, go do it. And I am more than happy to.

speaker2：[00:07:01 - 00:07:02]

Hit that on the back end.

speaker1：[00:07:02 - 00:07:20]

So then we are basically the, so we'll put in the, and frankly it happens rarely enough that we're over, well, we are overreacting in the sense that we're doing all this stuff, but if we can get the event handler in, we can almost just ignore everything else, knowing that eventually we'll get it.

speaker2：[00:07:20 - 00:07:29]

Fixed, but because I wanna make sure I understand why, because you're gonna catch the event, it's gonna throw, you're gonna handle it, but the point is you're also gonna see that there's a gap, and then you're gonna plug it.

speaker1：[00:07:29 - 00:07:37]

So, yeah, well, basically, we catch the event, when it happens, we'll error handle and basically fail to a human queue. So, okay, perfect.

speaker1：[00:07:37 - 00:07:42]

So, but it'll be an inelegant, like, you know, it'll probably, you ask it a question, and it'll be, Ah,  I die.

speaker1：[00:07:42 - 00:07:46]

Yeah, and they'll have no contact, so it'll just get thrown into a hold.

speaker2：[00:07:47 - 00:07:48]

But they're not dead.

speaker1：[00:07:48 - 00:07:55]

But they're not dead. Yeah, or maybe in the error handler you can, I don't know, maybe in the error handler we can see.

speaker1：[00:07:55 - 00:08:00]

say we've encountered an issue and due to this we'll be connecting you to OLS guy teammate. You know something like this.

speaker1：[00:08:00 - 00:08:10]

It's happened, it happens at like most often it happens at like 15 out of every 500 calls or something. So this is a low, low, low number.

speaker2：[00:08:10 - 00:08:14]

So give me those numbers again. Just guess, I'm not holding it to you.

speaker1：[00:08:14 - 00:08:24]

So hold on, there was a one day, one day we hit it 15 times. So it's the numerator is 15, the denominator is total average calls a day for non-payer.

speaker2：[00:08:27 - 00:08:34]

So here I can cut that up real quick. Good.

speaker1：[00:08:34 - 00:08:34]

Yeah.

speaker2：[00:08:36 - 00:08:40]

But okay, so my two cents on this though, and I'm curious what you think my reaction is.

speaker2：[00:08:40 - 00:08:45]

I feel like this was kind of Taylor, what's his name? Jarlette.

speaker1：[00:08:46 - 00:08:46]

Yeah.

speaker2：[00:08:47 - 00:08:54]

I feel like this is a. man, he remember, I mean, I always remember saying like, dang, he did it pretty quick.

speaker2：[00:08:54 - 00:08:58]

And then, and then we're like, all right, good. And I feel like this is that he was green.

speaker1：[00:08:59 - 00:08:59]

Yeah.

speaker2：[00:08:59 - 00:09:08]

And, I, and I still think he did a great job. I am not complaining, but I'm also sort of like, you know what I mean?

speaker1：[00:09:08 - 00:09:08]

Yeah.

speaker2：[00:09:08 - 00:09:10]

And so is that, is that a reasonable?

speaker1：[00:09:10 - 00:09:12]

I, yeah, Jelloret, that's his name. Yeah.

speaker1：[00:09:15 - 00:09:27]

Yeah, I think you're right. I mean, they didn't know, like they were at no point did they say, and also make sure your articles are below X number of characters.

speaker1：[00:09:27 - 00:09:34]

And that was exactly like, tell us that it can't be greater than say 10 pages or whatever, 10,000 characters. I don't care.

speaker1：[00:09:34 - 00:09:40]

I could have made that a part of the upload process. It would have been, you know, and really.

speaker1：[00:09:41 - 00:09:47]

Honestly, no. I mean, really what should have happened was it should have been part of the ETL script, the export script.

speaker1：[00:09:48 - 00:09:49]

That's where they should have chunked it.

speaker2：[00:09:50 - 00:09:51]

Yeah, it should have been caught.

speaker1：[00:09:51 - 00:09:58]

Yeah, it should have been caught. And so that's probably, if you want to run that, I mean, I'm sure Josh is going to be like, well, it's too bad.

speaker1：[00:09:58 - 00:09:59]

Let me know if I can, you know, he's just.

speaker2：[00:10:00 - 00:10:11]

Going to say, stand up. Well, I want to make the statement to Josh and say, hey, kind of saying, look, here's what we're doing. Here's our view of the screw up.

speaker2：[00:10:12 - 00:10:18]

And then be like, Josh, like, let's you and I get a line on what's going back to Chris, right? Like, let's be partners on it.

speaker2：[00:10:18 - 00:10:24]

I'm not trying to throw you under the bus. But like, I'm going to be kind of direct with him.

speaker2：[00:10:24 - 00:10:30]

I'd be like, you know, Michael's team has got to do all this stuff. And instead we're band-aiding misses from you guys.

speaker2：[00:10:30 - 00:10:37]

And I think that's kind of the vibe I want to give him. to say, and so, okay, so basically, I mean, awesome, awesome job.

speaker2：[00:10:37 - 00:10:42]

I'll hit up Corbin Engage because I'm like, their ability to react to that effectively is huge.

speaker2：[00:10:43 - 00:10:57]

I mean, because if we weren't like, even though it's minor, if they weren't able to do that, Sherpatel would be all over Chris and then Chris would be all over us for 15 calls a day, which I'm not saying is insignificant. But I mean, you and I tend to kind of be like, It's fine.

speaker1：[00:10:57 - 00:11:06]

Yeah, but at the same time, and that's kind of what I put in here is like, I actually, I think I did in the original message. What did I say?

speaker1：[00:11:09 - 00:11:13]

Yeah, given our clients are getting truly stuck, a non-zero number of occurrences is unacceptable.

speaker2：[00:11:14 - 00:11:14]

Exactly.

speaker1：[00:11:14 - 00:11:16]

That's kind of where I'm at on that. It just, yeah.

speaker2：[00:11:17 - 00:11:24]

Well, and I think you and I, that's exactly the tone we always have to take. It's one in 15 under it's like.

speaker1：[00:11:25 - 00:11:37]

So, and so anyway, so I'm not, it's one of those things too where I don't, this is where I don't think I necessarily need to know. I'm not an engineer, I'm not in the guts of the thing all day long.

speaker1：[00:11:37 - 00:11:44]

I wish I had a little bit better line of sight on the error handling itself. What goes into that?

speaker1：[00:11:44 - 00:11:51]

I also, because it came up and I said what would go into that to the Google Gemini resource. And he hadn't addressed it yet.

speaker1：[00:11:51 - 00:11:57]

So I'm like, all right, does that mean we're going to go after Google, this guy? And of course, ironically, not ironically, whatever, it's the way it always works.

speaker1：[00:11:58 - 00:12:04]

Google Gemini resource we were working with, who's been really good, is out of the office right now. So he's got a person backing him up.

speaker1：[00:12:04 - 00:12:10]

So maybe I'll just jump in there and say, hey, number one priority as we're reading through this is to assist us with the error handling.

speaker1：[00:12:11 - 00:12:25]

The other thing that I think going back to Josh long term is we know this is a problem right now with the way that it is Our article sizes are too large, which is exceeding a token limit. I mean, that's kind of the.

speaker2：[00:12:25 - 00:12:28]

Yeah, that's a black and white event. Who cares, who cares, who cares?

speaker1：[00:12:28 - 00:12:33]

So that presents, I mean, and that is the base of all of what we're doing.

speaker1：[00:12:33 - 00:12:40]

That presents, you know, so when we build a chat bot, we could have, you know, that insinuates we can have problems with the chat.

speaker1：[00:12:40 - 00:12:47]

Anything that's hammering this data store, we could have unpredictable outcomes. So that's where I'm kind of like, yeah, we got error handling for this one.

speaker1：[00:12:48 - 00:13:07]

And we'll learn our lesson, and as we're building out chat in this new environment, we'll make sure to build in error handling for when, like, we just need to know from now on an if statement, if token limits are exceeded, then do whatever. But we need to structure our data.

speaker2：[00:13:07 - 00:13:10]

Well, because the nuance with chat is there's nowhere to send them. It's like dirps and dirps.

speaker1：[00:13:10 - 00:13:15]

And then you're like, what are you going to do? Yeah, it's like I logged a case for you, I screwed up and I logged a case for you.

speaker1：[00:13:15 - 00:13:22]

So yeah, it's like. The error handling is fine, and we can kind of walk away from it at that point, but we can't totally walk away from it, and that's where it gets a little nice.

speaker2：[00:13:23 - 00:13:26]

Well, and I want, and this is very much, so anyway, okay, I'm totally aligned.

speaker2：[00:13:27 - 00:13:39]

I'll hit you up with a draft of what I'm gonna tell Josh, and then he's out of town today, so my meeting with Josh is Thursday. Yeah, Thursday.

speaker2：[00:13:41 - 00:13:45]

Okay, so okay, so we, so okay, so I think we're good there. I'm aligned with you.

speaker2：[00:13:48 - 00:13:57]

I mean, I mean, I am just super happy with the Band-Aid because it's like, I feel like it's big time dodged to bullet. Yeah, So good job.

speaker1：[00:13:57 - 00:14:04]

Thank you. I mean, I wish we'd have found it sooner because it's one of those, I don't, I'm gonna put the blinders on and not go look and see how many times we had it occur since jam one.

speaker2：[00:14:05 - 00:14:10]

Let's, yeah, I'll tell you, if I feel like I'm gonna get that type of pressure from Chris, I'll try to give you a line of time to it.

speaker1：[00:14:11 - 00:14:19]

Frankly, Tom already figured out a query to go tell how many times it exceeds, because it's a rubber stamp error, so we can get the number.

speaker2：[00:14:20 - 00:14:26]

Good. I mean, I would say that if it's not high labor at some point at Tom's leisure.

speaker1：[00:14:26 - 00:14:31]

Yeah, probably a good idea. I'll ask him on the back end and say, Hey, can you just tell me what it was so I know?

speaker1：[00:14:32 - 00:14:36]

Yeah, because then actually maybe it adds a little bit more weight to your conversation with Josh anyway.

speaker2：[00:14:36 - 00:14:42]

Yeah, it will, and I think it also just makes us look button up to Chris, you know what I mean? Also, not implying it on the pressure.

speaker1：[00:14:42 - 00:14:45]

No, I'm with you. Since it's easy, I will go get it.

speaker2：[00:14:45 - 00:14:47]

Cool, Okay, cool.

speaker1：[00:14:47 - 00:14:51]

All right, so going back to chat, let me tell you kind of where I'm at on it, just as far as chat's concerned.

speaker1：[00:14:52 - 00:15:08]

I am going to, number one, I'm gonna go in and honestly, I'm going to look at our current sprint from a new lens and say we got a lot of  to do, so I'm gonna start dumping stuff off of here, where I'm basically gonna go to our pressure and be like... our priorities.

speaker1：[00:15:08 - 00:15:16]

If you can't get this done, or if you don't feel like, or if it's too much, tell me we're just gonna take it off the sprint. Our sprint might have two things on it, off this cycle.

speaker2：[00:15:17 - 00:15:24]

It is, because I mean, and this is the, I'm just saying out loud, like this is dysfunctional, but it's because of Chris going, go, and it's like.

speaker1：[00:15:25 - 00:15:33]

And frankly, we're in a good spot. We are, we're, we're, we've landed, we're settled a little bit, and that's obviously out of town, which adds a wrinkle.

speaker1：[00:15:33 - 00:15:39]

I mean, we're reacting to this, but honestly, I'm glad we're reacting to this week and not a month ago. You know, two months ago, you know.

speaker2：[00:15:39 - 00:15:43]

I don't want to the comment about Annette though, it's like I'm out of week two.

speaker1：[00:15:43 - 00:15:45]

So it's sort of like, it's great. I'm glad.

speaker1：[00:15:46 - 00:15:50]

And that's not to say that it's negatively affecting us. It's just, it's all part of the.

speaker2：[00:15:50 - 00:15:58]

It's just reality. And I think that the thing is, like, and just to, I always want to give you as much context as I can.

speaker2：[00:15:59 - 00:16:06]

I'm probably going to make at least a little bit of a comment to Josh. It was not anybody doing anything negative.

speaker2：[00:16:06 - 00:16:11]

But Jade being like, this is fast and this is easy and stuff.

speaker2：[00:16:11 - 00:16:23]

And I'm going to be like, Josh, when you guys are saying that stuff in front of Chris, And that there's a whole implementation execution timeline. Chris, who's a non-technical leader, walked out of there going two weeks.

speaker2：[00:16:24 - 00:16:30]

And then I have to do this whole crawlback. And I'm like, I'm not saying that I don't want you to pimp that the stuff is great.

speaker2：[00:16:31 - 00:16:36]

But I'm like, you create real material heartburn for you and I. And that occurs.

speaker1：[00:16:36 - 00:16:43]

I think that's very reasonable feedback. I was too.

speaker1：[00:16:43 - 00:16:47]

Every time, they say it's the easiest thing ever. I mean, I'm hoping he knows a little bit.

speaker2：[00:16:48 - 00:16:56]

I'm just writing down notes so that I can keep it all straight. But it's like, let's see.

speaker2：[00:16:57 - 00:17:05]

Yeah, I agree. Yeah, I agree.

speaker2：[00:17:05 - 00:17:09]

I agree. And so, and so I mean, Chris could tell when I was talking to him, he's like, oh man, blah, blah, blah.

speaker2：[00:17:09 - 00:17:15]

And I'm like, I was like, yeah, it certainly does sound better. I'll let you know when I talk to Michael.

speaker2：[00:17:15 - 00:17:16]

And we get through the training.

speaker1：[00:17:16 - 00:17:18]

Exactly. It's like, all right, so we got a big training.

speaker1：[00:17:18 - 00:17:28]

So as far as actual critical path, so I have set the, I've already set the expectation that they get it done as soon as possible.

speaker1：[00:17:28 - 00:17:37]

I mean, we have our team meeting this week and I'm just going to say formally, verbally, but what I've already given them written. And then we will go, I mean, we'll go through the training.

speaker1：[00:17:37 - 00:17:41]

We have something with Tommy that seems like the next two weeks, maybe a little bit more than that. Yeah.

speaker2：[00:17:42 - 00:17:54]

Because I think on that specifically, if you and I, why don't we throw, my thought is, what if we throw a date out to Josh or a couple dates for the week of the 8th? Somewhere in there.

speaker2：[00:17:54 - 00:17:57]

I'm thinking, oh my God.

speaker1：[00:17:57 - 00:18:00]

I mean, I think it'd have to be back. You're out the 15th through.

speaker2：[00:18:00 - 00:18:01]

I'm out the following week.

speaker1：[00:18:01 - 00:18:02]

The 15th.

speaker2：[00:18:02 - 00:18:06]

I'm out the 15th. So, and then we've got MLR on Wednesday.

speaker2：[00:18:06 - 00:18:15]

Weird. So that means, my vote would be we request a Tommy Knuckles session on the 11th or the 12th.

speaker1：[00:18:15 - 00:18:19]

I think so, yeah. And I mean, even that's a little tight, but yeah.

speaker2：[00:18:19 - 00:18:26]

I mean, I think, here's my thought. And again, I'll just, I think I just wanted you to know, like, I'll tell you my why and push back on me.

speaker2：[00:18:27 - 00:18:32]

Chris, Chris is really, really I mean, pumped, he's the same Chris.

speaker2：[00:18:32 - 00:18:43]

It's like, and so he will be looking at, he won't have any line of sight when we're doing training, but that Tommy Knuckles meeting is for him visually like, okay, that we're trucking.

speaker2：[00:18:44 - 00:18:52]

And so if the, I would say first of all, the quicker we get on the calendar the better, because then he'll go to the office. So, okay, so I'm good with that.

speaker1：[00:18:52 - 00:18:56]

So long as we, let me, okay, yes, 11 through 12 is a great time to request.

speaker1：[00:18:57 - 00:19:10]

So long as you and I kind of keep in our back pocket that we might need to push, there is even a world in which you may not be able to join the meeting and it's just us talking through it, although I'd much prefer to have you on there, or maybe not everybody's through with the training at that time.

speaker1：[00:19:11 - 00:19:18]

And really all of this is just by a little time based on our reaction to me just blowing up my team's day on Monday morning. So yeah, for sure.

speaker1：[00:19:18 - 00:19:23]

So I don't know, like we may be done with this. I don't think we're gonna be done with this today.

speaker1：[00:19:23 - 00:19:27]

But we might be done with this by Wednesday. And I say, all right, everybody, remember that thing we were supposed to do actually this week?

speaker1：[00:19:27 - 00:19:28]

Let's go do it now.

speaker2：[00:19:28 - 00:19:31]

Yeah. And I think, so then my, here's, here's my thought.

speaker2：[00:19:31 - 00:19:34]

It's a five-hour training. We're giving the team...

speaker1：[00:19:34 - 00:19:35]

Eight-hour training, actually.

speaker2：[00:19:35 - 00:19:36]

Oh, you're right. Okay.

speaker2：[00:19:38 - 00:19:41]

No, I mean, hey, man, keep me honest, dude. No problem.

speaker2：[00:19:42 - 00:19:50]

So we're giving them two weeks. I would also say this, like, that was them saying, hey, it's the same thing when we engage with Pam.

speaker2：[00:19:50 - 00:19:54]

They're like, get the really... There's not going to be any accountability.

speaker2：[00:19:54 - 00:20:01]

As long as you and I can hold the conversation with Tommy, and I think Vivek will be there. I think we're fine.

speaker2：[00:20:02 - 00:20:04]

Kind of saying like it's not like we got to be super aggressive.

speaker1：[00:20:04 - 00:20:11]

Yeah, okay, I'm with you there. Yeah, having the conversation and like making sure that the right people are in that conversation as best we can is going to be.

speaker2：[00:20:11 - 00:20:20]

So then we need to make sure that this is recorded for now. And then we want Vivek, you, me.

speaker2：[00:20:21 - 00:20:28]

Corbin, I'm going to say a beer up just because it's just help.

speaker1：[00:20:29 - 00:20:40]

Yes, in fact, if you, there you go, you have that. I gave, so I gave the list to Jason and Josh.

speaker1：[00:20:41 - 00:20:46]

Oh, okay. Sorry, one second.

speaker1：[00:20:47 - 00:20:59]

okay, and then Zaid needs to grant us access to this learning, but here's here's the poll list: everybody I have to take the learning. Okay, yeah, I put you on here, but really that's just your list that you're making right now.

speaker2：[00:20:59 - 00:21:06]

No, all good, man. Yeah, we had a nice a nice break up.

speaker2：[00:21:06 - 00:21:09]

We went off and did our respective jobs, and now we're back to the...

speaker1：[00:21:09 - 00:21:10]

Yeah, exactly, yeah.

speaker2：[00:21:10 - 00:21:14]

Did you get these other guys there? Perfect, okay.

speaker2：[00:21:15 - 00:21:17]

Okay, perfect. All right.

speaker2：[00:21:17 - 00:21:29]

So, okay, so then another thing that I'm just kind of saying, I'm not sure, is they said Tommy Knuckles is a good architect. And then we also have Google training.

speaker2：[00:21:30 - 00:21:37]

So I just wrote a note that's told, I said to Josh, I said, we'll just schedule the Google training as soon as we can.

speaker1：[00:21:37 - 00:21:37]

Yeah.

speaker2：[00:21:37 - 00:21:41]

I don't, he didn't give me any context, we've got a trainer and we can help. Great.

speaker2：[00:21:41 - 00:21:43]

So I'm just gonna say, all right, we'll schedule that.

speaker1：[00:21:43 - 00:21:46]

Yeah. I mean, based on the conversation, it sounds like there'd be some cost involved too.

speaker1：[00:21:46 - 00:21:48]

So we have to see what he comes back with. Yeah.

speaker1：[00:21:49 - 00:21:53]

So, but that does kind of insinuate kind of an important question.

speaker1：[00:21:53 - 00:21:56]

Do we take the training before we talk to Tommy, or do we talk to Tommy before we take the training?

speaker2：[00:21:56 - 00:21:59]

They specifically said, please take the training before you talk to Tommy.

speaker1：[00:21:59 - 00:21:59]

Okay.

speaker2：[00:22:00 - 00:22:02]

I think the nuance is the Google training.

speaker1：[00:22:02 - 00:22:05]

The in-person training, I mean. The training resource training.

speaker1：[00:22:05 - 00:22:10]

We need to. Well, and I guess if they're saying there's a charge involved, they can't say that.

speaker2：[00:22:10 - 00:22:17]

I'd say, it's interesting though, because I don't think they know if we have to have it or not, because you know what I mean? It's such a weird thing with Gen.

speaker2：[00:22:17 - 00:22:21]

AI where it's like, can we just handle it ourselves? Maybe, not.

speaker2：[00:22:21 - 00:22:33]

So I'll say, I'll ask though, do we need to... Okay, so all right, so perfect.

speaker2：[00:22:33 - 00:22:40]

So we're going for the 11th or the 12th. For the Tommy Knuckles training, and then, and then let's see here, record for net.

speaker2：[00:22:40 - 00:22:47]

I'm gonna say Vivex in here, we got a beer up. Okay, cool.

speaker2：[00:22:47 - 00:22:59]

Okay, so now let's assume that we are now trained and we kind of have a high level how we're gonna build it, right? So, at this point now, I mean my...

speaker2：[00:23:00 - 00:23:11]

My assumption, and just tell me if you think it's right, because you spent more time in the dialogue book than I have, and I feel like that's the only base we got, is now for chat.

speaker2：[00:23:12 - 00:23:26]

And Jade said we could use a single, basically, architecture for the virtual agent and then make nuanced changes across chat and voice. And I asked her a couple of details, and it seemed fine.

speaker2：[00:23:27 - 00:23:35]

So for example, like saying at the voice, at the channel level, we can say be more concise with the chat, say be more verbose, and Chaggy can have a link. She was like, oh, that's fine.

speaker2：[00:23:37 - 00:23:56]

So I think then the nuance would be This kind of goes back, I think, in my head to the exact way we rolled out voice, which is I think we basically have a proof of concept with, again, if we want to do personal care, it doesn't matter, but I think we pick one.

speaker1：[00:23:56 - 00:23:57]

Yeah, we've got to pick one, yeah.

speaker2：[00:23:57 - 00:24:04]

And we basically say, okay, we're going to build it out. And that'll kind of be, so here I'll start writing some stuff.

speaker1：[00:24:04 - 00:24:10]

And I am in a, I think personal care is a very target-rich environment to use. So just assume we're using it.

speaker2：[00:24:10 - 00:24:17]

Cool. So then, so then I'll just, I'm just going to say, and I just want to kind of like lay out clearly what we're doing and not doing.

speaker2：[00:24:17 - 00:24:24]

This is CRC chat for personal care only. Yes, that's it.

speaker2：[00:24:24 - 00:24:30]

And so when we're doing this, we need to Let's see here.

speaker2：[00:24:30 - 00:24:33]

A couple of things we need to do. I do think we need to auth in some way.

speaker2：[00:24:33 - 00:24:39]

And I think that that's a Vivec problem. So auth and this is Vivec on how.

speaker2：[00:24:41 - 00:24:49]

We have to do the knowledge ingest, which right now let's assume no change. So we're going to say existing knowledge.

speaker2：[00:24:52 - 00:24:56]

Existing knowledge. And so I'm gonna put GCP.

speaker2：[00:24:56 - 00:25:00]

I'm gonna keep writing GCP bucket. Sure, yeah.

speaker2：[00:25:00 - 00:25:02]

Because I'm just meaning that's not graph.

speaker1：[00:25:02 - 00:25:05]

Right, not graph, not knowledge cloud, or knowledge, whatever they're calling it.

speaker2：[00:25:05 - 00:25:10]

I know, and it's a stupid name. I'm like, I'm gonna get it confused forever.

speaker2：[00:25:11 - 00:25:15]

Okay, so if we got the auth, we've got the existing knowledge.

speaker2：[00:25:16 - 00:25:34]

I think a maybe here is any Salesforce integration. And so why don't we say, Why don't we say TBD, but we need Katie. And we need to say for Katie, I think, so this is very much what do you think?

speaker2：[00:25:34 - 00:25:43]

I think at a baseline level, and I'm even going to call this POC. I shouldn't do that for Chris, he's looking mad about that.

speaker2：[00:25:43 - 00:25:59]

But I think they should be able to say, I'm a user, I have a case, or cases. So this would be Users, cases, and I'm going to say details per case.

speaker1：[00:26:00 - 00:26:02]

Yeah, so it can fetch context.

speaker2：[00:26:02 - 00:26:07]

Yeah, because to me, this is 2 APIs. I'm a user, so give me the list of cases.

speaker2：[00:26:07 - 00:26:17]

And then based on that list, I get the details. Now it would be, I'll put this as one, because two would be update case.

speaker2：[00:26:19 - 00:26:24]

And that's simply, I think that's all Katie. Can you support those integrations?

speaker1：[00:26:25 - 00:26:33]

And I will say, just as a kind of editorializing, I think that use case isn't going to be very common, as common as we think.

speaker1：[00:26:33 - 00:26:38]

I just don't people, so when you log a case in CRC.

speaker1：[00:26:39 - 00:26:46]

you get that and then you go off and do your business and you wait for an update. When you get the update, it's in the form of an e-mail or a case comment.

speaker1：[00:26:47 - 00:26:58]

So I think a lot of people are actually going back in, or not going back in, they're just replying to the e-mail or a case comment, which then chews through the Salesforce system and ends up on a case anyway. So I don't, and I could be wrong.

speaker1：[00:26:58 - 00:26:59]

I mean, that's just my impression.

speaker2：[00:27:00 - 00:27:05]

I think you're right. My priority for doing it is to basically show.

speaker1：[00:27:05 - 00:27:08]

I mean, it's still, we have to do it. Sorry, let me.

speaker1：[00:27:09 - 00:27:13]

What I just said is we have to do it, but we can keep it pretty basic.

speaker2：[00:27:13 - 00:27:20]

That's what I thought, because for me, if I'm being totally transparent, I want to see an enterprise API integrated into chat.

speaker2：[00:27:20 - 00:27:25]

I'm pretty indifferent on what, but if we don't establish something...

speaker2：[00:27:27 - 00:27:40]

But I think the reason I say it like that is because if you have a more impactful use case, I think, again, Salesforce, I'm all ears, but I don't want it to be weird or anything, you know what I mean? But I think I'm very much aligned with you.

speaker2：[00:27:40 - 00:27:40]

It's like rare.

speaker1：[00:27:41 - 00:27:48]

And then the other thing, the risk of sounding like a broken record, but the Vivec auth stuff can be tied to Salesforce.

speaker1：[00:27:48 - 00:28:05]

Like, I mean, if we can fetch the user information from Salesforce, then now it is our, it goes back to it's a band-aid, but it doesn't allow you to utilize, well, you still get to utilize Okta as a bludgeon for all of these.

speaker2：[00:28:06 - 00:28:10]

Maybe, I mean, I think those are things where like I have an opinion, but I think it's all kind of a Vivec and Kate.

speaker1：[00:28:10 - 00:28:18]

Yeah, but like we could, if we tie back to Salesforce, we know their user, we've assumed authentication, then we don't have to do any of it.

speaker1：[00:28:18 - 00:28:23]

in the tooling itself, which is my preference, because we've already got them in the front door, the assumption we got them in the front door.

speaker1：[00:28:23 - 00:28:32]

Now, all that's out the window as soon as we introduce it into a solution, but this is V1, so I'm not, yeah.

speaker1：[00:28:32 - 00:28:39]

And even with the solution, the personal care, certain profiles, which again, we still know their Salesforce profile based on their Okta.

speaker2：[00:28:42 - 00:28:48]

That's a good, let's look for the sake of doing it. Let's say this is V1, yeah, and then I'm gonna say.

speaker1：[00:28:48 - 00:28:50]

And get rid of POC, that's right.

speaker2：[00:28:50 - 00:29:11]

And then I'm gonna say for V2, this is gonna be solution stuff, solution in app, because you're right, the whole off thing blows up, and so solution in app, and then this is gonna be. Auth, new.

speaker2：[00:29:12 - 00:29:18]

And then I'm also going to say APIs, question, don't know. If they don't support it, don't support it.

speaker2：[00:29:18 - 00:29:22]

But I think it's important for us to box it this way, because this is a bunch of crap we can't control.

speaker1：[00:29:22 - 00:29:31]

Yeah, that's all, we'll figure it out, you know, that's shiny stuff. I mean, meanwhile, you have home health at risk of non-compliance with our own WellSky corporate, you know, like requirements, so whatever.

speaker1：[00:29:31 - 00:29:39]

So with that, yeah, so and that's kind of, I mean, that V1, I'm sure we can add to the list, but that's what I have in mind.

speaker2：[00:29:39 - 00:29:57]

So here's what else I got. So then I think that we got to design, basically the, I like the word dialogue flow a lot better than agent studio, because I want to say design agent studio, which grammatically doesn't make sense to me.

speaker2：[00:29:57 - 00:30:04]

So I'm going to say design flow using agent studio. And I think that is very much your key.

speaker2：[00:30:04 - 00:30:10]

Like you guys take the training, you do that. And so then we do that.

speaker2：[00:30:10 - 00:30:14]

Is there any form? There's no real form of migration.

speaker2：[00:30:15 - 00:30:20]

The only thing is the existing knowledge we bring over, but that's not a migration.

speaker1：[00:30:20 - 00:30:27]

I mean, my hope is the migration is cooked into the actual design, meaning.

speaker1：[00:30:27 - 00:30:39]

Kind of what I mentioned last week where I was like, best case scenario, we can take a BLOB file of our existing agent and put it in there with extra requirements around chat, and that would be a migration in my brain. That's what I thought too.

speaker1：[00:30:39 - 00:30:47]

It's a moot point whether we call it a migration or a design, and honestly, for the sake of... I'm presenting to Chris, I prefer design, because I do.

speaker1：[00:30:47 - 00:30:49]

Migration insinuates faster.

speaker2：[00:30:49 - 00:30:52]

Well, and I also think like there's really, we aren't truly migrating.

speaker1：[00:30:52 - 00:30:52]

Yeah, that's true.

speaker2：[00:30:52 - 00:30:54]

It's the same cases, it's the same knowledge, we're just attaching.

speaker1：[00:30:54 - 00:30:59]

Yeah, and in fact, they never, Google never offered us any kind of migration, formal migration pathway.

speaker2：[00:30:59 - 00:31:01]

So that's right.

speaker1：[00:31:01 - 00:31:06]

So really, we can't say migrate anyway, we're still designing. So okay, and all right, keep going, keep going.

speaker2：[00:31:06 - 00:31:14]

Okay, so then, okay, so now if these things are done, we're saying that we made, I'm gonna also say no change to CRC.

speaker2：[00:31:15 - 00:31:20]

No change to implying it is the CRC today, and we're whacking chat.

speaker1：[00:31:20 - 00:31:23]

We're just embedding a URL in there using some, yeah.

speaker2：[00:31:23 - 00:31:33]

So then if we're saying that we're doing training right now to figure this out, Vivek owns the authentication. owns any Salesforce integration.

speaker2：[00:31:34 - 00:31:49]

So then really the thing is if you design this and Tommy Knuckles, Vivek and the whole team own that, then I think at that point we're living in a world where it is going out the door.

speaker1：[00:31:49 - 00:32:22]

Yeah, I would agree with that. Yeah, and I would think that some of the, I mean the GCP bucket stuff, with the assumption that we're utilizing the same architecture and fetching and a lot of stuff that we have today, It comes back to my team a little bit too. So it's kind of a, that's a shared responsibility, meaning, and again, unanswered questions will get answers to like the CX Agent Studio need us to establish an API key to it, or is it going to utilize the existing API keys that we have at a cloud level, or you know, at a GCP cloud level, you know, stuff like, but that's all just, that's design stuff we'll walk through.

speaker2：[00:32:22 - 00:32:27]

So then here's what I'd like to do on this design flow.

speaker2：[00:32:28 - 00:32:34]

Because what I think we need to do is also take a look at what we know from what we've past experience.

speaker2：[00:32:34 - 00:32:51]

So I think this design requirements needs to be, I'm gonna say ability to customize per solution. Now, I don't know what that means.

speaker2：[00:32:52 - 00:33:05]

But I think as you go through this and we get the training and stuff, I think I want to be able to throw that there so that they've got, kind of like put it on a net in Corbin and say, give you line of sight. I'd like to be able to do that.

speaker1：[00:33:05 - 00:33:11]

That'll be an interesting one. And I, this is something because you mentioned it a couple times and it's very reasonable to include.

speaker1：[00:33:11 - 00:33:23]

What I think is really interesting is I am still waiting for a compelling use case that says, We need to customize further than what the standard front door that we have today.

speaker1：[00:33:23 - 00:33:30]

The 2 that I have today are Steve thinking a customized question will increase engagement and increase bypass.

speaker1：[00:33:30 - 00:33:37]

And then Jackie Dennon coming out of the woodwork saying we need to call out the solution when they call it in, which I still don't understand why she's so obsessed with it.

speaker2：[00:33:37 - 00:33:38]

Say that last one again.

speaker1：[00:33:38 - 00:33:52]

Jackie Dennon, she's lead over hospice. She's convinced that clients are getting confused when they call because we don't, they don't, they're essentially getting amnesia. So they call home health and they forget what WellSky solution they're calling, it doesn't make sense and I shouldn't even mention it.

speaker1：[00:33:52 - 00:33:54]

Like basically I'm not even entertaining that one.

speaker2：[00:33:54 - 00:33:55]

Yeah, I agree.

speaker1：[00:33:56 - 00:34:16]

And even the Steve one, I'm kind of like, for as much as we've dragged out people saying, are being, for lack of a better term, anti-AI engagement, bypassing, da-da-da, I don't know how much juice there is out of a, we can customize the question and change it every other week to your heart's content. balancing that with the work it takes to change it every week kind of thing.

speaker1：[00:34:16 - 00:34:24]

So all that said is I would love to brainstorm more to find a really much more compelling reason. Is there anything?

speaker2：[00:34:24 - 00:34:35]

So let's just talk through, those are great questions. And I think, so then let me tell you what I think, because this is very much like very healthy conversation between us to get aligned, because I don't want to spout crap that doesn't value.

speaker2：[00:34:36 - 00:34:42]

But I also know that Chris, and he's creating frustration with the support leaders where he's like, what's your AI strategy? What's your AI strategy?

speaker2：[00:34:42 - 00:34:45]

And it's like, to be honest, and especially on this one, they don't have any levers to pull.

speaker1：[00:34:45 - 00:34:51]

They feel like their hands are tied. I guess, and this is where it gets, yeah, and that goes back to like, great, lean on them.

speaker1：[00:34:52 - 00:34:56]

And I think you're right. I think we say we need the ability to customize on a per solution basis.

speaker1：[00:34:56 - 00:35:01]

What does that mean? We're not sure yet, but know that, and I know architecturally, I know how it happens.

speaker1：[00:35:01 - 00:35:18]

It's call solution, use solution, call to go do different things. I mean, that's Just like what we're doing today, where we come in, they call home health, we pull based on the essential metadata of what they had, that we can say, all right, this solution is home health. We create a case with home health and we use the home health data store for it.

speaker1：[00:35:19 - 00:35:33]

So we can use that architecture to do it, but I want to, and so I'm happy, frankly, I think we've already committed to doing this because we're calling only the solutions documentation already, but customizing further, I just.

speaker2：[00:35:35 - 00:35:39]

So here's what I think, because I agree with you. I think it needs to be not vague.

speaker1：[00:35:39 - 00:35:42]

Yeah, it needs to be not. Well, and I think it can be vague now.

speaker1：[00:35:42 - 00:35:46]

Well, I'll tell you what I want. Yeah, okay, yeah, please.

speaker2：[00:35:46 - 00:35:56]

Because I think what I want is I think that we need to have a knowledge, I'll say source, trying to be generic, that's specific to a use case.

speaker2：[00:35:57 - 00:36:03]

Because that means that then when they have a nuanced thing that they're getting a ton of calls about, To me, I go back to EVV.

speaker1：[00:36:03 - 00:36:07]

Okay, I was about to say, is this like an EVV scenario? It's like EVV, like subsetting into it.

speaker2：[00:36:07 - 00:36:11]

Once Steve said it, I've got four people talking to me about a version of it. Okay.

speaker2：[00:36:11 - 00:36:20]

And so I think that would, and I'll even put EVV here, but really that's basically saying like we now have data, we have knowledge coming in that's not necessarily formally technical.

speaker1：[00:36:20 - 00:36:23]

I see. So we're like sub-categorizing inside, but okay, I'm done with that.

speaker1：[00:36:23 - 00:36:34]

Which actually, when we go back to the knowledge structure and a lot of what we're discussing with metadata tagging and all that good stuff, we're kind of. Kind of already getting there, once we have a proper knowledge.

speaker2：[00:36:35 - 00:36:44]

And I think as long as I wanna frame it generically, because it might actually be that it's not truly a unique flow. Yeah, if we can deliver this functionality, right.

speaker1：[00:36:44 - 00:36:52]

It starts to feel like a knowledge 2.0 a little bit there, where it's like we're already going to be doing this because when we're able to...

speaker1：[00:36:53 - 00:37:02]

deploy our knowledge in a way that is actually a little bit more adherent to the architecture that we want. It's gonna happen naturally anyway, but I'm still with you.

speaker1：[00:37:02 - 00:37:20]

We need the ability to customize per solution. I think maybe what I was saying is just to reframe it a little bit is I understand the solution, like the leaders are getting hammered, but if the best thing you can come up with is tell me what solution you're calling or let me customize a question, I somewhat like, you're not.

speaker1：[00:37:21 - 00:37:22]

Digging very deep. No, you're not.

speaker1：[00:37:22 - 00:37:26]

And so I think that's right. So I need to get past that and just I'm past that now.

speaker1：[00:37:26 - 00:37:29]

I'm totally with you now. We're saying we are customizing per solution.

speaker1：[00:37:29 - 00:37:36]

We will make it cooler, but that doesn't mean that we're going to necessarily go and tweak the knobs every time they want to call something.

speaker2：[00:37:36 - 00:37:42]

I think if I can, if we, I guess what I'm kind of saying is we can fulfill a nuanced knowledge source.

speaker2：[00:37:43 - 00:37:53]

An API integration to a flow that's specific to the solution, and then I do wanna just allow them to make whatever work changes they want, because that shows ownership.

speaker2：[00:37:54 - 00:38:04]

Sure, so for me, I feel like that's, but I think here's my thing on this whole little bubble: you guys come back and tell me if that's okay. Yeah, if you gotta push back on it, it's totally to me.

speaker1：[00:38:04 - 00:38:12]

I think it's the 1.5 to adjust it at my just first glance, 'cause it's like we can do all this and if we use existing knowledge architecture.

speaker1：[00:38:13 - 00:38:30]

I feel like that's going to feel easy to Corbin and Annette to say, Hey, we got the existing knowledge architecture here all you gotta do is go yank out the same  you have, we just present it in a more chat-friendly format, which means we can go detail, we can give links, da da da da da. I think they're gonna feel really good about getting out the gates with that, and then...

speaker1：[00:38:31 - 00:38:52]

fast follow with doing this, but at the same time, I think it might be worth leaning in with Jason a little bit to say, all right, what does, as we're having these parallel conversations with redoing knowledge and everything and adding in metadata tagging and doing all these essentially cool things, I don't wanna build a bunch of custom stuff that we're eventually gonna have to explode here, and maybe we should, I don't know.

speaker2：[00:38:52 - 00:38:59]

Well, I think this is actually, we put to Tommy Knuckles. Okay, sure, and say, we've done the training.

speaker2：[00:39:00 - 00:39:04]

These are the nuances of how we want the architecture.

speaker2：[00:39:04 - 00:39:12]

So then when he comes back to me, the way that this would land in my head is we all go take training. We all say, hey, Tommy, here's what we want.

speaker2：[00:39:12 - 00:39:20]

And it's just basically saying we want chat and knowledge. And then in there, it's like, hey, Tommy, we need you to support these use cases.

speaker2：[00:39:20 - 00:39:24]

How would you do it? And then he's going to tell us, and then we go back, react.

speaker2：[00:39:24 - 00:39:27]

And that's when you guys push back, move this around.

speaker1：[00:39:27 - 00:39:40]

Okay, I'm with you too, because he may say, just use our knowledge product, or he may say, as long as you have something with metadata, which is what we already know, and we say, okay, cool, when that's done, then we know we can re-swizzle this and keep going.

speaker2：[00:39:40 - 00:39:59]

I should write to, I'm just going to write a thing for Tommy to basically, I need to make sure, I'm just going to say clarify go live function, because I want to make sure that he understands for instance, we're using the existing GCP bucket.

speaker2：[00:39:59 - 00:40:05]

He's seen a lot of variations. And so I actually, this is, I think what I'm gonna do is I'll give him a design doc going into it.

speaker2：[00:40:06 - 00:40:19]

These are the conditions we've got, which is sort of this. Okay, so then I think if we go there, then we've got, so then the nuance would be we'll commit to chat, I'll get an e-mail out, or commit to training to be done, and that'll do Tommy.

speaker2：[00:40:19 - 00:40:30]

So then that moves this whole thing forward. And then So then the action items we got here are... I mean, this thing's going to ruin the dang whiteboard.

speaker1：[00:40:30 - 00:40:32]

It feels like you got it clean.

speaker2：[00:40:32 - 00:40:39]

I feel like it's not. I'm like, at this point, I'm almost ready to just slide it somewhere, leave it, and just write on the windows.

speaker2：[00:40:39 - 00:40:42]

Or go find a new whiteboard. Dude, I know.

speaker2：[00:40:42 - 00:40:48]

It's the only thing. Okay, so we've got Tommy training.

speaker1：[00:40:48 - 00:40:53]

It's not a whiteboard while I. So, we got Tommy.

speaker2：[00:40:53 - 00:41:08]

Training, we got Google training, we need to talk to Katie for that, we need to talk to Vivek, which really I almost say after Tommy.

speaker1：[00:41:08 - 00:41:09]

Yeah, I think so.

speaker2：[00:41:09 - 00:41:22]

Yeah, after Tommy, and so if we have all that rolling, so then I think then the question would be... So then how do we want to communicate to Chris?

speaker2：[00:41:23 - 00:41:30]

Because of course, Chris is going to say, I want to know when chat is done. And this is personal care only, which I still agree with.

speaker2：[00:41:30 - 00:41:44]

I think that's the right way to do it. But what I think we want to do is say, when we land here and say we're done with this, then I think you'll have run off for a week or whatever, land this.

speaker2：[00:41:44 - 00:41:53]

And then you're going to say, we're going to say personal care, you know, live or done or whatever we want to say on a date.

speaker2：[00:41:54 - 00:41:58]

And then we're also going to say ETA for other solutions.

speaker2：[00:41:59 - 00:42:03]

We'll have an estimate at this time too because we'll base it off person.

speaker1：[00:42:04 - 00:42:24]

It'll be really interesting too for the ETA for other solutions in terms of how, I mean it was a material effort. The long pull in the tent of every implementation was building out the virtual agents that could have the new solution. So that was also one thing that I didn't lean in too much on.

speaker1：[00:42:24 - 00:42:28]

And in fact, I thought it should have been easier than it was. So it'll be interesting to see if this is easier than it was.

speaker1：[00:42:28 - 00:42:40]

So that'll be really interesting to see. The other thing that shouldn't go on the whiteboard that we should think about is for CRCs that are not well adopted.

speaker1：[00:42:43 - 00:42:48]

So I'm thinking, and this is so tough. Two biggest client bases, Home Health and Connected Network.

speaker1：[00:42:48 - 00:42:54]

Let's take Connected Networks off. Home Health, they get less than 50 logins per month.

speaker1：[00:42:54 - 00:42:58]

They've got thousands upon thousands of users. That's Shelby's fault, as far as I'm concerned.

speaker1：[00:42:58 - 00:43:04]

I mean, sure, use SSO as a bludgeon. do we, I mean, first of all, they're at the way back of the line.

speaker1：[00:43:05 - 00:43:13]

We use it as a reason to get in to CRC, or for them to push to CRC, but this is where we start to say, all right, does aging and disability really need one?

speaker1：[00:43:13 - 00:43:24]

So I guess having a secondary conversation around, or do we design it in such a way that as long as there's knowledge, we can deploy it there because we don't care and all we're doing is just generating an embed URL that fetches?

speaker2：[00:43:24 - 00:43:31]

That's my sense, because here's how I think I would look at it from Chris's endpoint. Because he knows that too.

speaker2：[00:43:31 - 00:43:43]

And really what we've got right now are we're staffing because we're obligated to with humans because we have no other options. This is now a new option, which is a unmanned support layer.

speaker2：[00:43:43 - 00:43:48]

So that's highly appealing to Chris. So I think we need one per.

speaker2：[00:43:48 - 00:43:55]

But I also think that at some point, let's just write comms or marketing. Because you're exactly right.

speaker2：[00:43:58 - 00:44:06]

if it's not being used, let's, you and I are so busy, we don't need to do stuff that doesn't matter.

speaker1：[00:44:06 - 00:44:26]

Yeah, well, and maybe there is a level of effort that's much lower than that, and I just need to, it's one of the, that's an unknown that I'd like to make known is once we get this damn thing built out, how easy it is it to, all right, CX Agent Studio, where I can have a contextual conversation with AI Coding AI, I want to add in a new solution, go do it. And maybe it is, maybe it's just.

speaker1：[00:44:27 - 00:44:34]

Do everything you just did, only do it for this. The other thing that's an interesting architectural challenge is CRCs are solution specific.

speaker1：[00:44:35 - 00:44:48]

So you log into personal care, you get personal care. We will, and this is just a problem to solve, I am assuming we only want to deliver a personal care answer from within personal care chatbot.

speaker2：[00:44:49 - 00:44:50]

Yes.

speaker1：[00:44:50 - 00:44:51]

Yeah. Okay.

speaker1：[00:44:51 - 00:44:57]

Because in my head, I'm like, well, if they're, for example, personal care and home health, and they say, well, I'm at it, I got a home health question.

speaker2：[00:44:57 - 00:45:08]

I like where your head's at, but I think that for that to not be confusing, our clients have to see that we operate that way and we don't today.

speaker1：[00:45:08 - 00:45:20]

Okay, yeah, that's true. And in fact, maybe the get out of jail free card on that is everybody gets a knowledge article, if you're in chat, everybody gets a knowledge article that says, if asked a question about That's right.

speaker2：[00:45:21 - 00:45:25]

That's exactly what it is. We need a little skill that'll link them to the other.

speaker1：[00:45:25 - 00:45:30]

And that shouldn't be that shouldn't be hard. That's honestly, that's frankly, that's an article.

speaker1：[00:45:30 - 00:45:36]

That's a if they ask for a home health, if they ask a home health question and they're in personal care, then so.

speaker2：[00:45:37 - 00:45:38]

Yeah, I agree.

speaker1：[00:45:38 - 00:45:46]

So then the other thing that I think is worth talking about here is We're done with all this, and this is like that.

speaker2：[00:45:46 - 00:45:47]

I'm gonna write directory skill.

speaker1：[00:45:47 - 00:45:48]

Yeah, okay, perfect.

speaker2：[00:45:48 - 00:45:48]

Chat directory skill.

speaker1：[00:45:49 - 00:45:59]

This is, blessedly not my responsibility, defining containment in chat. What do we define as a win in chat?

speaker1：[00:46:00 - 00:46:01]

Is it every chat? That's a great question.

speaker1：[00:46:01 - 00:46:05]

How many? So, and it's I think it's a McCall Bree thing.

speaker2：[00:46:05 - 00:46:08]

It is, but it's a thing on here.

speaker1：[00:46:08 - 00:46:12]

It's a per chat count, per web case submission count.

speaker2：[00:46:13 - 00:46:18]

I'll say chat containment, and I'm gonna say define metric.

speaker1：[00:46:18 - 00:46:31]

Yeah, and lucky for me, the only thing I gotta do is just feed them some information, or Corbin and Gage Riker, feed them information about what we're passing on so they can go get it.

speaker2：[00:46:31 - 00:46:34]

I agree. But I agree, this is no call.

speaker2：[00:46:35 - 00:46:42]

And I also wrote Ops Impact because of the we blew up the Salesforce list. And I would just wanna make sure that that's all him.

speaker1：[00:46:43 - 00:46:46]

So then, okay, so then this is getting...

speaker2：[00:46:46 - 00:46:48]

No, this is what we need to do.

speaker1：[00:46:48 - 00:46:59]

Well, this is 100% interesting. So the CCAI module of it, there is a chat functionality in there which we, I am curious, and this is a Tommy question too a little bit.

speaker1：[00:47:01 - 00:47:09]

If we're not putting a human behind the chat, then do we even set up CCAI for chat? I don't know.

speaker2：[00:47:09 - 00:47:10]

I don't know.

speaker1：[00:47:11 - 00:47:20]

 where it's zero hours of staffing just so we can have the capability to log a case or can we circumvent that utilize I think that's an API key question.

speaker1：[00:47:20 - 00:47:24]

That's an ugly question too, because what's gonna happen?

speaker2：[00:47:24 - 00:47:26]

Is, should I write that down?

speaker1：[00:47:26 - 00:47:42]

It's like Tommy questions. That's a big Tommy question, yeah, because what's gonna happen is their data, their reporting is so terrible that we're logging in case every time a call comes in and it's created a bunch of terrible data.

speaker1：[00:47:43 - 00:47:51]

a big burden of data for us on the Salesforce side. So if the insinuation is the only way for us to tell what the hell happened in a chat is to...

speaker2：[00:47:51 - 00:47:53]

Because we're basically saying, does it go in Gemini CX?

speaker1：[00:47:53 - 00:47:54]

Yes, correct.

speaker2：[00:47:54 - 00:47:57]

I agree, I agree. Which is weird to write, but I know what you mean.

speaker1：[00:47:57 - 00:48:06]

Yeah, like, so we're gonna have a case per chat just so that... So assume out of every 10 chats that take place, you get 3 cases.

speaker1：[00:48:07 - 00:48:14]

Are we actually gonna have 10 cases, but we gotta go figure out a way to make three of them legit and the other seven are just going in the crash? I'm hoping not, 'cuz I'd like to not do that.

speaker1：[00:48:14 - 00:48:19]

In fact, I don't love right now how many cases we're logging and just killing.

speaker2：[00:48:19 - 00:48:25]

We should, is this gonna cover it? No human, no human too, or do you think we need to add some more detail?

speaker1：[00:48:25 - 00:48:33]

I think that's fine, as long as we remember the context of it, which is how do we make sure we're getting cases logged and get good data out of that, because I think there's also we need.

speaker2：[00:48:34 - 00:48:35]

To, can't bend over the book.

speaker1：[00:48:35 - 00:48:41]

I know, it's getting to get up. I know, I'm glad my back feels pretty good after because I played keeper the whole time yesterday too, so nice.

speaker2：[00:48:41 - 00:48:43]

All right, I'm gonna write good cases. Good cases.

speaker1：[00:48:43 - 00:48:45]

Good cases only, exactly.

speaker2：[00:48:45 - 00:48:47]

Good cases only. Okay.

speaker2：[00:48:48 - 00:48:51]

No, this is good. This is 100% what I wanted to do, because there's just so many angles to it.

speaker1：[00:48:51 - 00:49:01]

Yeah, and I mean, and that's the thing is we're gonna have, since we came up with all this without even taking the damn training, which means this is probably gonna double in size by the time we get through the training. So I think it's a good start.

speaker2：[00:49:02 - 00:49:12]

It 100% is, because I think, because I mean, to be honest, we're gonna get through the training, we're gonna have Tommy, and then we're gonna have the Google training, and I totally agree. We're probably going to need to come back around on this.

speaker1：[00:49:12 - 00:49:14]

Yeah, Oh, God, yes.

speaker2：[00:49:14 - 00:49:20]

Because, but that's okay, because here's our date for Chris. We get through all of this first.

speaker2：[00:49:21 - 00:49:30]

So I think this is kind of you and I have the scaffolding of a plan, people are moving forward, but we're also not ahead of our skis making commitments we can't do.

speaker1：[00:49:30 - 00:49:43]

Absolutely. And to the point where like, I am not going to ask my team to commit to a date until probably I mean, I think we have to get through almost all this. Maybe we don't, yeah, that we need to as well because we have to have them.

speaker2：[00:49:43 - 00:49:58]

Yeah, I mean, well, because your team really, if we get through the Tommy training, the Google training, and then they took the online training, if that's all done, which is in about two weeks since, we're going to be close. And then I'll get the meeting scheduled with Katie and Brad.

speaker2：[00:49:58 - 00:50:07]

Oh, by the way, I need to talk to you about why I wrote Brad. then I think that's when we, that's when we're like, okay, now we need some dates.

speaker2：[00:50:07 - 00:50:08]

So I think that's fine.

speaker1：[00:50:08 - 00:50:13]

I think that, and then I go back, and it's funny too, because that's also a net return.

speaker1：[00:50:13 - 00:50:21]

So I'll have to be a little bit tactical with her, so I'm not just hammering her the moment she gets back, because she's going to, we'll get her through the training, I'll catch her up. I'm not worried about it.

speaker1：[00:50:21 - 00:50:24]

More from an emotional management standpoint than an actual development standpoint.

speaker2：[00:50:24 - 00:50:29]

But can we do her a solid? Because the other thing is I'm out of week 2.

speaker2：[00:50:29 - 00:50:33]

So when she returns, I love it.

speaker2：[00:50:33 - 00:50:44]

And then it's like, because to be honest, like she's the lead. And I want her to feel comfortable.

speaker2：[00:50:44 - 00:50:45]

And it's like this.

speaker1：[00:50:45 - 00:50:47]

That's a good grace. That's a good grace.

speaker1：[00:50:47 - 00:50:51]

She'll have her own set of questions and it'll be a bunch of  that we didn't even think of because she's, you know.

speaker2：[00:50:51 - 00:50:53]

Yeah, and I don't want her reacting in the rear.

speaker1：[00:50:53 - 00:50:53]

Exactly, yeah.

speaker2：[00:50:54 - 00:50:59]

So the problem is, so then that means we'll have the Tommy training while she's out.

speaker2：[00:51:01 - 00:51:05]

But we will not do any of this until I am back and she's had a week.

speaker1：[00:51:05 - 00:51:24]

And if Chris absolutely must have a date, we can tell him, whatever, the 19th, which is the Monday after you're back, that you and I can come together and sometime, 19th or 20th, maybe the 21st is the latest, we will come back to him with an estimated go-live date based on all the information. That's right.

speaker1：[00:51:25 - 00:51:30]

We could commit to giving a go live date 3 weeks from today at the absolute earliest.

speaker1：[00:51:30 - 00:51:35]

And I would even, I mean, I would love to not do that.

speaker2：[00:51:35 - 00:51:39]

But it feels tight. Let's put it on a, let's throw it on a calendar and see how it looks.

speaker1：[00:51:39 - 00:51:39]

Yeah. Okay.

speaker1：[00:51:39 - 00:51:40]

That's, yeah.

speaker2：[00:51:40 - 00:51:48]

But I really like, I really like this point. Cause I mean, the thing is, like we're by us doing this now, we're proactively managing Chris rather than we're like, hey, we're working.

speaker2：[00:51:48 - 00:51:50]

And then he gets all anxious.

speaker1：[00:51:50 - 00:51:54]

Yeah, he wants, he just wants, yeah, give him something to look at. I just, yeah, that is the.

speaker1：[00:51:56 - 00:52:01]

That'll give her, that'll be a week. And that way I can start with, can you get through this for me?

speaker1：[00:52:01 - 00:52:03]

I'll run interference on all the other stuff.

speaker2：[00:52:04 - 00:52:10]

So then, okay, so my notes on the critical path, I said the, let's see, June 11th or 12th has taught me.

speaker2：[00:52:11 - 00:52:18]

So then we're saying here that I'm out the 15th, that's the 19th.

speaker1：[00:52:18 - 00:52:22]

So here's the calendar. So we're committing to.

speaker2：[00:52:22 - 00:52:26]

Because we're saying training's here. Annette is caught up here.

speaker2：[00:52:27 - 00:52:35]

So we will make a commitment here. So then I'm going to say, so then without me being, I think it's okay.

speaker2：[00:52:35 - 00:52:48]

So if we're saying the week of 615 is Annette gets all caught back up, And then you guys start to work through the scoping.

speaker1：[00:52:48 - 00:53:03]

22nd, 23rd, 24, or like we're, and really we're scoping towards the end of 18-19 too, where I'm putting together a call with me, Corbin, Annette, you know, with just my team and say, hey, all right, we got it, you know, and some, you know, we know all we can know about this, we gotta go tell them.

speaker2：[00:53:03 - 00:53:12]

So then I'll say 619, I'm gonna say internal deadline, and I'm putting in parentheses, not to Chris.

speaker2：[00:53:13 - 00:53:21]

I'm going to say your team has high level, you know what I mean, LOG.

speaker2：[00:53:22 - 00:53:29]

So then I'll say when I get back, so let's say the 23rd, 623.

speaker2：[00:53:29 - 00:53:35]

So I just didn't put on a Monday, because I'm going to say Ryan is back, review plan with Michael.

speaker2：[00:53:35 - 00:53:40]

So then we're saying that I'm going to tell Chris by 626.

speaker2：[00:53:44 - 00:53:53]

We will have a timeline for chat for personal care.

speaker2：[00:53:54 - 00:54:01]

And I'll say estimate for the remaining solutions.

speaker2：[00:54:03 - 00:54:09]

I'll say under the assumption, personal care estimate turns out to be true. Kind of saying like, you know what I mean?

speaker1：[00:54:09 - 00:54:24]

And that's one where like you don't want to It's so tough because you don't want Chris to have to ask for where are we at, what can I expect, but also, yeah, so that's at the very least that will allow you to say, let's look at this because I'm...

speaker1：[00:54:25 - 00:54:27]

I'm kind of glad. I'm hoping this isn't the case.

speaker1：[00:54:27 - 00:54:31]

We'll see. I'm glad he's not saying I want it day one, fiscal year 27.

speaker1：[00:54:31 - 00:54:32]

So hopefully that doesn't.

speaker2：[00:54:32 - 00:54:34]

Oh, he's trying. And I'm telling you, but that's on me.

speaker2：[00:54:35 - 00:54:41]

Like, I feel like when he does crap like that, I don't even want you to give that head space. Yeah, because that's him being way too aggressive.

speaker1：[00:54:42 - 00:54:45]

Well, and it goes back to the Josh and Jade thing to be like, damn, why'd you do that?

speaker2：[00:54:46 - 00:54:53]

And so like he is, but I got that. So then my thought is just saying, I'll just put this in the notes.

speaker2：[00:54:53 - 00:54:59]

I'll say No, I want to put this in those optics.

speaker2：[00:55:01 - 00:55:12]

If the week I'm out and you guys are estimating and stuff, I will probably imply to Chris that work air quotes has begun. We're learning it.

speaker2：[00:55:13 - 00:55:18]

But my point is, hands are on keyboard we just haven't put dates to it, yeah, so sort of like work started.

speaker1：[00:55:19 - 00:55:28]

Don't think we're, and you could literally, I think, if you wanna, or this is just me kinda suggesting it softly, but you could even set the stage with, literally, you have to turn the lights on first.

speaker1：[00:55:28 - 00:55:32]

I mean, that's step one is go enable CX Agent Studio, which I never did in that.

speaker1：[00:55:34 - 00:55:43]

I was supposed to a screenshot about weeks ago, it was like the day after Google Next, because I was looking at stuff and I was like, look at that. And then, but then I slowly backed away.

speaker1：[00:55:43 - 00:55:50]

So I guess just insinuating that like the door is closed to the room that we need to go in and we haven't even entered it yet. That's right.

speaker1：[00:55:50 - 00:55:52]

This is all the stuff we're doing outside before we enter the door.

speaker2：[00:55:52 - 00:55:53]

That's right. We're preparing to open.

speaker1：[00:55:53 - 00:55:55]

Maybe breach the door would be a better term at this point.

speaker2：[00:55:55 - 00:55:59]

So, well, and it's and yeah, so I think this is good.

speaker2：[00:56:00 - 00:56:15]

I'll say there's gonna be so many versions of this that I almost, like in my head, like, I mean, we got chat version one, we're aligned on. Chat version two, also something.

speaker2：[00:56:15 - 00:56:23]

I don't know if this is chat version 2.5 or three or somewhere in the middle, but we also have, do we put the knowledge graph in at some point? I do not know.

speaker2：[00:56:24 - 00:56:29]

that is technically part of the critical path, but it's like, why jack with it? Just we got to do this first.

speaker2：[00:56:30 - 00:56:39]

And I think the thing is, when we have the Vivec meetings, if he wants to start to do those things with a beer up, great, but it's off of you.

speaker2：[00:56:39 - 00:56:48]

And then I think, and that's where I think just saying out loud, like you do not need to get your arms around all this. I want Jared to take that crap.

speaker1：[00:56:48 - 00:56:49]

Okay.

speaker2：[00:56:49 - 00:57:00]

Right. So like any of a beer up stuff, Vivek making commitments, Katie stuff, like 100% like just get that to Jared and just be like, I just need you to bird dog dates.

speaker2：[00:57:00 - 00:57:01]

Okay. Like, you know what I mean?

speaker2：[00:57:02 - 00:57:07]

It's just he's I just I need him to be the PM. So then you and I aren't.

speaker1：[00:57:07 - 00:57:13]

Do I need to bring him into the omnichannel project and let him kind of take some of this?

speaker2：[00:57:13 - 00:57:18]

I'm totally okay with that if you are. I think for me, it's me just being clear with you.

speaker2：[00:57:18 - 00:57:24]

I need it done by the date, but I think very much empowering you to do any way you want. Heck yeah, use Jared.

speaker1：[00:57:24 - 00:57:29]

Yeah, I'm kind of like, I don't think I necessarily need him yet, but what I need is, I mean... Our wild card here is Molly.

speaker1：[00:57:29 - 00:57:37]

I mean, Molly needs to provide the information to Annette and Corbin so that they can rebuild our 855 WellSky system.

speaker1：[00:57:37 - 00:57:46]

And once that's rebuilt to the spec that we need, but that also, I don't know, there is a shitload of work going into that. And so there is that along with this that we need to do.

speaker2：[00:57:46 - 00:57:53]

Do you want you and I to sit through and do this for Amazon Connect? Or do you want to take it, run with it?

speaker2：[00:57:53 - 00:58:21]

Because I do think I'll say out loud. I think having something like this that rolls into a critical path and having some meetings with Molly, getting commitments, putting them on a spreadsheet, because what I will feel better if we have basically 2 critical paths and who's doing what, because I don't want to, I don't, what scares me is like, oh, whoops, Annette ends up not being able to have the 4th of July because she has double commitments.

speaker1：[00:58:23 - 00:58:27]

I mean, I don't think you and I shouldn't have to do this. You or you shouldn't have to do that.

speaker1：[00:58:27 - 00:58:35]

Let me do a version of that myself and or with Jared. I mean, it's mostly all up here anyway and written down in the epic anyway.

speaker1：[00:58:35 - 00:58:39]

Like it's all there, but actually defining dates, that's where it gets a little hanky.

speaker1：[00:58:40 - 00:58:49]

And there's, I mean, there's stuff that we can then go back and say, Katie and Molly, you this is on you for missing that.

speaker2：[00:58:50 - 00:58:53]

That's what I exactly. That's 100% what I want.

speaker1：[00:58:53 - 00:58:59]

Which we have, we've got their cases logged to do the shift that they need to do, like the deprecation of the phone numbers.

speaker1：[00:58:59 - 00:59:11]

But there are some, there's some things that we're waiting, like for example, the mapping out of the existing 855 WellSky Tree that also includes dumping some people to voice mails and things like that, which we can still do, but we need to know that it needs to be done.

speaker2：[00:59:11 - 00:59:17]

'Cause 100%, I think that we're gonna have enough work going in different directions. I think we should get it all on paper.

speaker2：[00:59:18 - 00:59:25]

And 100% on any of our dependencies, because if they don't get it, then it's real clear. So, yeah, I think we're totally like...

speaker1：[00:59:25 - 00:59:27]

I'll probably need to bring in Jared, I think, on that, just to...

speaker2：[00:59:28 - 00:59:34]

Well, and I would just do it so that to me, Jared gets me out of meetings. It's like you understand what needs to come out of this.

speaker2：[00:59:35 - 00:59:40]

So I don't need to be the adult in the room. And Jared's just, I mean, I treat Jared like, here are my key bullet points of the things that have to happen.

speaker2：[00:59:40 - 00:59:44]

He's not technical enough to know what they are, but he'll say it in the meeting and someone's gonna go, oh crap.

speaker1：[00:59:44 - 00:59:45]

Yeah, that's true.

speaker2：[00:59:46 - 00:59:48]

Okay. One thing I forgot to mention here.

speaker2：[00:59:48 - 00:59:48]

I wrote Brad.

speaker1：[00:59:48 - 00:59:49]

Yeah, okay.

speaker2：[00:59:49 - 00:59:54]

Brad is telling me he wants to consolidate the CRCs from 1 to 25 to 1. Right.

speaker2：[00:59:55 - 00:59:57]

I'm totally cool with that, but I don't have a dog in that.

speaker1：[00:59:57 - 00:59:59]

Yeah, let me know how you're gonna do it. Yeah, boom.

speaker2：[00:59:59 - 01:00:02]

So I'm gonna bring that up. Do not care here.

speaker1：[01:00:02 - 01:00:10]

Yeah, that'll be interesting. Well, and it will, there will be implications though for Chat when they do it.

speaker1：[01:00:10 - 01:00:11]

So, okay.

speaker2：[01:00:12 - 01:00:15]

I think my thing is I need to, I'll get a meeting.

speaker2：[01:00:15 - 01:00:19]

I mean, you're gonna be in the meeting anyway, but I think I'm gonna schedule a meeting with Brad and Katie, you and I.

speaker2：[01:00:20 - 01:00:26]

And you know, I'm gonna continue to drag Jared to anything that might have a timeline impact. And say, here's what we're doing.

speaker2：[01:00:26 - 01:00:30]

By the way, Brad, you said you wanted this. It also might be a good time to just talk about Molly too.

speaker2：[01:00:32 - 01:00:34]

and be like, this is what we're doing, what are you doing?

speaker1：[01:00:36 - 01:00:45]

And frankly, at this point, based on our design, consulting the CRC actually might make our lives harder instead of easier. I mean, it might.

speaker2：[01:00:45 - 01:00:57]

So because we're gonna need, because yes, you're right. And in fact, that's a great point because he's gonna look at authentication generically and we need to know which solution the person is coming into.

speaker2：[01:00:59 - 01:01:02]

we'll talk about it. That's a problem for the future, Michael Ryan.

speaker1：[01:01:02 - 01:01:13]

Yeah, exactly, truly. And frankly, I don't, as much as he'd love to do it and wants to do it, I don't see them having the horsepower to do it anytime soon because we tell him, I mean, they want to do it because they want to do it.

speaker1：[01:01:13 - 01:01:20]

It's not that, I mean, the architecture is already there. The burden isn't, yeah, it sucks having to do something 25 times when you really have to do it.

speaker1：[01:01:20 - 01:01:21]

We don't have to do it that often.

speaker2：[01:01:21 - 01:01:28]

I know it, and I'm also like, I want to get tech writing over to the new data store, which would blow up CRC, right?

speaker1：[01:01:28 - 01:01:32]

Which, and that's kind of where my head's at. Like, why consolidate if we're telling him it's gonna go away anyway?

speaker1：[01:01:32 - 01:01:35]

It just seems like work that probably isn't.

speaker2：[01:01:35 - 01:01:42]

I think he has KPIs around not making Salesforce suck, and he's got a bunch of... What are they?

speaker2：[01:01:42 - 01:01:47]

Library packages? His packages are out of date in the CRC, they're barking at him.

speaker2：[01:01:47 - 01:01:49]

So he just wants them gone or something.

speaker1：[01:01:49 - 01:01:51]

Okay, that's interesting. All right, yeah, let me know as you hear more about it.

speaker1：[01:01:51 - 01:01:54]

I'd be interested to hear what packages they don't like.

speaker2：[01:01:54 - 01:02:00]

That's my assumption, but I think it's more of just the Salesforce liability lies on Brad, and that's how it's trying to create it.

speaker1：[01:02:00 - 01:02:08]

Well, and I think it's easy for them, frankly, I think it's easy for them to point at something they really, you know, they made us build twenty-five of these and it takes a lot of work. I'm like, yeah, it's not that bad actually, especially now.

speaker1：[01:02:08 - 01:02:09]

I mean, all the work's already been done.

speaker2：[01:02:10 - 01:02:11]

Yeah, 'cause I'm fine bleeping it.

speaker1：[01:02:12 - 01:02:22]

If you want to insinuate to Brad that our lives are easier leaving it and that he could just kick that can down the road and say eventually we're getting out of CRC business anyway, that's what I want to do.

speaker2：[01:02:22 - 01:02:22]

I'm good with that.

speaker1：[01:02:22 - 01:02:25]

I mean, he may disagree, which is fine. That's his prerogative and he can tell us that.

speaker2：[01:02:26 - 01:02:29]

I think I totally agree with you. I think the conversation will boil down to dates.

speaker2：[01:02:29 - 01:02:35]

And if Brad has a hard date, he needs to hit, because we do not. We can get chat without our graph database.

speaker2：[01:02:35 - 01:02:35]

Okay.

speaker1：[01:02:36 - 01:02:36]

Cool, man. All right.

speaker2：[01:02:36 - 01:02:42]

Hey, I'll make all the meetings. And I'll send you some notes just to keep us tied together.

speaker1：[01:02:43 - 01:02:49]

I'll see how this thing's going with the other thing, and I'll get going on the omni channel stuff too. All right, go ahead.

speaker1：[01:02:49 - 01:02:56]

And then out for two weeks. It'll be interesting to see, I think Molly's gonna take two weeks off from working on it too, so that'll be interesting.

speaker2：[01:02:57 - 01:02:57]

I agree.

speaker1：[01:02:58 - 01:02:59]

We'll close.

speaker2：[01:02:59 - 01:03:00]

I'll leave it open. Thanks, man.

speaker2：[01:03:00 - 01:03:01]

Appreciate you.