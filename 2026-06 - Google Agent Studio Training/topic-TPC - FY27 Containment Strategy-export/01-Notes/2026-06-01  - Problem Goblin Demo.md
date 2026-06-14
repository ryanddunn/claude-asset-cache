---
fileClass: note
type: note
created_date: 2026-06-01T00:00:00.000Z
notes_status: Reviewed
meta:
  - Meeting
topics:
  - '[[TPC - Agent Beta Program]]'
  - '[[TPC - FY27 Containment Strategy]]'
entities:
  - '[[Gage Bradley]]'
  - '[[05-Entities/Jarrad Weinzerl]]'
  - '[[05-Entities/Chris Coffey]]'
  - '[[Tom Lemon]]'
---

# Notes

* Reviewed data sources necessary for the tool, these are what we need automated integrated with Vivek
* how to research scenarios
* how to track bypass and fallback
* Chris provided a lot of context on how he would like to see leaders use this tool and also his expectations on support leaders
* Training for all leaders
* Here is how problem mgmt uses it
* Chris provided a lot of feedback on how support leaders should use this
* ==action - built out CE command center home page where alerts for all agents ==
	* dashboard?
* hybrid support later discussion

# Summary

Gage Bradley demoed **Problem Goblin** — a Chrome extension / Salesforce overlay he built to help support leaders analyze CCAI contact center data without needing deep technical access. Chris Coffey and Jarrad Weinzerl were present. The meeting was a tipping-point demo that shifted from "hold for pitch day" to "get this into production now."

## What Problem Goblin Does
- Sits as an overlay inside Salesforce and merges data from **three sources**: Salesforce case object, Salesforce UJET object, and GCP logs
- Currently requires two manual Salesforce CSV report exports to load (this is the main friction point — targeted for automation via Vivek integration)
- Key capabilities:
  - Unified case + UJET data table with call recordings accessible in one place
  - **Mass transcript search** across all cases simultaneously
  - **Bypass and fallback escalation tracking** — surfaces articles that failed to contain and may need content improvement
  - **Article reference viewer** — shows snippets, URLs, and content the AI used when responding
  - **LQL generator** — auto-writes GCP log query syntax so leaders can pull detailed logs without needing direct GCP access (Gage runs it for them for now)
  - Normalized export for further analysis

## Key Discussion Points
- **For support leaders** — gives non-technical, analytics-minded leaders a self-service path to investigate CCAI performance, bypass trends, and article quality without going through Tom or Gage every time
- **Chris's direction**: don't wait for pitch day — deploy now, use real adoption as proof for the competition. Build 3–4 prescriptive training scenarios so leaders know exactly how to use it
- **Scope clarity**: Problem Management will use the tool differently than support leaders. PM surfaces trends and feeds leaders; leaders use it to investigate issues that don't surface naturally
- **The bigger vision**: Problem Goblin becomes a feeder into the **CE Command Center home page** — a persona-based dashboard where AI surfaces the top opportunities/alerts to a support leader's "inbox" each morning, rather than requiring them to go find it themselves
- **Toward agentic operations**: Tools being built today are "skills" — eventually they roll up into a role-profile-based agent ecosystem where a support manager dashboard auto-assigns the right skills and surfaces AI-generated recommendations. Human-in-the-loop shrinks over time as accuracy improves

## Next Steps
- [ ] **Vivek integration** — automate the two manual CSV uploads so data flows live (highest priority unlock)
- [ ] Publish Problem Goblin in **CE Command Center** as a cataloged tool
- [ ] Gage + Ryan: develop **3–4 prescriptive training use cases** for support leaders ("complaint hit my windshield — here's what you do")
- [ ] Chris + Jarrad: determine where CE Command Center home page / unified dashboard falls in the backlog
- [ ] ==Build out CE Command Center home page with AI agent alerts==

# Transcript

speaker1：[00:00:00 - 00:00:01]

Prop Goblin demo.

speaker1：[00:00:08 - 00:00:10]

I'm here. No, a little.

speaker2：[00:00:10 - 00:00:10]

Not too bad.

speaker1：[00:00:10 - 00:00:12]

How's your weekend?

speaker2：[00:00:12 - 00:00:15]

Pretty good. I got some gardening.

speaker2：[00:00:15 - 00:00:17]

Nice. How's yours?

speaker1：[00:00:18 - 00:00:18]

Good. It was real low key.

speaker1：[00:00:18 - 00:00:21]

We didn't really have any sports. It's funny you said the gardening.

speaker1：[00:00:21 - 00:00:31]

Like we got, we do a little bit of it and I really like doing it. I shouldn't say I don't do anything, but my wife does.

speaker1：[00:00:31 - 00:00:39]

And I like that we're doing it. And so I was just telling her, I was like, I said, I want to build a larger thing.

speaker1：[00:00:39 - 00:00:43]

And we didn't really make an attempt to landscape our backyard. It's just sort of big and open with the kids.

speaker1：[00:00:44 - 00:00:45]

So anyway, that's cool, man.

speaker2：[00:00:47 - 00:00:52]

Yeah, well, it's our second year doing it. I'm not historically a gardener, so we'll see how it goes.

speaker1：[00:00:53 - 00:00:54]

Right on.

speaker2：[00:00:54 - 00:00:56]

But yeah, it's fun to do.

speaker1：[00:00:57 - 00:01:01]

I like the vibe of it. Vibe of it.

speaker2：[00:01:01 - 00:01:12]

It's like, it's just a nice way to get outside, honestly. Are they coming here?

speaker1：[00:01:13 - 00:01:16]

He's coming here. Afternoon, sir.

speaker1：[00:01:19 - 00:01:19]

How we doing?

speaker3：[00:01:19 - 00:01:20]

Not sleepy in here.

speaker1：[00:01:21 - 00:01:26]

I just shut it because I was too bright for me. But.

speaker3：[00:01:27 - 00:01:29]

Me too, Ben. Thanks.

speaker3：[00:01:29 - 00:01:32]

My eyes are going to . That's your bad form.

speaker3：[00:01:32 - 00:01:39]

