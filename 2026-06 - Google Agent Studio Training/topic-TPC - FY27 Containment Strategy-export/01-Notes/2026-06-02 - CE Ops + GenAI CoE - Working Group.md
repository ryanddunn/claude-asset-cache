---
fileClass: note
type: note
created_date: 2026-06-02T00:00:00.000Z
notes_status: Reviewed
meta:
  - Meeting - Working GenAI CoE + CE Ops
topics:
  - '[[TPC - Agent Beta Program]]'
  - '[[TPC - FY27 Containment Strategy]]'
entities:
  - '[[Vivek Pissay]]'
  - '[[Patrick Herrington]]'
  - '[[05-Entities/Jarrad Weinzerl]]'
---

# My Notes

Gemini ENT - Sharing
* Issue on Google's end


![[Pasted image 20260602103512.png]]


![[Pasted image 20260602104030.png]]

* Maintanence on Agents
	* close out meeting
	* proffer + abhirup

Katie P
* data sources integrated?
* Chris's CS Agent is just using CSV files
* meeting Katie

GraphDB - Meta Data Tuning
* 

Gmeini ENT Sharing Process
* submit REQ
* Gmeini ENT
	* week turn around
	* can use the share feature Gemini ENT
# Transcript

speaker1：[00:00:00 - 00:00:04]

come to you unless it is broken and something has to be fixed.

speaker2：[00:00:04 - 00:00:11]

So I've got staff to take all of that, Patrick. And so this is very timely.

speaker2：[00:00:12 - 00:00:18]

So formally, Michael Proffer owns all of my Gen. AI operations.

speaker2：[00:00:18 - 00:00:29]

So if there is any formal... Like, let's say there's a, let's say that there's a master admin approval workflow or something where we just can't grant anybody access, kind of like system admin type stuff.

speaker2：[00:00:30 - 00:00:40]

That should all fall on Proffered, and he's kind of in general your drop it off and dump any of the maintenance on him.

speaker2：[00:00:41 - 00:00:52]

The other nuance is if there's a technical aspect to this, an integration or something that's fragile or something like that, we should start looping in a beer up.

speaker2：[00:00:53 - 00:01:06]

And a beer up will be our backstop on any dev work so that ideally he hits it and you are his get out of jail free card. But he should be apt enough to do that.

speaker2：[00:01:06 - 00:01:16]

So I think, and then I think, and so Patrick, I kind of think actually, maybe we need to formally close out work on these agents.

speaker2：[00:01:16 - 00:01:24]

And as part of it, in my head, we would do observability because there's got to be, it'll cause big, big heartburn if we can't track what we're doing.

speaker2：[00:01:24 - 00:01:35]

And then any of the, and I think this is honestly kind of you just giving the work back to my team and saying, you know what I mean? Like maybe we just have a closeout meeting with Proffer and a beer up.

speaker2：[00:01:35 - 00:01:37]

And me, you and Jared.

speaker1：[00:01:37 - 00:01:39]

Just a handoff. You guys have a handoff?

speaker2：[00:01:39 - 00:01:39]

Yeah.

speaker1：[00:01:39 - 00:01:42]

That's what I used to do as an architect is handoff.

speaker2：[00:01:42 - 00:01:44]

So let's just do that. Let's just start.

speaker2：[00:01:44 - 00:01:49]

Let's just, and I mean, Jared, would you mind just when they're done, we'll just schedule it. And it does need to be urgent.

speaker2：[00:01:50 - 00:01:57]

But I think it's very healthy, Patrick, because we're putting my people in the seats they're supposed to be. So this is great.

speaker1：[00:01:57 - 00:01:58]

That makes sense. That's awesome.

speaker1：[00:01:58 - 00:02:00]

That's awesome. I like that plan.

speaker1：[00:02:00 - 00:02:00]

Cool.

speaker2：[00:02:01 - 00:02:01]

Awesome. Awesome.

speaker1：[00:02:03 - 00:02:10]

I was getting a little bit stressed about that. I'm like, I'm getting ready to make another two, so now I have seven that I've got to maintain.

