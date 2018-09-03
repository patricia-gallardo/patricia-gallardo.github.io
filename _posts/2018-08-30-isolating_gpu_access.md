---
title: Isolating GPU Access in its Own Process
description: Composing Using Multiple Processes
author: Patricia Aas
layout: post
icon: fa-film
image: "/assets/images/graffiti-3610348_640.jpg"
---

Chromium's process architecture has graphics access restricted to a separate GPU-process. There are several reasons why this could make sense, three common ones are: Security, Robustness and Dependency Separation. 

GPU access restricted to a single process requires an efficient framework for communication over IPC from the other processes, and most likely a framework for composition of surfaces. This talk describes both the possible motivations for this kind of architecture and Chromium's solution for the IPC framework. We will demonstrate how a multi-process program can compose into a single window on Linux.

<iframe src="//www.slideshare.net/slideshow/embed_code/key/61khbx38ukcRLG" width="595" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/PatriciaAas/isolating-gpu-access-in-its-own-process" title="Isolating GPU Access in its Own Process" target="_blank">Isolating GPU Access in its Own Process</a> </strong> from <strong><a href="https://www.slideshare.net/PatriciaAas" target="_blank">Patricia Aas</a></strong> </div>