I'm turning to an old system engineer. You just need some light bulbs.

speaker1：[00:01:39 - 00:01:47]

I feel like you need the glasses where you lean back and they make your eyes look huge and they're like, it's like you're a professor that tinkers with welding on the side.

speaker2：[00:01:47 - 00:01:56]

I already have my blue light filters. It's 78%.

speaker3：[00:01:56 - 00:01:58]

I am blanking out. Not The Office.

speaker3：[00:02:00 - 00:02:06]

What was that movie? The Red Stapler guy.

speaker1：[00:02:06 - 00:02:09]

Oh yeah, The Office. Oh, Lots of Space.

speaker3：[00:02:09 - 00:02:13]

He kept getting stuck on The Office. I'm like, no, Office Space.

speaker3：[00:02:14 - 00:02:16]

With the guy with the big glasses with the red stapler.

speaker1：[00:02:16 - 00:02:22]

Yeah, Actually, that's exactly what he did. Do we got, we got Tom or no Tom?

speaker3：[00:02:22 - 00:02:23]

Hey, he's famous. Do you guys know that?

speaker1：[00:02:24 - 00:02:26]

And what did he finally punched a parent? Like, what did he do?

speaker1：[00:02:26 - 00:02:28]

close. close.

speaker3：[00:02:28 - 00:02:30]

News story hit USA Today.

speaker1：[00:02:31 - 00:02:32]

What did you do?

speaker4：[00:02:32 - 00:02:35]

Dude, the one I told you about where the kid threw the fastball into the dugout?

speaker3：[00:02:35 - 00:02:37]

I saw it this weekend on USA Today.

speaker4：[00:02:37 - 00:02:39]

Yeah, you're kidding me. Yeah, it's national news.

speaker1：[00:02:39 - 00:02:41]

Dude, you got to send me the link.

speaker3：[00:02:41 - 00:02:43]

Yeah, I'll send you. I texted it to Jared.

speaker1：[00:02:43 - 00:02:45]

I'm going to print and have Jared sign it.

speaker3：[00:02:45 - 00:02:46]

Yeah, let's do that.

speaker4：[00:02:48 - 00:02:49]

Yeah, it's national news, man.

speaker1：[00:02:50 - 00:02:53]

What's it feel like on the national stage? A little bit of a .

speaker4：[00:02:54 - 00:02:58]

Like I told Chris, I wish it was something for a hell of a lot better than tossing out, than injecting a coach.

speaker1：[00:02:58 - 00:03:03]

No, I mean, I'm thinking tossed him out. I'm a total power play.

speaker1：[00:03:03 - 00:03:04]

Dude, I totally agree.

speaker3：[00:03:05 - 00:03:07]

Total power play. I'd take that all day long.

speaker1：[00:03:09 - 00:03:10]

Yeah, man, you gotta.

speaker3：[00:03:10 - 00:03:13]

I send it to all my family and friends and I go, I know this guy.

speaker1：[00:03:14 - 00:03:17]

And he's mean and he's mean as hell too. Like I'm not surprised at all.

speaker1：[00:03:17 - 00:03:19]

That parent didn't even know what he's doing. Good.

speaker1：[00:03:20 - 00:03:21]

Dude, that's awesome.

speaker3：[00:03:21 - 00:03:23]

Here we go. Send it to you.

speaker1：[00:03:24 - 00:03:24]

Thank you.

speaker4：[00:03:26 - 00:03:29]

He ended up getting a lot. The coach got a lifetime ban.

speaker3：[00:03:29 - 00:03:30]

That's what I saw.

speaker4：[00:03:30 - 00:03:30]

Yeah.

speaker1：[00:03:30 - 00:03:32]

Oh, is that? And the kid got a five-year.

speaker4：[00:03:32 - 00:03:33]

Five-year, yeah.

speaker1：[00:03:33 - 00:03:34]

I did see that.

speaker4：[00:03:34 - 00:03:35]

Yeah. That's so funny.

speaker3：[00:03:35 - 00:03:38]

That kid, like not that he had a baseball career coming, but like.

speaker4：[00:03:38 - 00:03:46]

Well, the thing is, it's only through U Triple SA, but there's like two or three other organizations in Kent City, like he can play for a perfect game or whatever.

speaker3：[00:03:46 - 00:03:49]

Well, he's an Oklahoma team, wasn't it? Yeah.

speaker4：[00:03:49 - 00:03:54]

So I mean, they've got perfect game and stuff down there, but you triple SA, he's they're done.

speaker1：[00:03:54 - 00:03:54]

Yeah.

speaker4：[00:03:55 - 00:03:55]

So.

speaker3：[00:03:55 - 00:03:57]

 . Did you see it?

speaker4：[00:04:00 - 00:04:03]

I umpire and I direct baseball tournaments on the weekends, so yeah.

speaker1：[00:04:06 - 00:04:07]

Are you named in it? No.

speaker3：[00:04:08 - 00:04:10]

Do you want to be?

speaker1：[00:04:10 - 00:04:10]

Should I write your name?

speaker4：[00:04:11 - 00:04:14]

No, I want my name anywhere associated with it.

speaker3：[00:04:14 - 00:04:17]

I like the idea of printing it off and get his signature on it.

speaker4：[00:04:18 - 00:04:21]

But we have officially sidetracked this game.

speaker1：[00:04:22 - 00:04:26]

Okay, all right, if we got to get back on track. Okay, here's the context.

speaker1：[00:04:27 - 00:04:34]

Gage has been secretly building an agent that I intentionally didn't want to tell anybody because it's really strong for pitch day.

speaker1：[00:04:34 - 00:04:45]

So I was sort of like, he's doing his thing, just let him roll because I was like, I thought it was going to be really, quite frankly, an impactful splash. But you keep working on it and it keeps getting better to the point where I can't not.

speaker3：[00:04:46 - 00:04:54]

The tough part about pitch day is we can't hold things in our back pocket until pitch day. It's too far away.

speaker1：[00:04:54 - 00:04:55]

That's what this is.

speaker3：[00:04:55 - 00:05:01]

We've got to deploy it out and then we can still, I think, still be in the pitch day competition.