speaker1：[00:02:10 - 00:02:10]

How am I going to do that?

speaker2：[00:02:11 - 00:02:19]

You know, I got a dev and then I made promises I'm not going to do black ops IT, so I need some work for them, Patrick. So like, keep them busy, man.

speaker1：[00:02:19 - 00:02:20]

There you go.

speaker2：[00:02:20 - 00:02:26]

Otherwise, they're going to be black ops IT and you're going to get mad at me. Well, cool.

speaker2：[00:02:27 - 00:02:31]

Okay, anything else? I got a couple things, but like I said, nothing major, but just other stuff.

speaker1：[00:02:34 - 00:02:42]

My updates were just the release notes thing seems to be going pretty well.

speaker1：[00:02:42 - 00:02:54]

I'm jumping back on the audits today, finish off their last five requests, and then we'll have three days where they can play with it. Yeah, so we're all good.

speaker2：[00:02:54 - 00:02:56]

I agree. I'm hearing good stuff there too.

speaker2：[00:02:56 - 00:03:01]

Okay, so the two things I got. Vivek, I think the first one's related to you.

speaker2：[00:03:01 - 00:03:09]

Katie Phillips shot me an e-mail and said that she wanted to get aligned on what data sources we're integrating with.

speaker2：[00:03:10 - 00:03:18]

I mean, it's kind of everything, but specifically Chris's client experience agent that you're building, because a lot of the data overlaps.

speaker2：[00:03:18 - 00:03:26]

And I wasn't sure if, I didn't want to throw a meeting on the calendar until I talked to you, but she was asking, and I was like, it does make sense. It's a very similar use case.

speaker2：[00:03:30 - 00:03:31]

You're muted if you're that.

speaker3：[00:03:31 - 00:03:43]

Is a good question, but as of now what I was building with this was like based on the loading like CSV files, right? Like I'm not really bringing any like that was the phase one.

speaker3：[00:03:44 - 00:03:54]

Once I have understanding of the C of those CSV files, that's when we will get into like correcting that directly to BigQuery. Okay, but basically we have an.

speaker3：[00:03:56 - 00:04:08]

We have connectivity to all Salesforce data sets, like the major tables out there. So yeah, I don't know.

speaker3：[00:04:09 - 00:04:17]

It's really on her use case for what is it, what data that she needs. I think we'll have to clarify that and then we can go from there.

speaker2：[00:04:17 - 00:04:19]

Yeah, and Vivek, I'll do this. I got everything I need in that case.

speaker2：[00:04:19 - 00:04:21]

I'll hit her up. I'll schedule a meeting with her.

speaker2：[00:04:21 - 00:04:29]

I'm going to review my strategy and then say that, we're building these data sources. I'll just stay tight with her and she doesn't need to talk to you yet.

speaker2：[00:04:29 - 00:04:32]

It's too early. So once we get some stuff built, I'll follow up.

speaker2：[00:04:33 - 00:04:34]

Cool. Okay.

speaker2：[00:04:34 - 00:04:35]

So that was one. I'm all good with that.

speaker2：[00:04:35 - 00:04:42]

I'll just schedule a meeting with her and just handle it on my own. The other one I've got, Vivek, I threw this on the calendar.

speaker2：[00:04:43 - 00:05:03]

Patrick and Jared, I didn't invite you, but I'm totally cool if you guys want to come. It is the information architecture metadata tuning strategy, so that how do we enrich tech writing content in order to support a graph database for Gen.

speaker2：[00:05:03 - 00:05:03]

AI tuning.

speaker1：[00:05:04 - 00:05:17]

So, yeah, you invited me on that. Sorry, like I said, I already have graph, I mean the whole thing is graph a couple weeks ago whenever my chroma disappeared and I had a, that's what it was, it's the graph messed up.

speaker1：[00:05:19 - 00:05:28]

The security told me my GraphDB wasn't good, so I had to do a different GraphDB. So Graph is all the way through the entire thing.

speaker1：[00:05:28 - 00:05:30]

