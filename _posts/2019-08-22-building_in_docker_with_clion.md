---
title: Building in Docker with CLion
description: Personal Notes
author: Patricia Aas
layout: post
icon: fa-film
image: "/assets/images/skeleton-3995547_640.jpg"
---

This workflow was inspired by the Windows Subsystem for Linux (WSL) workflow described by Jetbrains [here][1].

The idea is to be able to develop for Linux in CLion on Windows and Mac aswell. For Windows the WSL is preferable because it's faster and has a lot of support. On Mac there isn't a similar native Linux solution. The idea was to use a Docker container as a Remote Host following [this Jetbrans article][2].

To do this we need a suitable Docker image, this one has currently only been tested on Linux, but seems to work: [Dockerfile][3].

Do use it you have to run the container - there are some comments in the [Dockerfile][3] on how. Then set up CLion using the [Remote Host][2] tutorial.

[1]: https://www.jetbrains.com/help/clion/how-to-use-wsl-development-environment-in-clion.html
[2]: https://www.jetbrains.com/help/clion/remote-projects-support.html
[3]: https://github.com/patricia-gallardo/c_on_linux/blob/master/toolchain/Dockerfile