speaker2：[00:05:01 - 00:05:05]

That's my plan. I would like people to use this as soon as possible.

speaker3：[00:05:05 - 00:05:11]

And I think we should push that with everybody is like, that's not your big splash out there. Do it between now and then.

speaker3：[00:05:11 - 00:05:14]

And if you want to submit, two or three or four different things go do it.

speaker3：[00:05:14 - 00:05:18]

Our goal is how are we building a catalog of these things and start using it?

speaker2：[00:05:18 - 00:05:19]

I feel like that's, yes.

speaker3：[00:05:19 - 00:05:24]

Because that honestly, that could be in your pitch of like, how have you validated this works? I'm like, well, everybody's freaking using it.

speaker3：[00:05:24 - 00:05:26]

So that's a good point.

speaker1：[00:05:26 - 00:05:34]

So that's kind of where it is. I felt like Gage gave me a demo and it was to a tipping point where I'm like, we need to get this in operation.

speaker1：[00:05:34 - 00:05:43]

So the context that I think for you, Chris, which is why I think it is so important is that basically trying to build leaders with Gen.

speaker1：[00:05:43 - 00:05:57]

AI strategies, right? And it's a tough thing and I was talking to Gage about it and I'm like, there's a lot, everybody's got a lot of different skill sets and I want, I feel like right now we're a little bit over index on if you don't have a pretty solid technical acumen, they're floundering.

speaker1：[00:05:58 - 00:06:21]

And I think this solves that problem because, and what Gage is gonna be able to show you is like basically the scenario of, and I'm looking at this through a Steve Yeager, Shelby type of viewpoint where it's like, I'm getting crushed on ops, you know what I mean, with support, whether it's average handle time or whatever the case may be, what do I do? This is the answer of you do this.

speaker1：[00:06:21 - 00:06:33]

And then, and I think from there, I think Gage just, let's just walk through a demo of it because I think you'll be very surprised how. I mean, really what this thing will do.

speaker1：[00:06:34 - 00:06:38]

And I think the very next thing you're going to say, Chris, is, oh, we got to wire this up to live data. Yes, we do.

speaker1：[00:06:39 - 00:06:40]

And then this thing will be there.

speaker3：[00:06:41 - 00:06:45]

The one thing I will say, I think it might be coming out of the TV.

speaker3：[00:06:48 - 00:07:04]

The one thing, and I agree with you that you have to have a little bit of technical acumen to be able to figure out this AI stuff. Our leaders should be challenged more than anybody else of like, that's actually your job expectation is to have some technical accuracy.

speaker3：[00:07:04 - 00:07:16]

But the leap we need to make is an effective support leader, not saying you have to be an expert, but you cannot be an effective support leader if you don't have an analytics mindset.

speaker3：[00:07:17 - 00:07:24]

You have to be able to look at a backlog, at incoming volume, at client data, export it and go look through some Excels with some pivot tables.

speaker3：[00:07:24 - 00:07:30]

If you can't do that as a support leader, that's like 101 stuff that's existed for decades.

speaker3：[00:07:30 - 00:07:37]

And so this is kind of the conversion of that, was the baseline, now this is the new baseline.

speaker1：[00:07:38 - 00:07:43]

Yeah, and I think the new baseline is a little bit of an understanding of connecting UI to API.

speaker1：[00:07:44 - 00:07:59]

And data stores, so then you can kinda take action on it, yeah, versus because I completely, and I think that I'm trying to connect the analytics side, which actually this is, that's a great segue, yeah, because I think this is gonna marry it up pretty well. So, anyway, I think this is gonna be really good.

speaker1：[00:07:59 - 00:08:00]

No pressure, Gage.

speaker2：[00:08:01 - 00:08:02]

All the pressure.

speaker1：[00:08:02 - 00:08:04]

You gotta start with that. We gotta explain that, 'cause.

speaker2：[00:08:05 - 00:08:11]

Yeah, so it lives, it's a Salesforce. it's a Chrome extension that lives locally, right?

speaker2：[00:08:11 - 00:08:12]

So it's not published, obviously.

speaker3：[00:08:12 - 00:08:14]

'Cause this little dude down here.

speaker2：[00:08:14 - 00:08:23]

Yeah, so it's an overlay, right? It sits in Salesforce, so look at that dude, you gotta tell him what it is, it's a goblin, it's a prob, it's the prob goblin.

speaker3：[00:08:23 - 00:08:24]

It looks like an angry Yoda.

speaker2：[00:08:25 - 00:08:27]

It's A prop goblin. It's A prop goblin.

speaker2：[00:08:27 - 00:08:34]

So this is just one module of this, right? This reporting, I've built all these other things I do.

speaker2：[00:08:35 - 00:08:49]

I won't demo that today, but that'll be a pitch day thing. So basically the reporting, what this does is like, so the problem with Google data right now is it lives in three places or three different reports.

speaker2：[00:08:50 - 00:09:00]

the Salesforce case object, the Salesforce UJET object, and then the GCP logs, which includes all the article references and stuff. This basically marries a lot together.

speaker3：[00:09:00 - 00:09:06]

Does the user have to have access individually to those data sources to use this?

speaker2：[00:09:07 - 00:09:10]

They do. So this is, no one's going to have the GCP access.

speaker2：[00:09:10 - 00:09:22]

If they want that data, they can ask me, and I've enabled them to This will write a GCP query for them based on the data in here that they can give to me.

speaker3：[00:09:22 - 00:09:25]

Is there a way to tie that data in from a future state?

speaker1：[00:09:25 - 00:09:36]

Oh yeah, I mean, yeah, I think talking out loud, what I'd want to do so that we don't impact GCP directly is we'd have a nightly job that would dump the logs into some place that would represent them where we could dynamically run it through BigQuery.

speaker3：[00:09:36 - 00:09:41]

Do you see this living inside of Salesforce? Is there like a workflow reason it's in there?

speaker2：[00:09:42 - 00:09:42]

Yes.

speaker3：[00:09:42 - 00:09:46]

So it would not go in like the client experience command center that you run as an independent tool.