I don't even know if it would be possible without Graph.

speaker2：[00:05:30 - 00:05:41]

Well, and I think what I want to do, Patrick, is I'm trying to develop a core competency in my team where they enrich the content in a way that is tuned to understand how Graph will react to it.

speaker1：[00:05:42 - 00:05:47]

Yeah, I can definitely help with that. I mean, I have a...

speaker1：[00:05:47 - 00:05:50]

I haven't trained anybody in a while on the graph, but...

speaker2：[00:05:51 - 00:05:56]

We're not going that deep yet. I think what I want to do is just develop an ETL pipeline that can be used.

speaker2：[00:05:56 - 00:06:04]

This is, we are the, this is like the light tech version of the same thing. So anyway, that's on Monday.

speaker2：[00:06:04 - 00:06:09]

I added both of you to it. But basically, I just want to get line of sight from a technical viewpoint.

speaker2：[00:06:10 - 00:06:15]

And then a Birup is in the meeting. He should be able to run with the requirements and wherever we land.

speaker2：[00:06:15 - 00:06:25]

And then that way, what I'm also doing is getting a beer up tight with you two, Vivek and Patrick. So now he's got working context so that, you know what I mean?

speaker2：[00:06:25 - 00:06:28]

Like he doesn't get out in left field. And I think eventually he may need to join this meeting.

speaker2：[00:06:29 - 00:06:30]

But we'll just see how it lands.

speaker1：[00:06:30 - 00:06:32]

OK. Yep, that works.

speaker1：[00:06:33 - 00:06:47]

Yeah, so as far as the graph goes, where I was going with that is originally it took me about nine months to learn the graph, but we're not going that. technical, I think it'll be pretty easy.

speaker1：[00:06:47 - 00:06:52]

It's just a matter of explaining what it does and how it works.

speaker1：[00:06:52 - 00:07:01]

So that way you can think about how it's going to chunk things out, which I can do.

speaker3：[00:07:02 - 00:07:13]

So one thing to remember is like graph is like out of box now with BigQuery. So We might not have to send up any other services.

speaker2：[00:07:14 - 00:07:14]

Right.

speaker3：[00:07:15 - 00:07:21]

So, please remember that and that's what I think the path we should go forward with kind of like the data that we have.

speaker3：[00:07:22 - 00:07:31]

I don't know if it's really worth for us to write like a different services for like optimization and whatnot. So, yeah.

speaker1：[00:07:31 - 00:07:40]

I would agree with that BigQuery. I haven't used it yet in that capacity, but it's supposed to have relational graphs.

speaker3：[00:07:40 - 00:07:49]

Yeah, I saw your protocol, so I think we should just stick to it.

speaker3：[00:07:49 - 00:07:54]

Patrick, we will need the business logic more than anything, and not the technical implementation.

speaker2：[00:07:54 - 00:08:03]

That was what I was gonna say. I wrote a whole document attached to the meeting invite that'll give you a rundown of what I'm trying to do, and it is non-technical.

speaker2：[00:08:03 - 00:08:09]

It's a business ops data flow thing, because I want you guys to define it, but I think the main question I have.

speaker2：[00:08:10 - 00:08:16]

to be clear coming out of that meeting is how do we structure the markdown to support the metadata?

speaker2：[00:08:16 - 00:08:24]

I think we want a YAML front matter type of thing that we would be at the top of the markdown file, but that is in my head, that's your guys' call, not mine.

speaker2：[00:08:25 - 00:08:31]

So I just want you guys to, I'll propose something, but I just want to make sure that you guys are the owners, you're the architects, you know.

speaker1：[00:08:33 - 00:08:41]

Yeah, a non-technical sense of bibliography is always very useful.

speaker2：[00:08:41 - 00:08:48]

Yeah, And there's some nuances in there with legal that are weird, but we'll hit it in the meeting. But anyway, I just wanted you guys to have context.

speaker2：[00:08:48 - 00:08:53]

And it's good for you to just know that like that'll be the beginning of that whole knowledge data pipeline. Okay.

