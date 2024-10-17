---
title: Ask Why: The Pagination Problem
description: Evaluating user feedback
author: Patricia Aas
layout: post
icon: fa-pencil
image: "/assets/images/streetart-8922115_1920.500.jpg"
---

Once upon a time a dev working on a project got an urgent feature request. There are really only two types of priorities in tech: "House is on fire" and "I'll call you maybe", and this was "House is on fire" priority.

The system was a case management system, replacing a legacy system. The users had flagged that they Absolutely Could Not adopt the New System unless it had this particular feature:

__"The user has to be able to go through all open cases"__

There were at any given time thousands of open cases, with 20 cases per page this would be a hell of pagination, where the user would click to go to the next of hundreds of pages.

* This seemed excessive.
* This seemed absolutely unusable.

__The dev asks the question we should all ask:__

*"Why? What do they need it for?"*

Filtered through 4 layers of middle management there was no real explanation, only the sentiment had survived the transfer:

"IT'S REALLY IMPORTANT!! THEY CANNOT USE THE SYSTEM WITHOUT IT!!!"

So the dev asked what we should all ask:

*"Ok, sure, but what do they need it for? Maybe I can speak to one of them?"*

Middle Management were very stressed, they had been in a ton of meetings trying to get the users to get on board, and this had turned into a complete showstopper, and now the dev was refusing to do it!!! 

"JUST DO IT OK??? THEY CANNOT USE THE SYSTEM WITHOUT IT!!!"

The dev was starting to give up, but gave it one last shot:

*"I'll solve the problem, don't worry, but can I please just speak to one of the case workers? Just 30 minutes?"*

Middle Management threw up their hands and gave in: "Ok, whatever, but get to it!"

The case worker looked stressed and worried as she walked into the meeting room for the meeting with the dev, and without prompting started nervously and intently saying: "We really, really need this, we just can't use the system without it." Her voice was emotional, clearly worried that this dev would refuse.

The dev tried to put her at ease:

*"Don't worry, if this is what you need, I'll make it, I just want to know more about how you use this view, could you explain a bit about your process?"*

Slightly more at ease, she starts to explain:

Their case handling is highly regulated, and one important constraint is that they have hard deadlines for how long a case can remain in a certain state. This is something they have to be on top of at all times. So once a week a person in the team would be in charge of going through all open cases and making a note of all cases approaching their deadline. This task was incredibly tedious. To make it less frustrating, they had a rotation so that each person would only need to do this once every 1-2 months. It basically took an entire workday. But it was incredibly important. Without it, they would miss their deadlines, which was unacceptable.

The dev took notes and, when she was done explaining, thought for a bit.

"Ok, I have an idea. What if in your regular view we add a panel on the right where you can get alerts for cases that are approaching their deadlines?"

The case worker was stunned.

"Maybe we could even make some custom alerts? So you can be alerted about the kinds of cases or deadlines you are interested in? Or maybe the ones you've worked on? Would that make sense?"

Her voice was even more emotional than in the beginning: "Wait. Is that possible?"

"Sure! Then y'all don't have to do this thing anymore! What do you think? What will the other case workers think?"

"Omg, that would be amazing! This part of the job has really sucked, and it would take away the concern that we might've missed one…"

This feature became the main focus for development in the coming weeks and the case workers were extremely excited and had a lot of ideas for alerts, and the scope only grew.

And Middle management were profoundly relieved.

## So what is the lesson here?

We tend to conflate competence (or incompetence) in one area with the same in a completely different one. So if you think your users are fantastic at understanding the domain and their field, you might assume that they also know best what they need. Or inversely, if you have experienced a lot of terrible suggestions for solutions from your users, you might disregard what they say entirely.

But both of these are wrong.

Users are experts on their experience. Devs are experts at making software. Both tend to be worse than the other at the others' field.

Another "bad habit" is that people feel like they should be "constructive" when they say your software doesn't work well with their workflow. But that results in two things that both are bad: 

1. A lot of people just take the user's suggestion for a solution at face value, even if it isn't optimal for their problem.
2. Users tend to become very invested in their idea, and that might make it difficult to convince them that maybe another solution might be better.

__Quality feedback is actually: "This sucks for me because…"__

And finally: when you get a weird request, or what seems to be a very impractical feature request:

__Ask why.__

Ask the users directly, and if you still don't understand, ask if you can shadow them at work to understand better how they work.

* They are the experts on their problem.
* You are the expert on the solution space.