speaker2：[00:09:47 - 00:09:55]

It could. The nice thing about having it as a Salesforce plugin is that it can automate Salesforce tasks, which is another function of this.

speaker2：[00:09:55 - 00:09:55]

Okay.

speaker3：[00:09:56 - 00:09:57]

All right, I'll stop interrupting.

speaker1：[00:09:57 - 00:10:02]

The answer is partially yes and partially no. So I think this is actually going to be a tool where like.

speaker1：[00:10:02 - 00:10:10]

Gage built a bunch of stuff. I think if this scales, we might need to drop some in Command Center and some natively, because part of the...

speaker3：[00:10:10 - 00:10:15]

In the install and instructions and cataloging of it goes in Command Center as a published tool, right?

speaker3：[00:10:16 - 00:10:22]

That for a support leader, you need to go pull this, but the install file might put a workflow somewhere else. Yeah, that's fine too.

speaker2：[00:10:22 - 00:10:34]

The reporting doesn't need to be in Salesforce, but it's just there because I built it in that to start with. Okay, so To start with, they come here. I've got pre-built Salesforce reports, so it runs off of two that they both need to run externally.

speaker2：[00:10:34 - 00:10:39]

This is where the brunt of the work exists. It's just the fact that we have to live with this for now.

speaker3：[00:10:39 - 00:10:41]

And this would be the part that you would look at tying it up.

speaker1：[00:10:41 - 00:10:45]

Yep, Vivek would integrate this in natively, so these two parts would go away.

speaker2：[00:10:45 - 00:10:48]

Got it. So 2 Salesforce reports that I've pre-built.

speaker2：[00:10:48 - 00:10:55]

One is to pull all the UJET data for a time frame for inbound stuff only, and the other is same thing for cases only.

speaker3：[00:10:55 - 00:11:05]

And you clicked those buttons to launch. launch the report, did it automatically filter in the context of a profile being tied to specialty care or?

speaker2：[00:11:05 - 00:11:08]

No, that's something I've yet to do. Eventually that would be nice.

speaker3：[00:11:09 - 00:11:15]

So we could do that with the integration. If you have an integration there, direct integration, you could just filter it directly from that port.

speaker2：[00:11:15 - 00:11:19]

Yeah, so that's a one click process. So for now, all they have to do is change their solution, right?

speaker2：[00:11:20 - 00:11:28]

Then they run it, then they go to upload CSV. And I did AND just as an example because it's kind of a small data set.

speaker2：[00:11:29 - 00:11:33]

So it'll tell you when your source has been uploaded. Actually, I've got some old logs in there.

speaker2：[00:11:33 - 00:11:44]

Let me do that again. So right away, I mean, this is even helpful for just looking at, come on here, case data.

speaker2：[00:11:44 - 00:11:50]

And UJET data, 'cause you've got, like, you can listen and download all the calls right from here instead of having to go through the UJET stuff.

speaker3：[00:11:50 - 00:11:54]

So, again, with that, you have to be logged in to Google.

speaker3：[00:11:55 - 00:11:59]

You do, yeah, it's like a cookie session or something that allows you to get into it.

speaker2：[00:11:59 - 00:12:03]

Yes, okay, but you would anyway in Salesforce. This is just nice, 'cause do all leaders have that?

speaker2：[00:12:04 - 00:12:15]

They should, yeah, but this is nice 'cause it's all in one place, and then you come back here, we'll upload the case half of it. And this will just kind of concatenate into one table, right?

speaker2：[00:12:15 - 00:12:17]

So now you've got all the cases you can link out to.

speaker1：[00:12:17 - 00:12:23]

What you just did, though, is a big deal. His upload didn't go like this.

speaker3：[00:12:23 - 00:12:24]

It went like this.

speaker2：[00:12:24 - 00:12:32]

It went like that. And it pivots out the UJet stuff, because right now, all of this stuff lives in short description.

speaker3：[00:12:33 - 00:12:34]

Yeah, so it separates it out.

speaker2：[00:12:34 - 00:12:38]

Yeah, so I had to do that and then link it all together. So that's this, right?

speaker2：[00:12:38 - 00:12:42]

And now here's the really cool part. You can...

speaker2：[00:12:42 - 00:12:50]

We've got all the transcripts in here. I can come in here and you can mass search every transcript for every case in here.

speaker2：[00:12:50 - 00:12:57]

And then if I want to include text search for descriptions and subjects with no transcripts, I can do that. If I want transcripts only, I can do that.

speaker1：[00:12:57 - 00:13:01]

You can see how helpful this is for Tom and Gage to identify gaps.

speaker2：[00:13:02 - 00:13:06]

It's a discoverability tool, basically. Now the really cool part is...

speaker2：[00:13:07 - 00:13:11]

Based on what's filtered, I can export a normalized report with all these columns.

speaker2：[00:13:11 - 00:13:17]

I can click this, which generates an LQL.

speaker1：[00:13:17 - 00:13:23]

Are you guys familiar with LQL? This is the logging query language inside of GCP.

speaker1：[00:13:23 - 00:13:34]

So when we get feedback that says, somebody set a call drop, you go into the logs of GCP, of which the Gemini client experiences throwing logs.

speaker1：[00:13:34 - 00:13:42]

That and what LQL is SQL for logging, he pre-built the syntax.

speaker1：[00:13:42 - 00:13:48]

So now the bottom there immediately filters out millions of logs to only get what you need.

speaker2：[00:13:48 - 00:13:52]

Just what's here. So you come here, this is the part that they can't do.

speaker2：[00:13:52 - 00:13:56]

If they want me to do it, I'll do it. So I don't click that button, send this to me.

speaker2：[00:13:56 - 00:13:59]

I plug it in here, run it, and then I get back to them.

speaker1：[00:13:59 - 00:14:06]

This could also be completely done by ViaVivec, so that they'd never see the GCP console, but they would get the log, because.

speaker3：[00:14:06 - 00:14:13]

There's a lot of handoffs of data between different systems and stuff, and I think that's in order to kind of commercialize it, if you will.

speaker3：[00:14:14 - 00:14:20]