speaker2：[00:08:53 - 00:08:55]

Cool. Okay, that's all right guys, that's everything I got.

speaker1：[00:08:55 - 00:08:58]

Sounds good. All right.

speaker1：[00:09:00 - 00:09:01]

We're going to work on smart.

speaker2：[00:09:01 - 00:09:02]

All right.

speaker4：[00:09:02 - 00:09:07]

Hey, Vivek, did you give that EBB agent to everyone that was on that list earlier?

speaker3：[00:09:08 - 00:09:10]

They should be. They should all have access.

speaker4：[00:09:10 - 00:09:12]

Okay, I'll go talk to Sam and have him.

speaker2：[00:09:12 - 00:09:14]

What is our process for sharing? Did we define one?

speaker4：[00:09:15 - 00:09:15]

No.

speaker2：[00:09:15 - 00:09:19]

So then, Vivek, can I just send a rack through in the meantime, or is there a better way?

speaker3：[00:09:20 - 00:09:28]

So what you need to do is, yeah, let me talk through the process. There are two ways you can do it.

speaker3：[00:09:28 - 00:09:33]

Either like... submit a request position and I can manage it that way.

speaker3：[00:09:33 - 00:09:39]

Or if you go to like Gemini Enterprise, right?

speaker3：[00:09:40 - 00:09:56]

And then, I'll need that, but either ways, but what you can go, so if you go to Gemini Enterprise, and then...

speaker2：[00:09:57 - 00:09:58]

So 3 dots.

speaker3：[00:09:59 - 00:10:05]

So if you go here, or whatever that is, share with the agent, and then you can add.

speaker2：[00:10:07 - 00:10:10]

Okay, and that will work, that will totally work.

speaker1：[00:10:11 - 00:10:15]

Yeah, you have to, if you have to fully type in the e-mail, if it's not out of the go, but that.

speaker3：[00:10:16 - 00:10:28]

Is not it, sure, we are working through that, so you can do that, and then you submit a request to 3ACOE and go approve it in case you need to, with the escalator speak me.

speaker4：[00:10:29 - 00:10:41]

Okay, and if, because I don't want to escalate those all the time, what would be the normal turnaround time on getting like the requests approved to the people that are trying to be shared?

speaker3：[00:10:42 - 00:10:47]

Probably will be okay, unfortunately we are really like lagging behind.

speaker4：[00:10:48 - 00:10:55]

And that's perfectly fine. I just want to be able to give and set expectations, so yeah, cool.

speaker2：[00:10:57 - 00:11:04]

Alright, well hey, I think that's all, like I said, it's no, as long as we're aligned, I'm not worried about timing, so that's fine, Vivek. Cool.

speaker3：[00:11:06 - 00:11:08]

I have like 20 unassigned requests out there.

speaker1：[00:11:10 - 00:11:12]

Yep, unmanageable.

speaker2：[00:11:12 - 00:11:21]

Vivek, Vivek, we are yelling at Dusty to give you all kinds of money for people, so you just need to take it. Just have like 20 people on your team, it'll be fine.

speaker2：[00:11:23 - 00:11:24]

Better you than me.

speaker1：[00:11:24 - 00:11:26]

It's a whole other headache.

speaker2：[00:11:26 - 00:11:28]

Not mine. That's Vivek's.

speaker4：[00:11:29 - 00:11:31]

That's a lot of reviews to write, Vivek.

speaker1：[00:11:33 - 00:11:33]

Oh, man. Oh, God.

speaker1：[00:11:33 - 00:11:35]

Don't give me PTSD.

speaker2：[00:11:38 - 00:11:38]

Cool. All right.

speaker2：[00:11:38 - 00:11:40]

Well, I think that's everything we got then.

speaker1：[00:11:42 - 00:11:42]

All right.

speaker2：[00:11:42 - 00:11:43]

I'll catch you guys later.

speaker4：[00:11:43 - 00:11:44]

Thanks, guys.

speaker2：[00:11:45 - 00:11:46]

All right. Later.

speaker2：[00:11:49 - 00:11:51]

