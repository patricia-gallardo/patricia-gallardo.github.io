---
title: Why make a browser?
description: Learning by Doing
author: Patricia Aas
layout: post
icon: fa-pencil
image: "/assets/images/face-woman-3514196_640.jpg"
---

I understand why it might seem odd that the first thing I make is a browser, especially right after leaving a browser company. The logic behind it is a bit convoluted, but bear with me. I have a plan.

<span class="image right"><img src="{{ 'assets/images/art-3558354_640.jpg' | relative_url }}" alt="" /></span>

In the coming months I aim to learn and make a wide variety of things. Each thing I’m planning to make should provide me with at least two things:
What I make should (over time) evolve into a tool I can use in my job
I should learn something I’ve been wanting to learn

A third concern is that I need to prepare for conference talks that I’m doing this fall. So the order in which I’m making things is going to be influenced by which talk is next. 

My first talk this fall will be at [NDC TechTown][1] towards the end of August. There I will talk about GPU access in Chromium. I’ve done a version of this talk before, while I was working for Vivaldi, at [Foss-North 2018 in Gothenburg][2]. At the time I used the Vivaldi browser as the starting point for the talk, but as I no longer work there, I no longer have access to the Vivaldi source code. So I need another browser that is “easy” for me to play with.

Now, I’ve been planning to make a tool based around a browser, where the purpose is to integrate various tools for the security testing of websites. The primary purpose of this tool is technical and the idea is that it will evolve over time to do more, as I learn more.

The initial version (which I was working on last week) is a very basic browser. As I develop it, its features will probably become more and more esoteric, but hopefully they will be interesting for developers. Especially web developers and security testers. Or at least, that’s the plan, right now it’s too early to tell.

NDC TechTown is fast approaching and I want to do a remake of my talk using my new browser and tweaking the talk to be even more relevant to an embedded audience. 

For now, though, it is fun to code in qml again and playing around with QtWebEngine. Also it’s nice to have gotten a hands-on start on my “study months”.

[1]: https://ndctechtown.com/talk/isolating-gpu-access-in-its-own-process/
[2]: /2018/04/23/isolating_gpu_access.html