All of that has to be tied up and it has to not be dependent on you got 75% of the investigation done, now go to Gage.

speaker1：[00:14:21 - 00:14:24]

I think that I completely agree with you. That's actually why I wanted the demo.

speaker1：[00:14:24 - 00:14:31]

Because I think it warrants slating up and because you're exactly right, all the file movement, Vivek will solve.

speaker3：[00:14:31 - 00:14:35]

So, okay, you get all this data, you simplify it down.

speaker3：[00:14:36 - 00:14:49]

What's the benefit, aside from the obvious scaling conversation, I feel like this largely, like you and Tom are two people with oversight over a lot of different things.

speaker3：[00:14:50 - 00:15:02]

But this is simplifying it all down to like, yeah, I'm manually searching it, but why couldn't I just do a, have a view on this that says, go tell me the top hit rate on words, phrases, or topics.

speaker3：[00:15:03 - 00:15:12]

And you have a dashboard from this data set that is just constantly curating, saying, what are my most common things.

speaker3：[00:15:12 - 00:15:21]

But the reason I say that is like, I don't need every support manager going and doing that because it's already there. It's already done.

speaker3：[00:15:21 - 00:15:31]

Now what you might need is a. a weekly output from problem management that drops into a support leader's queue that says this was identified and it's not tied to a PBM yet.

speaker3：[00:15:31 - 00:15:36]

Like you go review it and come back to me if you want to log a PBM. But like I get what?

speaker1：[00:15:36 - 00:15:53]

You're saying, but I think the other thing is like without being prescriptive, this allows them a path to be speculative against where they're thinking they want to put pressure because that's where I was going is like now you've got a support leader, like you said, an analytic minded person, but not necessarily technical.

speaker1：[00:15:53 - 00:15:57]

Now the whole entire data set, it's like now they can start to say, I mean, I.

speaker3：[00:15:58 - 00:16:08]

100% see the value of it. And I do think the more about a solution, the more you're going to ask questions in detail that you and Tom won't naturally ask.

speaker3：[00:16:09 - 00:16:16]

So there's value in that side of it, but it's also, and this gets into where's the handoff between problem management and everybody else.

speaker3：[00:16:16 - 00:16:21]

Some of this stuff, I'm just going to surface up and say our algorithms are telling that this is a high hit rate thing.

speaker3：[00:16:22 - 00:16:27]

And I'm gonna feed you high hit rate things, and then we need to work together on what do we do about it.

speaker3：[00:16:28 - 00:16:38]

This gives you a portal to get into things that maybe aren't naturally teasing out there, and where we've gotta challenge people of stop waiting for things to be teased out through the tools.

speaker3：[00:16:39 - 00:16:44]

I need you to go find something that didn't naturally tease out, and this does help give them that.

speaker1：[00:16:44 - 00:16:47]

That's where I was going. Now they're proactive, yep.

speaker5：[00:16:47 - 00:17:02]

Because it's easy to like, we've got all the low-hanging fruit problems that they come and it's like our elephant in the room topics during a meeting, and then after that we're kind of like, Okay, well everyone go look for something, yeah, so this is so it doesn't have to bottleneck through Tom and I, which is kind of nice, but yeah, talk.

speaker3：[00:17:02 - 00:17:06]

Me through those columns right there, there's the user utterance.

speaker5：[00:17:06 - 00:17:11]

Yeah, so response type through the end, these are all from GCP, right?

speaker3：[00:17:11 - 00:17:13]

User is this like a chronological like...

speaker5：[00:17:14 - 00:17:22]

So user, so these are separated by bars, right? And these are chronologically what the person said to the agent in order.

speaker5：[00:17:23 - 00:17:28]

Rewritten query, so like it says hello on everyone. I don't know why, that's like the welcome message.

speaker5：[00:17:28 - 00:17:29]

They're not saying hello.

speaker3：[00:17:29 - 00:17:29]

Yeah, that's fine.

speaker5：[00:17:30 - 00:17:38]

Locked out of account is what they said. This is the AI interpreted question, like this is the rewritten question that AI grabbed and said, this is what they asked me.

speaker5：[00:17:38 - 00:17:43]

And then here is what the AI spat out in response to their query here.

speaker5：[00:17:43 - 00:17:52]

So if this, there's some stuff that's not quite consistent in here, like this should, there shouldn't be a QA peer here.

speaker5：[00:17:52 - 00:17:58]

But once I fix that, you can come in here and like look at every article that's referenced, right?

speaker5：[00:17:58 - 00:18:06]

You can come into snippets and view like the article, the URL, the content that it was looking at when it specified.

speaker1：[00:18:06 - 00:18:12]

So now they're able to say if somebody's like, I think it's wrong. You can go find out where the AI references are.

speaker3：[00:18:13 - 00:18:19]

Like I dropped a call or someone calls in and they're not happy with an experience. This is now where you go find it.

speaker3：[00:18:20 - 00:18:27]

Or as long as you can get a case number or whatever, then you go in here and it'll give you more layman's terms breakdown of the file log.

speaker3：[00:18:28 - 00:18:43]

And that's a good example of like a use case of that's where support managers are going to be. Like they need to live in that world of And maybe it triggers off of CSAT and we start looking at, okay, negative CSAT, why was it in the catalog?

speaker3：[00:18:43 - 00:18:50]

And then I gotta go pull the data on what was the interaction experience on that negative CSAT? Was there something bad here?

speaker5：[00:18:51 - 00:19:04]

Yeah. And like here's another good use case, for example, like you wanna look at all agent requests and fallback escalations, like times where an article is referenced, but someone either said, no, it didn't answer my question or it tried too many times and then transferred them.

speaker5：[00:19:05 - 00:19:07]

So this is bypass. They're all right here.

speaker5：[00:19:07 - 00:19:11]

And this is not a great example because there aren't a lot in here.

speaker5：[00:19:11 - 00:19:16]

But you would go, okay, this article, for this line, scroll over.

speaker3：[00:19:16 - 00:19:17]

So this is bypass.

speaker5：[00:19:17 - 00:19:22]

This is, well, I did bypass and fallback. Like this one, we can see that was a fallback.