Okay. I totally don't believe in that the share works.

speaker2：[00:11:51 - 00:11:55]

I just shared you my Rd. Wellsky agent.

speaker4：[00:11:55 - 00:11:55]

Yeah.

speaker2：[00:11:56 - 00:11:58]

I just want to see if it pops.

speaker4：[00:11:58 - 00:11:58]

It won't.

speaker2：[00:11:58 - 00:11:59]

It won't. It won't.

speaker2：[00:12:00 - 00:12:03]

So then in that case, I'm putting everything through a rec.

speaker4：[00:12:03 - 00:12:03]

Yeah.

speaker2：[00:12:03 - 00:12:04]

And it's fine.

speaker4：[00:12:04 - 00:12:17]

I will tell, what I'm going to do is I'm going to tell whoever it is, input the e-mail address, share it that way, and then I can put the name in the rec that I send to Vivek's team, go approve this, make it right.

speaker2：[00:12:17 - 00:12:22]

Because I'll tell you, and it's fine. And to be honest, I've been on both sides of where Vivek's at.

speaker2：[00:12:23 - 00:12:36]

I've been the builder and I've been the business owner. And I mean, the impact on your offshore team to not have all that data in Gemini is like ridiculous.

speaker2：[00:12:36 - 00:12:40]

And it's like, it's a huge deal. And Vivek's like, well, I gave it to Google.

speaker2：[00:12:40 - 00:12:43]

I'm like, I get that. It's going to be months.

speaker2：[00:12:44 - 00:12:45]

And so it's like, God dang it.

speaker4：[00:12:45 - 00:12:56]

Yeah. To me, that knowledge content connector in Gemini It should have been day one rollout. I mean.

speaker2：[00:12:56 - 00:13:00]

It was supposed to be clear back into copilot for support.

speaker2：[00:13:01 - 00:13:10]

And then that bombed and then we're like, that's okay, we'll use Gemini and then yeah, we'll have it done in a week, which has turned into, I mean, eight months.

speaker4：[00:13:10 - 00:13:10]

Yep.

speaker2：[00:13:11 - 00:13:27]

And I mean, and I'm again, like Vivek's doing everything he can, but it's just like, I don't know. Like, I don't think, I think Vivek is truly owning the prioritization across all of wells. And I don't know if it's always right, but whatever.

speaker4：[00:13:27 - 00:13:27]

Yeah.

speaker2：[00:13:28 - 00:13:30]

Anyway, well, cool, man. Hey, well, awesome.

speaker2：[00:13:30 - 00:13:32]

I mean, we're getting a ton of traction.

speaker4：[00:13:32 - 00:13:32]

Yeah.

speaker2：[00:13:32 - 00:13:39]

So like, I mean, and it feels like we're doing it in a way where nobody's dying and it's not dysfunctional.

speaker4：[00:13:39 - 00:13:39]

Yeah.

speaker2：[00:13:39 - 00:13:52]

And I'll tell you what, as we were saying, I love the idea of a closeout meeting because I've got to make sure that Proffer sees that his span is not a call center. And him and Chris and I have been in meetings where we're saying those things.

speaker2：[00:13:52 - 00:13:56]

You own all of ops for Ryan. Yeah, that sounds great.

speaker2：[00:13:56 - 00:13:58]

What is that? Well, it hasn't taken shape yet.

speaker2：[00:13:58 - 00:13:59]

So this is great.

speaker4：[00:14:00 - 00:14:07]

So the handoff meeting will basically be turning over any maintenance, like fixing or if something breaks to proffer.

speaker4：[00:14:07 - 00:14:12]

But Patrick will still own like build work for a V2, correct?

speaker2：[00:14:12 - 00:14:15]

I believe so. And I think, yes, formally.

speaker2：[00:14:16 - 00:14:33]

I think the way I see the closed meeting going and then And then let's say a V2 conversation, Patrick will, I bet, do a really good job of providing technical documentation and recommendations on like, here's what Michael needs to do, and here's some  that'll break for a beer up.

speaker2：[00:14:34 - 00:14:40]

