---
fileClass: note
type: note
created_date: 2026-06-08T00:00:00.000Z
notes_status: Reviewed
meta: []
topics:
  - '[[TPC - FY27 Containment Strategy]]'
entities:
  - '[[Vivek Pissay]]'
  - '[[Balki Nakshatrala]]'
  - '[[Abhirup Dash]]'
  - '[[Michael Proffer]]'
  - '[[Katie Rogers]]'
  - '[[05-Entities/Jarrad Weinzerl]]'
---

# My Notes
## Docs
[Meta Data + Graph DB Design.docx](https://wellskycorp-my.sharepoint.com/:w:/g/personal/ryan_dunn_wellsky_com/IQB4OCfNKoBoQppSS5BhfV4dATgVdLLXmgEVKGCPFGv4q6E?e=WCnIcT)

## Teams Meeting
https://teams.microsoft.com/l/meetup-join/19%3ameeting_MjcyYjljYTktZTA1OC00MzdjLWEzOTctNjE0YWYyOTZkMjVi%40thread.v2/0?context=%7b%22Tid%22%3a%2215d19784-ad58-4a57-a66f-ad1c0f826a45%22%2c%22Oid%22%3a%22e0718bbb-c61f-432e-ba89-322afbe87067%22%7d

## Notes
* Vectorization - helps with size of documents consumping to model
* ~~==ACTION - Balki - requested more details, review transcript
	* "not good" metrics
	* I'm sending documents
	* Send list to meeting peeps
* ~~==ACTION - Abhriup - owns alignment and convo's with Vivek and Balki
	* after I send the documentation out, note to group that Abhriup owns from here forward. 

# Transcript

speaker1：[00:00:00 - 00:00:04]

Jeff, we are seeing more and more of you on these calls.

speaker2：[00:00:05 - 00:00:09]

Well, Ryan, so I felt it'd be rude of me not to come.

speaker2：[00:00:12 - 00:00:22]

Just as long as you know I provide very little value being new and I'll chime in if there is something of value, but at this stage I do mostly listening.

speaker3：[00:00:23 - 00:00:24]

All good. Glad to have you.

speaker4：[00:00:25 - 00:00:25]

Thank you.

speaker3：[00:00:28 - 00:00:37]

All right, let's see here. Vivek, I don't think, I looked a beer up in, I don't think he's coming, so I'm going to get going unless you got any concerns here.

speaker3：[00:00:39 - 00:00:41]

I'm sorry, I'm at Bulky.

speaker4：[00:00:44 - 00:00:46]

So I'm just.

speaker3：[00:00:46 - 00:00:47]

Okay, all right, cool. Okay.

speaker3：[00:00:47 - 00:00:47]

He.

speaker4：[00:00:48 - 00:00:49]

Might not attack.

speaker3：[00:00:50 - 00:00:51]

I don't know. All good.

speaker3：[00:00:51 - 00:00:56]

Well, I think all I'm kind of saying is I think we got everybody but Bulky, so I'm going to get going if that's cool.

speaker3：[00:00:57 - 00:01:07]

Okay, I just threw Jeff and Scott, I threw a document into chat which gives a little bit of context of kind of the why behind everything.

speaker3：[00:01:07 - 00:01:11]

So no reason to read it now, but I think it's just context for the conversation.

speaker3：[00:01:14 - 00:01:46]

Okay, so I think what I'm looking to get out of this is a Vivek and a Birup. I think what I'm looking to get out of this meeting is the kind of architectural alignment and a technical implementation that aligns with Michael's team, the problem management team's ability, I'll use the word to enrich content from technical writing, to facilitate control in the Gen. AI model.

speaker3：[00:01:46 - 00:02:09]

So kind of what I'm saying is like, if we were to add a metadata field that somehow was like authority or weight, and we were going to add that to the technical writing documents, we would be able to, as a very simplified version, say, OK, well, we're putting a weight of 10, you know what I mean, on this particular document because it's super important. We get a ton of questions about it.

speaker3：[00:02:09 - 00:02:16]

And so we want the model to basically reference this document from a more authority, have more authority versus other content.

speaker3：[00:02:16 - 00:02:24]

That would allow Tom and Gage to, in a sense, tune the content with respect to the AI model to be more accurate.

speaker3：[00:02:24 - 00:02:38]

And so Abhirup and I have spent a decent amount of time in this document outlines the flow of how we want to have the technical writers and we're going to move them to Markdown and then move the Markdown and you know what I mean basically facilitate that whole that whole data pipeline.

speaker3：[00:02:39 - 00:02:47]

But I think my question is really about like the I think Vivek the right way to tune a graph database I guess is probably if I'm trying to be direct about it.

speaker3：[00:02:48 - 00:03:12]

And if I was to enrich the Markdown files in some way how could I translate that enrichment all the way down to where the model's consuming it out the graph database and in a way where I'm empowering Tom and Gage with levers to just simply like make the thing work better, if that makes sense. So I'll just kind of, that's kind of the context.

speaker3：[00:03:12 - 00:03:13]

I'll just kind of pause there. Does that land?

speaker4：[00:03:15 - 00:03:23]

Yeah, so Tom and Gage, when they use this. What are we going to create here?

speaker4：[00:03:24 - 00:03:33]

What are we enabling them for? Are we enabling them for to go look for like content or like what would be the from a functionality sample?

speaker4：[00:03:33 - 00:03:35]

What do you want it to be?

speaker3：[00:03:35 - 00:03:46]

I would in my head Vivek, it would look like on the when we create the markdown editor for the technical writers, so that would be the new tool where they author content.

speaker3：[00:03:48 - 00:04:04]

We would, for all the pages that they have where they're writing content, there would simply, in my head, be another section for every single content, just like it would kind of have a title. Under the title, it would have a metadata section.

speaker3：[00:04:04 - 00:04:14]

And that would be where Tom and Gage could manipulate the weights in that metadata section. And there simply would be voluntary for every piece of content.

speaker3：[00:04:14 - 00:04:21]

Because they wouldn't necessarily want to enrich every piece of content, but they would want to hit the strategic ones and bolster it that way.

speaker3：[00:04:22 - 00:04:34]

And so then my thought would be in the same editor that the technical writers are just simply writing content so that the output becomes markdown, we would add a feature to that editor that would allow metadata enrichment.

speaker4：[00:04:37 - 00:04:39]

And once you enrich this metadata, what happens after that?

speaker3：[00:04:40 - 00:04:46]

So then after we enrich the metadata, so then they hit save, right? They're on their little editor and they hit save.

speaker3：[00:04:47 - 00:04:53]

When they hit save, that creates a markdown file. So it writes the markdown file somewhere, arbitrarily.

speaker3：[00:04:53 - 00:05:05]

And then when that markdown file gets ingested into a relational database, then that metadata would get carried over correctly. So I don't want to say more than that.

speaker3：[00:05:05 - 00:05:09]

I'd say a beer up that's kind of more on the ETL side, but the point is it carries across.

speaker3：[00:05:10 - 00:05:17]

And then Vivek then, and in fact here, I'm going to share this screen because this is, for me, this is the visual that I'm looking at, so might as well just share it.

speaker3：[00:05:20 - 00:05:28]

So my thought is, here's a technical editor where we're adding the metadata enrichment. When you hit save, it publishes it to a markdown file.

speaker3：[00:05:28 - 00:05:34]

So then it's just a text file, but the text file has the metadata inside. We're going to ingest that into a relational database.

speaker3：[00:05:35 - 00:05:43]

And then that relational database gets over here, Vivek, which is where you come in. We can ignore the orange for the context of this conversation.

speaker3：[00:05:45 - 00:05:47]

Does that does that give you the context you're looking for?

speaker4：[00:05:49 - 00:06:01]

Yeah, and then it would be on like agents or even like searching for articles is kind of like what you're looking.

speaker4：[00:06:02 - 00:06:12]

The thing that I'm wondering about is do we really need like a relational database there or there's a way to manage this because it's unstructured data?

speaker3：[00:06:13 - 00:06:16]

Yeah, so I think, hey, how are you?

speaker5：[00:06:17 - 00:06:20]

Hey, I'm doing good. Sorry, just back-to-back after a small break.

speaker3：[00:06:21 - 00:06:33]

No worries, no worries. The requirement of the relational database is simply so that I have a path to build our legacy documents, so if we can fulfill that requirement.

speaker3：[00:06:34 - 00:06:48]

a different way I'm all good. I just simply need to make sure that I can build a CRC static website and rebuild all the legacy PDFs using the same, basically creating parity with the technical writing deliverables today.

speaker3：[00:06:49 - 00:06:51]

So that's my only reason for the relational database.

speaker4：[00:06:51 - 00:07:00]

So it's more of just a mapping table. between like your previous legacy document and the new documents that essentially that's about it and nothing else.

speaker3：[00:07:01 - 00:07:09]

Yeah, it's just this literal path I've got right here on this screen. So it just creates a path where I can say, oh, I maintain parity with all my legacy deliverables, right?

speaker3：[00:07:10 - 00:07:19]

Websites and PDFs. So the rational database, when the technical writers write the document, you know, my thought is like, let's say that they build it by paragraph.

speaker3：[00:07:19 - 00:07:26]

We'd sequentially put that into the relational database so then we could rebuild a document very cleanly.

speaker3：[00:07:26 - 00:07:39]

So that's the only reason for the relational database. If you have a different way where the technical writers can author content and support both use cases at this level, which is Gen.

speaker3：[00:07:39 - 00:07:44]

AI consumption and the PDFs and websites of the static content, I'm good.

speaker5：[00:07:47 - 00:07:57]

Just in same line as what Vivek is asking, I just took a quick look. Most of the information is just documents, right?

speaker5：[00:07:57 - 00:08:02]

There's no real structured data needed here. Is that correct?

speaker5：[00:08:02 - 00:08:04]

It's all content.

speaker4：[00:08:04 - 00:08:05]

Yeah, it's all unstructured.

speaker3：[00:08:06 - 00:08:07]

Yep, correct.

speaker5：[00:08:07 - 00:08:11]

Then I think what Vivek said kind of makes sense.

speaker5：[00:08:15 - 00:08:43]

If you have to create a graph, it might be even easier to have BigQuery have the chunks of processed documents, so I think the maybe one question ran is, can we make the spec more about like the what I think it's there, I haven't fully read it, but more about the.

speaker5：[00:08:44 - 00:08:52]

What we want, because I think then we can, we know that we have flexibility to change this diagram, right? So I think that's the main thing.

speaker5：[00:08:52 - 00:09:06]

Like, say, for example, you might say requirements are, hey, it's possible these documents get updated, so the how does graph update the incrementally latest information, right? Will it?

speaker5：[00:09:07 - 00:09:14]

I think we need to capture some of that I think is going to impact the way the graphs have to be maintained and the agent should work.

speaker3：[00:09:15 - 00:09:20]

Yeah, and bulky, I think that's very much the reason for this meeting. We are greenfield, haven't made anything yet.

speaker3：[00:09:21 - 00:09:25]

I've got a beer up pretty much aligned with me on at least my initial vision.

speaker3：[00:09:25 - 00:09:29]

We are very much at the scoping part of this, so this is good timing, bulky.

speaker3：[00:09:30 - 00:09:39]

But I think just to be very simple about it, I'm just trying to maintain the old things that tech writing is doing, but making it design Gen. AI first.

speaker3：[00:09:40 - 00:09:47]

And I'm just trying to fulfill those two use cases, which ultimately is just my simplistic way of throwing that relational database in, because I'm like, I know I could do both.

speaker3：[00:09:47 - 00:09:53]

And so Balki, if you can retool that in a way where it's more optimized, I'm all for it.

speaker4：[00:09:54 - 00:09:59]

Yeah, we might, correct me if I'm wrong, but we might be able to build something like...

speaker4：[00:10:03 - 00:10:08]

the RAG engine or whatever on top of it, and we should be able to read that, right? If we go ahead.

speaker5：[00:10:08 - 00:10:31]

No, in fact, I did experiment with the Andre, Karpathy, Zalal and Vicky, and few other variants of the graph RAG, and that's why I wanted to say that we don't need relational from those type of solutions as I see it, but I think Patrick has a question before we, I put you on this topic. You're on mute.

speaker6：[00:10:40 - 00:10:50]

So, Balky, the copywriter stuff is already doing a graph in memory.

speaker6：[00:10:52 - 00:11:01]

So, it's already doing vectorization and chunking out the files in memory. So, really, the hard lift is already done.

speaker6：[00:11:01 - 00:11:05]

It's just a matter of where we can save it as opposed to a beam in this read.

speaker5：[00:11:08 - 00:11:14]

But that's only one part, right? When I see the document, there are other types of documents also, I believe, here, right?

speaker5：[00:11:14 - 00:11:16]

It's not just that. Is that correct?

speaker3：[00:11:18 - 00:11:23]

Yeah, I've got, so high level, I've got basically 2 categories of documents I'm producing.

speaker3：[00:11:23 - 00:11:31]

One is HTML, and then the other is PDF, and then of the PDF, I've got a lot of variety. I've got user guides, release notes, knowledge articles, all kinds of stuff.

speaker7：[00:11:35 - 00:11:44]

Just real quick comment on size of those PDF on HTML, and maybe Patrick, you covered that a little bit, but they can, they can get very, very long.

speaker7：[00:11:45 - 00:11:48]

So just stating that, but Patrick, I think you might have covered for it anyway, I may not.

speaker6：[00:11:50 - 00:12:00]

And that's literally the reason why we are already doing vectorization in graph is that files are way too big to be helpful within just traditional LLM.

speaker6：[00:12:01 - 00:12:05]

So we're doing vectorization there, and I currently can handle up to 200 megabytes.

speaker6：[00:12:06 - 00:12:10]

I haven't tried any file anything bigger, but 200 works just fine.

speaker4：[00:12:10 - 00:12:19]

And I don't know if you had something. Yes, I have two questions.

speaker4：[00:12:19 - 00:12:23]

The first one is, what is the primary outcome of this metadata?

speaker4：[00:12:24 - 00:12:34]

Are we looking for better GNI answers or document discovery, agent routing or content governance? What exactly are you trying to do as a primary outcome of this?

speaker4：[00:12:36 - 00:12:41]

I think that's what Barki was asking, right? start with the end in mind, right?

speaker4：[00:12:41 - 00:12:47]

Let's identify like 2, three of three to five use cases that we want to address with this.

speaker4：[00:12:47 - 00:12:58]

Then what we can do is we experiment with a few documents and then we can try out a few options here, right?

speaker4：[00:12:58 - 00:13:02]

Like there are different ways we can address this, try out like what's going to serve a purpose.

speaker4：[00:13:03 - 00:13:07]

And also we need to think about what is the end goal?

speaker4：[00:13:07 - 00:13:13]

Is it going to be a custom app or do we want to go the Gemini Enterprise route and see what works the best?

speaker1：[00:13:13 - 00:13:13]

Yeah.

speaker5：[00:13:14 - 00:13:22]

I think, wait, that's right. I would start with, and I think Patrick's question kind of further made it clear for me.

speaker5：[00:13:23 - 00:13:27]

What is the current location and the process that works? Sure.

speaker5：[00:13:27 - 00:13:38]

So it's like showing, we have content people here, if they do something on a daily basis, it goes here, then these other people who are doing knowledge based articles, based articles, then it goes.

speaker5：[00:13:38 - 00:13:46]

So I think we should just map the flow of information. And finally, the use of it, right?

speaker5：[00:13:46 - 00:13:57]

Okay, the use is a chat in the, I don't know, client support tool, or is it something else, query tool? Where is it then actually this flow being used?

speaker5：[00:13:57 - 00:14:07]

Is it by clients or only our support people? So I think just let's highlight the process diagram and highlight what systems or what information and also the frequency of updates and stuff like that.

speaker5：[00:14:07 - 00:14:16]

And then finally, the last thing is when we show who then needs to use it, That's the point where we want to capture goals.

speaker5：[00:14:16 - 00:14:20]

That means today, here is why this is not good.

speaker5：[00:14:21 - 00:14:31]

So for example, it might say that there's a lag of 30 days before they see latest information, this user, end user. We need to bring it down to five days.

speaker5：[00:14:32 - 00:14:40]

So I think... I call them as metrics of what is not good about the current place where this information is being used that we want to improve.

speaker5：[00:14:40 - 00:14:49]

It could be also around accuracy or something like that, right? Accuracy means in a top five article should be relevant or something I'm making up.

speaker5：[00:14:49 - 00:15:00]

But I think once we do that, it will become very clear, oh, these are the systems and here is the goals we want. then we will know how to design the thing.

speaker5：[00:15:01 - 00:15:05]

And then one last thing to also highlight there is what's the volume usage there, right?

speaker5：[00:15:05 - 00:15:12]

So for example, if the volume is very low, we can even go with some higher costly model versus something cheaper.

speaker5：[00:15:12 - 00:15:20]

So I think those are the things that come to my mind as to capturing the input you're looking for, and then we'll know how to design it.

speaker3：[00:15:21 - 00:15:22]

Sure. So bulky, I'll.

speaker4：[00:15:23 - 00:15:41]

Before, because my second question was exactly something similar to, because the authoritative source of truth that you're mentioning, which one will be, I mean, the markdown file, relational database, or the graph DB, or BigQuery, or GCP, or the existing content that we already have?

speaker4：[00:15:42 - 00:15:46]

So that is something I was also planning to ask you for the one source.

speaker3：[00:15:48 - 00:15:55]

A bear up on that, I'd say that the alignment in this meeting would determine the answer to that question. So I'd say that that's kind of architecturally dependent.

speaker3：[00:15:55 - 00:16:06]

Bulky, back to, you know, your asks on, I'll say current state and then issues with the current state and then our future desired state. Yeah, I'll be more than happy to put all that together.

speaker3：[00:16:07 - 00:16:28]

I think bulky, I think I do want to highlight though, this is not an effort to Address a particular efficiency gap this is more of a fundamental foundational strategy that I'm attempting to kind of build against, our longer-term client experience support models, and so I think, absolutely.

speaker5：[00:16:28 - 00:16:33]

I think I know that, but I was saying that even that when we force our to say...

speaker5：[00:16:35 - 00:16:46]

The strategic thing is to because of I want to reduce the time lag or the automated process, the number of human interventions or the quality. Usually it comes down to three or four such metrics.

speaker5：[00:16:46 - 00:16:50]

I think it will help us to better design the...

speaker3：[00:16:50 - 00:16:52]

Sure. Oh, 100%.

speaker3：[00:16:52 - 00:16:54]

And I'll be bulky. I think they're great questions.

speaker3：[00:16:54 - 00:16:57]

I'll get all that to you. But I think I just want to say it out loud.

speaker3：[00:16:57 - 00:17:04]

I just feel better because I mean, like, you know, new working with Jeff and bulky, we haven't done a lot together either. So I just felt better about it.

speaker3：[00:17:04 - 00:17:11]

for context. The other thing I kind of want to say out loud just for my own anxiety, Michael Proffer's role in this is critical.

speaker3：[00:17:11 - 00:17:13]

The Gen. AI agents, bulky, it's exactly your question.

speaker3：[00:17:13 - 00:17:15]

So you're spot on. The Gen.

speaker3：[00:17:15 - 00:17:22]

AI agent at the bottom, the public facing consumption of that is the Gemini for client experience.

speaker3：[00:17:22 - 00:17:31]

So while we probably do, and I'll put all of this together, so I'll get, formally I'm going to get you all this bulky, but I just want to say out loud, we're going to have some internal use cases of this graph.

speaker3：[00:17:32 - 00:17:40]

and I think there's gonna be lots of them, but I think there's also a very, very high volume, high scale, public facing use case of a model.

speaker3：[00:17:40 - 00:17:51]

And I just, so when you were talking about do we use a Gemini model or something else, I just wanted to be clear that integration to our call center is critical too, just so it wasn't a surprise. Cool.

speaker3：[00:17:52 - 00:17:54]

Okay. then tell you what, I am more than happy then, Bulky.

speaker3：[00:17:54 - 00:18:02]

Let me, and in fact, Bulky, I think I'm going to do a little, I think I'm going to do one better. I'm going to put a document together that gives the entire strategy top to bottom.

speaker3：[00:18:03 - 00:18:08]

I'll try and not make it confusing, but it's going to give you the entire path of even current.

speaker5：[00:18:08 - 00:18:15]

Process diagram and current places of use and the challenge. And then after that, the strategy.

speaker5：[00:18:15 - 00:18:18]

I think the current, probably the most important. Yeah.

speaker3：[00:18:18 - 00:18:19]

Sure. Okay.

speaker3：[00:18:20 - 00:18:21]

No, happy to do that. So.

speaker3：[00:18:22 - 00:18:24]

great. Then I will do that.

speaker3：[00:18:25 - 00:18:29]

I think then maybe saying this out loud just to keep everybody aligned.

speaker3：[00:18:29 - 00:18:37]

As I do that, I think I'm looking for a BIRUP to get aligned with, I'll say, Vivek and Bulky from a design perspective on enterprise.

speaker3：[00:18:37 - 00:18:43]

And so I think however that lands, I think this is also just me being clear. I don't want to create a shadow ID.

speaker3：[00:18:43 - 00:18:47]

So you guys tell me where things need to live. We'll work together on that.

speaker3：[00:18:47 - 00:18:58]

But then ultimately, I think I'm looking for a BREPS alignment, because then a BREPS is going to help on a number of different tools and initiatives that are going to be critical that we're all aligned on the architecture.

speaker3：[00:18:58 - 00:19:10]

So I think that's kind of the goal I'm looking for, so that we, like I said, bulky, it's kind of a number of different work streams, but this is all great. This is perfectly timely, and I think this is the exact right next step.

speaker3：[00:19:11 - 00:19:12]

Cool. OK.

speaker5：[00:19:18 - 00:19:30]

As soon as we have the document, do an experiment of other things I can share, and then it's not like only one person has to do, so we can have different people experiment it, and then it'll inform us of the architecture.

speaker3：[00:19:31 - 00:19:36]

That's great, that's great. So then one other thing I'll throw out here to tie together the Salesforce folks.

speaker3：[00:19:37 - 00:19:44]

So one of the reasons that Jeff and Katie are here, I think I saw Scott earlier, was, yeah, there's Scott.

speaker3：[00:19:45 - 00:19:57]

So one of the reasons that I looped those folks in was because bulky, I wanted to make sure they were aligned because what we're doing is integrating Salesforce cases. Again, one more use case right against kind of this potential graph.

speaker3：[00:19:57 - 00:20:04]

And so I think for the Salesforce folks, I think this is to just say near term. I think we're totally aligned to move forward.

speaker3：[00:20:04 - 00:20:09]

I don't think there's any major pivots here. So just kind of stating that formally.

speaker3：[00:20:09 - 00:20:17]

So Jared, our first responder agent in the meetings that we had on Friday, Personally, I'm saying all good to go, no architectural issues.

speaker3：[00:20:17 - 00:20:22]

And then also saying as we uplift this, we'll keep everybody tight.

speaker3：[00:20:22 - 00:20:31]

But ultimately, I think, Patrick, your work with the Salesforce team is going to self-serve that because you're going to make sure that you're going to take the AI side of that anyway.

speaker3：[00:20:31 - 00:20:35]

So kind of just saying, I think we're all aligned, but I just want to say out loud kind of how the whole thing fits together.

speaker4：[00:20:37 - 00:20:42]

I want to have a discussion with you, so I'll get in touch with you on that one.

speaker3：[00:20:42 - 00:20:50]

Cool, yeah, all good, all good. We're all, this is all, there's a lot of, I think, work I'm representing, but so this is just getting everybody aligned.

speaker3：[00:20:50 - 00:21:01]

So I think we're in good shape because I was more worried about people starting before we had all the details, and I think we're landing it well where, you know what I mean, nobody's got any wasted work yet. So cool.

speaker3：[00:21:01 - 00:21:04]

Okay, well then that's everything I had to cover. I'll say action items on me.

speaker3：[00:21:05 - 00:21:12]

I will follow up. I'll just do it to this meeting group with bulky, the deliverables that you asked for.

speaker3：[00:21:12 - 00:21:21]

And then from there, I think, Abhirap, I'll probably hand it over to you to make sure that we get architecturally aligned, and I'll jump into meetings as necessary. So that sound good with everybody.

speaker6：[00:21:23 - 00:21:33]

Bulky, so you know, on the Salesforce side of things, we're also doing graph vectorization on those as well, not because of the size of the board.

speaker6：[00:21:33 - 00:21:49]

The files are actually quite small, but because there's such varied content, there's emails, there's chats, there's comments, there's actual case information, so since the data is so varied, I as well, so.

speaker5：[00:21:51 - 00:22:00]

Yeah, we can talk in a technical meeting, but when you say being vectorized, I mean the way...

speaker5：[00:22:01 - 00:22:11]

You do that is you just drop all the documents in some place and then you create a RAG in place which does all the vectorization checking and that kind of logic. Is that what you mean or you mean something else?

speaker6：[00:22:11 - 00:22:16]

Yeah, that is, but it's been shown because it's being saved to, it was originally Chrome, but now it's CG.

speaker6：[00:22:17 - 00:22:34]

So if it's just in memory stored at runtime and then disappears after it's ran, I think Ryan's wanting to go is to have that persist so that way we can look through it at any time. Does not happen to the upload and wait for that process.

speaker5：[00:22:35 - 00:22:40]

What is the tool that is requiring that in-memory vectorization or whatever?

speaker6：[00:22:41 - 00:22:47]

So it's our command service. I mean the tool that...

speaker6：[00:22:47 - 00:22:49]

We're using it in, it's no.

speaker5：[00:22:49 - 00:22:58]

Yeah, like if you use the work of vectorizing or whatever, for what use case was it implemented, the in-memory thing?

speaker6：[00:22:58 - 00:23:17]

It's for our so we have two currently, one is a case auditor, basically audits a case to make sure that everything scores how well we did on it, and then the other use case is for the tech writers doing release notes, so they upload.

speaker6：[00:23:17 - 00:23:25]

a 150 MB file and they need to know I have these 50 new things that need to go in this file, where does it go in that file?

speaker6：[00:23:26 - 00:23:31]

And then how do I match the language according to that file and all that kind of thing? So, got it.

speaker5：[00:23:31 - 00:23:35]

Okay, so then that's perfect. That's where RAG will come in and comes in perfectly.

speaker4：[00:23:36 - 00:23:38]

Yeah, makes sense.

speaker6：[00:23:39 - 00:23:50]

Nice, and let you know before I implemented full vectorization, we were getting about 70% accuracy, and then once we did, we had about ninety-five percent accuracy, so very, very, very helpful.

speaker5：[00:23:51 - 00:24:00]

And do we right now on a regular basis think Salesforce to any BigQuery GCS or anything like that today?

speaker4：[00:24:01 - 00:24:06]

No, we do it bulky, it's a nightly load, so it covers.

speaker4：[00:24:07 - 00:24:31]

Lot of objects, but not all objects, so whatever use cases that we have we bring in into that query, but if we're looking for something stressful, no, I don't think so it's moving any of his, I think we would need to figure out how to move those things.

speaker4：[00:24:33 - 00:24:38]

Yeah, so that's what we're going to talk about, creating a persistent storage.

speaker4：[00:24:38 - 00:24:43]

We're thinking that the BigQuery on GCS being the better option, so we're working through that.

speaker6：[00:24:44 - 00:24:49]

And also, so you know, Balki, that's two of the use cases for RAG.

speaker6：[00:24:50 - 00:24:55]

Jim has a whole bunch of others that he's been working on that you have to ask him about.

speaker6：[00:24:55 - 00:25:03]

And then I just talked to Katie Phillips about two hours ago, and she has one that's going to need a RAG engine into this.

speaker3：[00:25:11 - 00:25:12]

Great. Great.

speaker3：[00:25:12 - 00:25:16]

Okay. then I think, like I said, I think we're aligned next steps in my court.

speaker3：[00:25:16 - 00:25:22]

I'll probably make sure and align the whole document with you before I send out, just so then that way, you know what I mean?

speaker3：[00:25:22 - 00:25:29]

It just keeps every, in case I miss anything or anything you'd want to add or stuff like that, and then we'll get over to the rest of the team and go from there. So very cool.

speaker3：[00:25:31 - 00:25:33]

All right. Well, I appreciate everybody's time.

speaker3：[00:25:33 - 00:25:33]

Thank you very much.

speaker6：[00:25:34 - 00:25:35]

Have a good one.

speaker4：[00:25:35 - 00:25:36]

Thank you.