speaker5：[00:19:22 - 00:19:30]

So it referenced that article and it didn't answer their question or it tried too many times. So that would maybe be like an article that wasn't relevant to their question.

speaker5：[00:19:30 - 00:19:38]

Or if it was under here, they didn't think that it answered their question, so maybe we need to go look at this article and make sure that the content is good.

speaker3：[00:19:38 - 00:19:47]

Well, and that's where, how close do we get to when it's an answer is given and it wasn't accepted?

speaker3：[00:19:48 - 00:19:56]

And yet that ultimately ended up being the answer based on what I see in the context of the case documentation. How do I identify those?

speaker5：[00:19:56 - 00:20:01]

We'd have to come back here and maybe look at the resolution detail. And that depends on their documentation, which is.

speaker3：[00:20:01 - 00:20:08]

But I think that's a great example of like we have got to start hammering people of like your documentation is our brains.

speaker1：[00:20:09 - 00:20:10]

Like I said, this exposes the whole thing.

speaker3：[00:20:10 - 00:20:17]

If your resolution detail is I called them back and resolved it, you didn't do anything. You resolved an N of 1.

speaker3：[00:20:18 - 00:20:20]

And that's no longer worthwhile for us.

speaker5：[00:20:21 - 00:20:22]

Yep. Yeah.

speaker5：[00:20:22 - 00:20:31]

So for that, yeah, you maybe pull fallback escalations, article numbers, and then you come in here and search those resolutions and make sure they match what they expect. Yeah.

speaker3：[00:20:31 - 00:20:40]

I mean, that's right. I think about those use cases like that, or like, how can we, what information do we need to add on top of this to think differently about exploring bypass?

speaker3：[00:20:41 - 00:20:44]

And like, bypass is a psychology game more than anything.

speaker3：[00:20:45 - 00:20:50]

there's usually it's not anything more than that, but how do we find trends and themes and patterns?

speaker3：[00:20:50 - 00:20:56]

And that's a tougher one that I think we're going to have to go dig into.

speaker3：[00:20:56 - 00:21:02]

But anyway, this, I think if we get this tied up, so we're not jumping for sure data sets.

speaker1：[00:21:02 - 00:21:05]

That's what, that's yes, that's exactly what I think the next step is.

speaker3：[00:21:05 - 00:21:15]

We get that tied up, we get it published, and we get it a little bit like, we almost have to get it past the beta. get it to a basically publish one.

speaker3：[00:21:15 - 00:21:22]

And then I think we do an hour or two working session and maybe a series of them that we push every support.

speaker1：[00:21:22 - 00:21:23]

User through.

speaker3：[00:21:24 - 00:21:33]

And you come up with like 3 or 4 prescriptive use cases of like this complaint hit my windshield, what do I do with it?

speaker3：[00:21:33 - 00:21:45]

And then you start talking through three or four of these with the data already tied up so they're not having to go Because it's like 3 or 4 leaps to mentally think about what data do I need to do this, to do that.

speaker3：[00:21:46 - 00:21:49]

We close that gap and just say, go to this tool and ask it the question.

speaker1：[00:21:50 - 00:21:59]

Dude, that's right where my head is. we get the thing wired, we do some training, and we're like, look, here's how you tackle these hard problems that right now feel nebulous.

speaker3：[00:21:59 - 00:22:09]

And I think I would add another section to that as I'm thinking through it. I would say, here's how we in problem management are using the tool.

speaker3：[00:22:09 - 00:22:15]

You don't need to use the tool for these use cases because we're doing it, we're gonna give you the data.

speaker3：[00:22:15 - 00:22:25]

It's very much, this is the meeting we've had a couple times now of what is problem management and let's go define our scope and let's go define what support leader scope is. This I think helps bridges that gap.

speaker3：[00:22:25 - 00:22:35]

Bridge that gap because now it gives you access to all the same data and here's the standard stuff we are gonna go do. Don't worry about that.

speaker3：[00:22:35 - 00:22:38]

We'll give you updates there. Everything else, here's how you go get it.

speaker1：[00:22:38 - 00:22:47]

Because I think the nuance here is if we were to wire this up and get all the data working, right? I think, and so now it's like, okay, now the sport leaders can access it.

speaker1：[00:22:47 - 00:22:56]

I feel like it would almost be worth our time then for you to sit down with Bri and say, here are the trends. that immediately would pop.

speaker1：[00:22:57 - 00:23:00]

Bypass would be one. Where it's like, this is exactly how that.

speaker1：[00:23:00 - 00:23:11]

And then we just run it against the data store in the background and just marry it up to be alerts for leaders and be like, here's what we found in your space. And it's just a simple message on Teams or whatever.

speaker1：[00:23:11 - 00:23:21]

But my point is, we're leading you to water, but it's on you to jump in and get it. But you can continue to evolve in aggregate across the whole enterprise without, still making them accountable for this.

speaker3：[00:23:21 - 00:23:28]

Well, and I think that it kind of sets the agenda of your, I don't know. what you have weekly or bi-weekly meetings with BU leaders?

speaker5：[00:23:28 - 00:23:31]

I would love them to come in and tell me what we're talking about instead of vice versa.

speaker3：[00:23:32 - 00:23:35]

That's right. I think you come in and say, this is what we've identified.

speaker3：[00:23:35 - 00:23:42]

Here's the updates on these PBMs. Now what have you found you guys bring to me the other half of it?

speaker3：[00:23:42 - 00:23:55]

And I think that becomes the framework of it. And I'd be curious to know which ones of those people are coming to you with opportunities versus which ones are just coming in and waiting for you to report the news. Because it's very much a-.

speaker1：[00:23:55 - 00:24:00]

Because now, if we're in this scenario and that's occurring, they're not the analytical leaders you described.

speaker1：[00:24:01 - 00:24:07]

But the thing that I wanted to address is you don't have to be natively like software technical.

speaker1：[00:24:07 - 00:24:18]

Now we're back to, as long as you're curious and you're gonna spend the time, we're supporting you. And I like, and I mean, Just transparently, like I was so impressed with this tool from the second gauge, showed it to me.

