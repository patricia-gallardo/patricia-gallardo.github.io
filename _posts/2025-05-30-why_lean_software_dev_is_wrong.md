---
title: Why GUIs are built at least 2.5 times
description: Or Why I Think Lean Software Development is Wrong
author: Patricia Aas
layout: post
icon: fa-pencil
image: "/assets/images/face.500.jpg"
---

Over the past few days I've been writing on LinkedIn ([here][4] and [here][5]) and Mastodon ([here][6]), and this post is an attempt to explain better (?) or at least in one place, what I have been trying to express, but now in a less stream-of-consciousness manner.

I want to start with three different things that seem wildly disconnected, but are in my mind connected:

1. Robert Smallshire replied to me on [LinkedIn][7]: "I wish we could get away from trying to describe and understand software intensive systems and development processes through analogy with factories/gardens/farms/sports/whatever and deal with software on its own terms."

2. Peter Sommerlad replied to me on [Mastodon][1]: "are you equalling "factory" as a program metaphor to the "Pipes and Filters" architectural pattern that we described in Pattern-oriented Software Architecture \#POSA1?"

3. And something I tend to say: GUIs are built at least 2.5 times

## Hope

I share Smallshire's wish. Ideally, I would've liked it if we could "deal with software on its own terms", and I have, perhaps naively, thought that we had gotten to something in that realm. However, I am starting to wonder if we are not only not there, we are so far off we're not even speaking the same language anymore. So by breaking everything in his plea, I will try to make a step towards his wish.

## Architecture: The Factory

### The "Pipes and Filters" Architectural Pattern

I want to start with Sommerlad's observation, because to my dis-credit I didn't know this had a name, and names are useful. So let's have a look because there are a few aspects of this that don't completely fit what I will describe in this post, but I think it's a great start. By the way, this post will be long and surprisingly technical, but not meant for a particularly technical audience. That will be a challenge.

In programming we have seen the emergence of common ways to solve a problem, we often call these patterns. I have learned recently that in psychology they have a word for this (or something similar) called [*"schema"*][2] (which conveniently is something completely different in programming, but oh well).

Books have been written on patterns, and sometimes that causes us programmers to go overboard in using them, but that also is a debate for another day.

This particular pattern is so common in programming that we generally don't think much about it. It has been present in programming for at least half a century. It is present as a core feature of the Unix/Linux command line. It's basically that what I produce as output can be someone else's input. Which means you can line us up and one program/function/whatever can take something, do something to it, and hand the result off.

In functional programming there are lots of concepts around this like map, reduce, filter, transform etc. These operations represent what we do with our input, which is usually in the form of a collection of similar things.