So then we're gonna go. And then what's gonna happen is in four months, let's say it's Jill comes back and says, I want new stuff.

speaker2：[00:14:40 - 00:14:47]

Before we hit Patrick, I think she's gotta go through us and defend it. If it does, I think a beer up checks it out.

speaker2：[00:14:48 - 00:14:52]

And says, Hey, does he want the work or do we send it to Patrick?

speaker2：[00:14:52 - 00:15:01]

And I think so, and in my head, Abirab has, on the technical side, has right of first refusal. If he can take it and he wants it, go for it.

speaker2：[00:15:01 - 00:15:09]

We'll go hit Vivek, but the feedback I have gotten from Abirab, and it's been true so far, he will just build .

speaker2：[00:15:10 - 00:15:15]

And so he will never say no and never give any work to Patrick is my assumption, so we'll have to watch him.

speaker4：[00:15:15 - 00:15:15]

Okay.

speaker2：[00:15:15 - 00:15:18]

But that's okay. I mean, he wants to work.

speaker4：[00:15:18 - 00:15:19]

I'll take it.

speaker2：[00:15:19 - 00:15:27]

But I told you that he shot me a message and said he'll have chat done next month, right? And I'm like, Avira, I like you, but no.

speaker4：[00:15:27 - 00:15:29]

You are never talking to Chris, ever.

speaker2：[00:15:30 - 00:15:32]

That's a great point. I didn't even think of that.

speaker4：[00:15:32 - 00:15:34]

Don't let Chris talk to Avira.

speaker2：[00:15:34 - 00:15:39]

Actually, if they go around me, I'm not, I'm just gonna be like, sounds great. That sounds great.

speaker2：[00:15:39 - 00:15:41]

I can't wait to see it. I'm just going to let him  run.

speaker4：[00:15:41 - 00:15:42]

Just go with it.

speaker2：[00:15:42 - 00:15:47]

And I mean, they are both going to run right into a brick wall. I didn't even know that would happen, guys.

speaker4：[00:15:48 - 00:15:51]

Barup will be working 27 hours a day, just going.

speaker2：[00:15:52 - 00:15:58]

I mean, that's his own fault. Like, you know, Barup's a good guy.

speaker2：[00:15:58 - 00:16:03]

Oh, he is. And I'm, I mean, he wants to take the whole damn thing.

speaker2：[00:16:04 - 00:16:08]

he wants to build that entire strategy. He wants to build the graph databases.

speaker2：[00:16:08 - 00:16:14]

He wants to do the entire thing. And I'm like, look, man, I'm just going to bring him along for the ride and I'm just going to continue to be like, this is the outcome.

speaker2：[00:16:15 - 00:16:16]

Sort out the work.

speaker4：[00:16:16 - 00:16:18]

Does he have people reporting to him? He does.

speaker2：[00:16:18 - 00:16:19]

He's got two.

speaker4：[00:16:19 - 00:16:20]

Okay.

speaker2：[00:16:20 - 00:16:24]

But they're not. I've been told that they are not truly many of Europe's, meaning.

speaker2：[00:16:24 - 00:16:34]

Abhirap's pretty close to full stack. Like you can just hand him a problem and he'll be able to do the whole thing, which implies database, API, scaling design, cloud architecture.

speaker2：[00:16:34 - 00:16:38]

And he's pretty good so far. I don't think he's got any client side code.

speaker2：[00:16:38 - 00:16:43]

So the presentation he'd lack, but AI will do it. So he's kind of fine.

speaker2：[00:16:43 - 00:16:47]

But I've heard his other two people are a little more junior, like don't expect anything close to that.

speaker2：[00:16:47 - 00:16:57]

So, I haven't worked with him, and I believe his two direct reports are gonna stay tied to connected networks, so they're gonna matrix across. So, my point is, I don't know if William ran into it.

speaker4：[00:16:57 - 00:17:01]

Yeah, okay, cool. All right, good deal, dude.

speaker2：[00:17:01 - 00:17:04]

Yep, on to the next one.