speaker1：[00:24:19 - 00:24:34]

So I keep asking for updates and it finally tipped over the last time he showed me where I'm like, so I'm just very excited about this because I just, the amount of complexity behind all these data sets, I mean, we need to be good here. This is client experience being very mature in our school.

speaker3：[00:24:34 - 00:24:47]

This is cool. What would happen if you took, like you throw all the data set in here and export it in this aggregated view. So it's this.

speaker3：[00:24:47 - 00:24:52]

But then you're actually putting it in through AI, through a copilot analyst or through Claude or something else?

speaker5：[00:24:52 - 00:24:53]

Probably do much better.

speaker3：[00:24:53 - 00:25:04]

And saying, go identify the top 10 themes by solution, by like, I would think we could go do that. And you could probably bake that into the tool as well.

speaker3：[00:25:05 - 00:25:10]

And that's where I get into this. Like this is the whole conversation of I don't need a dashboard.

speaker3：[00:25:10 - 00:25:14]

I've got AI that's gonna visualize the content for me and propose recommendations.

speaker1：[00:25:14 - 00:25:15]

That's right.

speaker3：[00:25:15 - 00:25:28]

So that's almost like, here's the data dig inside of this, but I think there's another tab on this that I'm asking it to go do the full analysis with AI. And as you get this into like a Vivek tool.

speaker1：[00:25:28 - 00:25:28]

Yeah.

speaker3：[00:25:29 - 00:25:33]

It's the same thing. It's the same thing that my area of quality is.

speaker3：[00:25:33 - 00:25:35]

Because all that is, this uploader.

speaker1：[00:25:36 - 00:25:39]

Upload that data. No, it's exactly the same.

speaker3：[00:25:39 - 00:25:41]

And go analyze it and create the exports for me.

speaker1：[00:25:41 - 00:25:48]

It is perfectly the same. So then I've got something that I've been wrestling with here for a while now, and I'm just saying this is where my head goes.

speaker1：[00:25:48 - 00:25:52]

We build this, it does what you said. We've got a couple other Gen.

speaker1：[00:25:52 - 00:26:04]

AI agents, and what you end up being as a support leader, or at least my concern is, like this is gonna run some trend analysis, and you just said add another tab, and then you're gonna go see what things it found. There's gonna be more of those.

speaker1：[00:26:05 - 00:26:21]

And my concern is now what the support leaders have to do is, all right, I'm walking into my day, let me load 7 tools and look, And I think what we need to do collectively in cloud experience is identify a way how did the support leaders simply get notified agnostically from Gen. AI.

speaker1：[00:26:21 - 00:26:22]

Oh, 100%.

speaker3：[00:26:22 - 00:26:28]

And I think that's where, like, this is, this gets me into the analytical mind.

speaker3：[00:26:28 - 00:26:38]

And it did cool stuff because we used AI to go build the tool that gave me the analytics, but now it depends on me to do the analytics. The next layer is go do the analytics and let me look at the analytics.

speaker3：[00:26:38 - 00:26:41]

The next layer on that is I don't really give a  about the analytics. I don't even know what I'm supposed.

speaker1：[00:26:42 - 00:26:42]

To do about it.

speaker3：[00:26:42 - 00:26:47]

And what I'm supposed to do about it is here's the top three opportunities I identified and it dropped to my inbox at 8 A.m. on Monday morning.

speaker1：[00:26:48 - 00:26:51]

That's right. And so that's exactly what I'm talking about.

speaker1：[00:26:51 - 00:26:53]

And I think, but my question is this. But I think where's the inbox?

speaker3：[00:26:54 - 00:27:02]

I think that is Client Experience Command Center. I think we create a dashboard view in the command center and it will ultimately end up.

speaker1：[00:27:02 - 00:27:03]

The home page of client experience.

speaker3：[00:27:03 - 00:27:18]

Right, and I've seen this in our engineering where engineering pulls in their data of sprint planning and bug rates and they are running their monthly ops review out of a client experience command center or an engineering command center dashboard.

speaker3：[00:27:18 - 00:27:23]

I think that becomes where our support leaders live.

speaker1：[00:27:24 - 00:27:34]

And that's where we're going to send all the alerts, because Jared, I think this is our big, greater theme, which is like, let's just build it off of engineering. But point being like, this is we're going to feed it.

speaker1：[00:27:34 - 00:27:35]

Yes, I see it with Stu all the time.

speaker3：[00:27:36 - 00:27:44]

Yeah, Stuart's got it. And like, I think we do that where that right now the client experience command center is starting off to just be like a catalog of things, which is great.

speaker3：[00:27:44 - 00:27:50]

Let's get the things in there. But eventually, there gets to be a collection of things based on a persona as a support manager.

speaker3：[00:27:51 - 00:27:57]

That now the collection of things is great, that's where I go, but what I really need is a dashboard that helps me connect all the things.

speaker3：[00:27:57 - 00:28:07]

And that's where I think this goes to, up to and including is this where our hybrid support layer lives? Does it live in a client experience center dashboard?

speaker3：[00:28:08 - 00:28:13]

Where I will refresh it, like I control my own UI. It's asynchronous.

speaker1：[00:28:13 - 00:28:14]

I know, which is wild.

speaker3：[00:28:14 - 00:28:20]

It's asynchronous. I hit refresh, it pulls in the data I need with the proposals and recommendations, where I say yes or no.

speaker3：[00:28:22 - 00:28:27]

And it just goes. Yeah, and then eventually when our hit rate gets so good on yes, I don't even need to see it then.

speaker3：[00:28:27 - 00:28:36]

I only need to see it if it didn't get resolved and it came back with another set of questions, then I actually have to triage it out. But then I triage it out of that workflow.

speaker3：[00:28:37 - 00:28:47]

I think that becomes our landing page so that we're feeding behind a UI of agents that are giving you an inbox of tasks.

speaker1：[00:28:47 - 00:28:55]

And I think the way you described it is really important because what we're doing now is we're calling them agents, we're building skills.

speaker1：[00:28:56 - 00:29:09]