In a physical "factory" you could think of this as maybe a production line (I don't know anything about factories, so forgive me). One machine takes in something and transforms it somehow, and hands it off to another machine that might sort out undesirable things etc.

That doesn't fit exactly, because in "Pipes and Filters" we imagine that the kind of thing that goes in is the kind of thing that goes out. But I think this is us just being slightly imprecise because when we say "same" that is in shape, not in meaning.

So imagine a pipeline that takes in encrypted text and the first "filter" decrypts the text, the second takes the decrypted text and strips away the beginning and the end, the third takes its input and sends it in an email.

However this is 1 input to 1 input, and that is a simplification. Most of the time that's not actually how even *these* things work.

### The "Pads, Sources and Sinks" and "Signals and Slots" Architectural Patterns

I don't know if these patterns are in a book, or have a name, but if not, they are now in a blogpost, and therefore, by the authority invested in the internet, they are hereby named. These two patterns show something a bit more complicated (and are variants over the same theme), though I do think that some of this exists under the *"Pipes and Filters"* label in the wild.

One of these *"filters"*, from here on we'll call them *nodes*, can have both many inputs and many outputs. It is also the case that they may not be freely "composable", meaning that the output of one might not be suitable as the input of another. For example, a *node* (you can think of this as a program) that consumes jpeg's and converts them to png's which it outputs, might not accept png's as its input.

In this pattern an *input-pad* (or a *slot*) is where you get your input, and an *output-pad* (or a *signal*) is where you can hook up to get the output of the node. A node in such a network (which we confusingly tend to call graphs) can have zero or many *input-pads* and zero or many *output-pads*. Something that has no *input-pad* we often call a *source*, and something that has no *output-pad* we call a *sink*. A quite popular open source project with this type of architecture is ffmpeg, which is used to process and compose various media like video and audio.

So you can imagine a factory as a network of such nodes, where all the *source* nodes are *"parts"* and the *sink* nodes are *"products"*. The purpose of such a network is to take *"parts"* and transform them into *"products"* (cars in TPS).

### This Pattern Exists Everywhere in Software Development

An example from software architecture that is present in TPS (Toyota Production System or Lean) is triple buffering: 

> *"In triple buffering, the program has two back buffers and can immediately start drawing in the one that is not involved in such copying. The third buffer, the front buffer, is read by the graphics card to display the image on the monitor. Once the image has been sent to the monitor, the front buffer is flipped with (or copied from) the back buffer holding the most recent complete image. Since one of the back buffers is always complete, the graphics card never has to wait for the software to complete. Consequently, the software and the graphics card are completely independent and can run at their own pace. Finally, the displayed image was started without waiting for synchronization and thus with minimum lag."*
> ― Multiple buffering, [Wikipedia][3]

You can imagine this as two nodes in our network, operating in a TPS pull-like fashion (described in the original literature on *"The Factory"*), where the graphics card is pulling a frame from our node, but to make sure that the graphics card never has to wait and never gets a half filled image (containing parts of an old image and parts of a new image), we try to make sure there is always a frame ready for it to grab. We don't want to buffer much more than that, because that would mean we would start to lag behind, which would be terrible for any kind of *"real time"* experience, like games, video calls or typing text and seeing it on screen. This is where the terminology 60 fps, skipping frames, tearing, vsync etc comes from. Trying to manage this process, so it is unnoticeable for the user. *"Waste"* in this context would be a frame that arrives too late, causing the graphics card to skip it in favor of the next frame. This can give a choppy and less smooth experience, and we've spent cpu cycles creating an image we did not use. For certain media types the human brain is very sensitive. Our brains can often *"fix"* video, though we might notice in the *"feel"* of the game, for example. For audio we are often much more sensitive to these things.

The point is: variants of this architecture are well understood in the verticals that use it, for example in games.

### "The Factory" is the Program

The problem with trying to map anything to something else is that it will never match completely, and so the "metaphor breaks down". This is what, I believe, frustrates Smallshire, when he says we should "get away from [...] analogy" and "deal with software on its own terms". And that is completely valid, but I'm not sure it's possible. And I think *Lean Software Development* is a perfect example of why. People that don't understand how we work, will struggle to understand our process. And what we write is literally unreadable to them.

### DevOps: CI/CD as "The Factory"

A more well known system that uses a *"factory-like"* architecture is a CI/CD pipeline. It contains even more features of *"The Factory"*. For example, stopping the line. The idea here is to avoid producing low quality "products", in CI/CD the "products" would be "deployments" to production, we try to stop the deployment the moment we see that it is not of sufficient quality. Examples of this are tests failing in CI/CD. A CI/CD pipeline is generally of the form of a *"Pads, Sources and Sinks"* architecture. We write some code, we push it to git, it gets picked up by our CI/CD pipeline, which will pass it through a series of transformations or filters, some of which could be: check formatting, check with static analysis, check that it builds, check that it doesn't have any warnings, check that all tests pass, merge with any meta-data, package it, sign it, upload it to a package repository. From there you might have some other pipeline that pulls that package and deploys it in a test environment, runs some tests on it, and if it has made it this far, it will deploy it in production. This was DevOps. Eliminate people from this pipeline. Automate everything, make it auditable what came from where and what happened to it. In production it might still be monitored, metrics on how it behaves might be collected and sent back for analysis, maybe causing us to write more tests or checks.

This type of ripcord behavior exists in many places in programming, the most well-known (outside of DevOps) is probably exceptions and transaction rollbacks.

### It's Very Recognizable Because We Recognize It

Programmers bristle at some of this because they feel like they *Get It*. And yes, it is recognizable, it’s a very common architecture, it’s literally everywhere, most of us don't even know what it's called. That's how common it is.

However, it's not describing the way we work, it is describing the programs we write. It's everywhere, in Java/Kotlin streams, in all functional programming, on the commandline, it’s absolutely everywhere. Toyota Production System (/Lean) is extremely understandable to programmers BECAUSE IT IS A PROGRAM.

It’s a program being executed by a combination of humans and machines in an actual physical factory. But as a program it’s very basic. It’s not very complex or interesting in the field of software engineering. Which is understandable, because it’s not being run on a computer.

## If Lean Software Development ain't it, how do we actually work?

One thing I've learned over the years is that we really, really would like it to work this way. It's not just management that wants this to be clean and predictable. We work so hard at making our programs this way, we would *Absolutely Love It* if we could build our products the same way: Take *Problem*, break it down into parts, make each part, collect parts into a whole, DONE! That sounds so satisfying. Now we can just work on doing it faster!

### Then why is this so hard?

Short answer: We are not *"factories"*, we are designers of *"factories"*.

Very Long Answer:

I don’t know what it takes to *"get"* what we do, and how we do it, a lot of devs struggle to *"get it"* too. I think that is part of the reason we have struggled to find a *Better Way* to do things. What I have been starting to wonder is if the problem is the metal model we have for how it's done.

If you watch an author of fiction, they will look like a person typing. So if you don’t know what it means to write fiction, you might think that they're just typing out pages. If you want to optimize this process, you might try to optimize for them typing faster. But it isn’t typing speed that is constraining storytelling.

It isn’t typing speed that constrains developers either. We are constantly making custom work in a context, doing it well requires us to deeply understand our context. And to understand that, we need to "run experiments" (This is a weird way to say these things, but maybe a different way is good). The people who want things made for them don’t actually know precisely what they want. And even more interestingly: They quite often think they *do* know.

That’s not a failing on their part. If exactly what we’re making exists already, then they should probably use that. So what we make is pretty much always new in some way. It’s probably similar to something we have seen before, but the bit that is different is the reason we’re making it, and that’s novel. *That* we need to understand. Deeply.

People (even us) don’t fully know what we want in the abstract, but we know what we don’t want when we see it. So a thing we have learned (though we seem to need to relearn) is that the fastest way for me (and you) to figure out what you want is to give you something and listen to how it’s wrong, and based on that give you something else (or make a small adjustment) and repeat.

Like trying on shoes to find one you can wear day in and day out.

If you look at me working, it will look like I’m typing. But what I am trying to do is to express an understanding of what someone else wants. So I can show it to them in some fashion, and have them tell me I’m wrong, again and again, until suddenly I’m not.

This only looks like *"Waste"* if you don’t know what I’m doing: I’m trying to understand, deeply, what someone else wants, more than they understand themselves, because I have to explain it, *precisely*, to a computer.

I think one can understand this, even if one has never done it. This is not technical, it’s human. Imagine trying to buy the perfect gift for someone, but they could tell you honestly what they thought about it, and forget immediately. Or like that guessing game where you try to guess what someone is thinking of, but they can only say yes and no.

If you understand this process, then small "a" agile makes sense:

- we need to talk to the people who have the needs  
- we can’t be in an adversarial relationship with them  
- we need to work in small batches  
- we need to get feedback  
- we need to iterate

In this framing maybe even DevOps makes sense: we need to get stuff to our users as fast as possible, because that is our iteration loop, we need feedback. So anything that blocks that, slows everything down.

## Why Lean Software Development is Wrong

I think a big misunderstanding has been to think of Software Development as manufacturing. And I think this (possibly subconscious) notion, that software development is the manufacturing of code/features/whatever, is at the root of *Where It Went Wrong*.  Mapping Lean to other disciplines starts with trying to figure out "what is *"The Factory"*?" and "who are the workers in *"The Factory"*?". And this is where it's very easy to miss, and *Lean Software Development* missed completely in my opinion. In software development *"The Factory"* is what we are making, *"The Factory"* is the program. There are no actual people in *"The Factory"* in Software Development. *Lean Software Development* is a massive misunderstanding and so is by extension Kanban and everything else.

As a programmer, if you read Toyota Way or other books on actual TPS, you will see something that looks a lot like software development, but it's not very prominent: it's the people designing the factories and the people designing the cars (aside: look at how they design cars, they basically use libraries).

### Software doesn't behave economically as manufacturing

Software development has a weird attribute, making 1 app locally on your machine that you deploy locally to your phone as a hobby, can take days/months/years. But once it is "done" you can put it in an app store or online, and all subsequent copies are "free to produce". This is not how manufacturing works. Making item 2 and 3 has cost, in materials and labour. But in software all of, or the overwhelming amount of, cost is in making the *first* one (maybe you have some per user infrastructure etc).

So the perspective is wrong. Developers don't produce code. Developers are trying to design a solution to a problem, and that is not done in isolation, and more "stuff" isn't necessarily better. 

Like imagine you like a minimalistic style, putting more and more stuff into your house doesn't make it better, it makes it worse.

The goal isn't to write code faster, it's to make something that is valuable to someone.

So this is more like making a bespoke suit for someone. You need to try to get them to tell you what they want, you can try to show them different things they might not be familiar with, and most of the time they probably don't know what they want. So the process of making good software is about trying to find out what people want, even when they don't know themselves. That is a lot of trying stuff, a lot of iteration, a lot of back and forth. And that's not bad, that is actually optimal. The point is not to make a suit, the point is to make a suit that they will love.

Another weird thing is that sometimes, if we do it really well, you can't even say what is good. It just *Feels Right*. Like *Obviously This Is How It Had To Be*.

The manufacturing perspective just doesn't fit: we have no material cost (copies are free), we have no labour cost for manufacturing (copies are free), we don't need a factory (copies can be made on a laptop). This is a very different thing than the manufacturing of physical things. It's even different from the design process for manufacturing of physical things, because you can design a bridge, but building the bridge still costs money. And so does the next bridge from that same design. That's not software.

Another weird thing about software is that we can fundamentally change it after it's "done". Even after the customer has it. We can continue to change it, for decades and decades.

I sometimes compare it to trying to make a garden, it's never done, but it's still here, some years it's better than others and some years it actually might get worse.

## What does this have to do with GUIs?

Of all the things we build, the part that our users actually see and experience are the hardest to get right. Why? Because it comes down to extremely subjective experiences. And phrases like "usability" and "learnability" show up, but also things like "ugly" or "confusing".

I have made GUIs many, many times and my best case scenario goes something like:

1. A design has been made, everyone loves it. Detailed drawings have been made.  
2. The devs are told to *Make It*  
3. The devs *Make It*, exactly to spec  
4. Everyone looks at it and everyone hates it  
5. So many meetings. So much stress. This Is Terrible! What To Do?  
6. A new design is made. So much better! Detailed drawings are made.  
7. The devs are told to *Make It*  
8. The devs *Make It*, exactly to spec  
9. Everyone looks at it and *They Do Not Love It*  
10. So many meetings. So much stress. *This Is Terrible*! *What To Do*?  
11. Someone suggests in one of the many, many meetings what amount to basically minor changes, moving something, changing some colors, changing some text, something like that.  
12. The devs *Make It*, exactly to spec  
13. Nobody's happy. But nobody hates it.  
14. The devs are pissed.

That is, in my experience, the absolute best execution time you can hope for (and it is very rare, and probably not producing *Great Products* either). I've known many people over the years who swear by Pi. Just multiply everything with 3.14. I've met people who have never been below 10.

### Why does this happen?

We like to think we know what we want, but we don't. My advice to people who want to truly *Get Good* at making computer stuff for other humans, is to accept this. Don't fight it, work with it. Like a rip current. Make peace with it. Humans can't describe what they want in sufficient detail, but boy are they good at telling you what they don't like! This is the process that small "a" agile sussed out: we need to get told what is shit really fast. This has a ton of implications, far more than I can go into here.

## Why should you care?

The point of this whole blogpost is that your mental model for "what making software is" is extremely important when trying to figure out how to "manage" it. If you think it is manufacturing you will try to *Make It Right The First Time*, *Eliminate Waste*, etc. When you realize that it is a process of discovery, of trying to find out What Is Right, you will behave completely differently. You might want to get something into users hands as fast as possible (*Minimal Viable/Valuable Product*), or run parallel experiments in production with different versions (*A/B testing*), study users using the product (*UX testing*) etc. The goal isn't to *Produce*, the goal is to find out *What We Should Build*.

Of all the worst things that happened in software dev because of *Lean Software Development*, the biggest is probably the idea of *"Waste"*. Firstly, because a metaphor is a terrible basis for a clear meaning for a word, what *"Waste"* *is* is completely subjective, and very much dependent on what you think Software Development Is. And that brings us to the second problem, it is used as a reason to undermine and sabotage Anything I Don't Like.

But thirdly, and in my not so humble opinion, most importantly: So much of what is essential for Making Great Products, will look like *"Waste"*, when viewed through a manufacturing lens.

So finally, back to Robert Smallshire: "I wish we could get away from trying to describe and understand software intensive systems and development processes through analogy with factories/gardens/farms/sports/whatever and deal with software on its own terms".

What would that mean? What would that look like? Like I've been telling countless Agile Coaches over the past few days: "How can you coach something you don't understand?". But earlier in this post I also said: "I think one can understand this, even if one has never done it. This is not technical, it’s human". However, we have spent a good two decades barely progressing in some respects, and regressing in others. I really can't decide.

Instinctively, I feel that it should be possible, but I have been reminded time and time again over the past few days of the quote: 

> "It is difficult to get a man to understand something, when his salary depends on his not understanding it."
>
> ― Upton Sinclair, I, Candidate for Governor: And How I Got Licked

PS. Yes, this whole thread is relevant to the question: will AI take my programming job? But answering that question is left as an exercise to the reader.

[1]: https://mastodon.social/@PeterSommerlad/114580794562975021
[2]: https://en.wikipedia.org/wiki/Schema_(psychology)
[3]: https://en.wikipedia.org/wiki/Multiple_buffering
[4]: https://www.linkedin.com/posts/psmaas_patricia-aas-patriciavivaldinet-activity-7333124138225635328-hXsO?utm_source=share&utm_medium=member_desktop&rcm=ACoAAAEyu2wBPniL9U_Oc3z_cJDEPgHXix7RMnA
[5]: https://www.linkedin.com/feed/update/urn:li:activity:7334012465984274432/?commentUrn=urn%3Ali%3Acomment%3A%28activity%3A7334012465984274432%2C7334093321406955520%29&dashCommentUrn=urn%3Ali%3Afsd_comment%3A%287334093321406955520%2Curn%3Ali%3Aactivity%3A7334012465984274432%29
[6]: https://social.vivaldi.net/@Patricia/114580043643778705
[7]: https://www.linkedin.com/feed/update/urn:li:activity:7333124138225635328?commentUrn=urn%3Ali%3Acomment%3A%28activity%3A7333124138225635328%2C7333195667969830914%29&dashCommentUrn=urn%3Ali%3Afsd_comment%3A%287333195667969830914%2Curn%3Ali%3Aactivity%3A7333124138225635328%29