And eventually it's gonna roll up into a larger agent that has a lot of skills. And so our vocabulary is gonna shift, but when we're living in that, It's like now we're creating a whole ecosystem around this client experience support agent.

speaker3：[00:29:09 - 00:29:24]

And I think that's right. If you think about the client experience command center, the tools we build, if you think of them as skills, and then we assign skills to a role profile, role profile is a support manager.

speaker3：[00:29:24 - 00:29:30]

or the role profile is incident management or director or whatever.

speaker3：[00:29:30 - 00:29:38]

And then they have a dashboard that you just click on and you can see on the question mark in the upper right-hand corner, it just loads, here's the skills that you have assigned to you.

speaker1：[00:29:39 - 00:29:41]

And the context of the.

speaker3：[00:29:41 - 00:29:47]

Skill is, this will solve this thing, this will solve this thing. They don't really need to know all those skills because it just comes together.

speaker1：[00:29:47 - 00:30:00]

Yeah, because our backlog of all these agents we're building are simply the skills that people are asking for. But I think it's interesting too, So I agree. I think this is very foundational and we're going to evolve it big time.

speaker1：[00:30:00 - 00:30:20]

I wonder if, Gage, at some point we get so prescriptive that we're like for every single, I'll say bypass, we can call it fallback or human agent request, but for whatever it is, if we can get to the point where our backlogs are small enough, I think the IC level support people have to go through and review any of them and basically if it's a true gap.

speaker3：[00:30:21 - 00:30:29]

And I think that's the hybrid support layer to a degree is it's either resolved up front, contained by AI.

speaker3：[00:30:30 - 00:30:37]

You may have a human in the loop where you say yes, no, but eventually the whole goal of the human in the loop is that my accuracy is so good that it just pushes to contained.

speaker3：[00:30:37 - 00:30:42]

And then everything that comes through, I get it over to somebody else, but then it creates another work queue for me.

speaker3：[00:30:44 - 00:30:57]

Or maybe it doesn't immediately, but like once it's solved, then it drops a work queue and says, hey, something was solved by a human that didn't get contained. And now here's the trending on how you go look at it.

speaker1：[00:30:57 - 00:30:58]

I agree.

speaker3：[00:30:58 - 00:31:04]

So there's like a manager of the hybrid layer that that's their job is to say, how much can I push into?

speaker1：[00:31:04 - 00:31:12]

Because at this point, I mean, Gage has got it wired together. It's now just simply like we build a human in the loop and continue to scale it based on feedback.

speaker3：[00:31:12 - 00:31:20]

I think that visualization of what I'm looking at is the AI Analytics output of this data.

speaker1：[00:31:20 - 00:31:24]

Yeah, I agree with that. I was thinking that too on the homepage type of thing.

speaker3：[00:31:25 - 00:31:30]

Yeah, it's almost like a prob goblin analytics board, but that turns into the manager of the hybrid layer.

speaker1：[00:31:31 - 00:31:37]

I think so. Jared and I will work through where this would fall in the backlog, because I don't want to say where yet.

speaker1：[00:31:38 - 00:31:39]

We need to talk about all the stuff we got going.

speaker3：[00:31:40 - 00:31:53]

And I think we probably need a dozen more things in our client experience command center as proven commoditized tools that then we can start looking at, okay, how do we put a central UI persona based in the client experience command center that taps into the skills?

speaker1：[00:31:53 - 00:31:54]

So what would you?

speaker3：[00:31:54 - 00:31:56]

But we need to think about building it in that way.

speaker1：[00:31:56 - 00:32:05]

I mean, as far as next steps, I feel like a low-hanging fruit, the gauge is basically ready to go, is if We hit Vivec and said, Make those uploads real.

speaker1：[00:32:05 - 00:32:14]

From there, we can immediately start supporting our leaders, and Gage can prescriptively walk them through, and then we can evolve the command center.

speaker3：[00:32:14 - 00:32:18]

Well, and I think this becomes a feeder source into this.

speaker1：[00:32:19 - 00:32:20]

It does. It all connects.

speaker3：[00:32:20 - 00:32:22]

All you do is tap it in.

speaker1：[00:32:22 - 00:32:23]

I'll explain that.

speaker3：[00:32:24 - 00:32:27]

I don't actually want to go do all of that. I just want that to be my.

speaker3：[00:32:28 - 00:32:37]

my data, and then I ask my questions about, tell me about this solution, blah, blah, and it spits it out in the format that I ask. And the format I ask might be in HTML.

speaker3：[00:32:38 - 00:32:39]

And it just displays it right there.

speaker1：[00:32:39 - 00:32:43]

The data slicing that you have there is client. He's solutions.

speaker1：[00:32:43 - 00:32:52]

You take a client slice of that and stick it over there, and now the client success people have an immediate list of, hey, right at home, I got 50 call examples.

speaker3：[00:32:52 - 00:32:55]

He just happens to not be showing client name in there though. Exactly.

speaker3：[00:32:55 - 00:32:57]

It's already there. You could pull in client name.

speaker5：[00:32:58 - 00:33:00]

It is in here actually. There you go.

speaker5：[00:33:00 - 00:33:00]

Boom.

speaker3：[00:33:00 - 00:33:04]

So we're already pulling this data in. We're pulling it in from a different context.

speaker3：[00:33:04 - 00:33:12]

So it's before it processes in this aggregated view. Which means we probably need the case data that feeds this to just be that.

speaker3：[00:33:13 - 00:33:17]

Not be the other pieces because that's the complete set that connects up the calls. It is.

speaker3：[00:33:17 - 00:33:22]

So we'd have to change that, but that becomes the visualization. You and I got to jump.

speaker3：[00:33:22 - 00:33:23]

What do we what do we product demo.

speaker5：[00:33:24 - 00:33:24]

Oh, that's right.

speaker1：[00:33:25 - 00:33:25]

Yeah. Okay.

speaker1：[00:33:26 - 00:33:26]

Hey, great job.

speaker3：[00:33:27 - 00:33:28]

Thank you. Thanks.

speaker3：[00:33:29 - 00:33:29]

And there you have it.
