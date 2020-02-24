---
title: Inline Thinking
description: 97 Things Every Java Programmer Should Know
author: Patricia Aas
layout: post
icon: fa-pencil
image: "/assets/images/mario-4557908_640.jpg"
---
Computers changed. They changed in many ways, but for the purpose of this text they changed in one significant way: The relative cost of reading from RAM became extremely high.

This was something that happened gradually, until RAM accesses could completely dominate the performance metrics of an application. The CPU was constantly waiting for memory accesses to finish. And as the cost of going to RAM, relative to registers, grew and grew, chip manufacturers introduced more and more levels of cache and made them bigger and bigger.

And caches are great! If what you need is in them...

Caches are complex, but as a rule they will predict that a subsequent memory access will be close to, or preferably adjacent to, a recent, previous access. This is done by fetching a bit more than needed from memory, and storing this excess in the cache, often called pre-fetching. If a later access can get its value from the cache instead of RAM, it is referred to as a “cache friendly” access. 

Imagine that you need to iterate through a big array of relatively small objects, maybe a bunch of triangles. In Java today you don’t really have an array of triangles, you have an array of pointers to triangle objects, because regular objects in Java are “reference types”, meaning you access them through Java pointers/references. So even though the array is probably a contiguous section of memory, the triangle objects themselves can be anywhere on the Java heap. Looping through this array will be “cache un-friendly” since we will be jumping around in memory from triangle object to triangle object, and the cache pre-fetching will probably not help us much.

Imagine instead that the array contained the actual triangle objects, not pointers to them. Now they are close in memory and looping over them is much more “cache friendly”. The next triangle might be waiting for us right there in the cache. Object types that can be stored directly into an array like that are called “value types” or “inline types”. Java already has several inline types, for example int and char, and will soon have user defined ones, probably called “inline classes”. These will be similar to regular classes but simpler.

Another way to be “cache friendly” is to store objects in your stack frame, or directly in registers. A difference between inline types and reference types is that you don’t have to allocate inline types on the heap. This is useful for objects that live only for the scope of this method call. Since the relevant parts of the stack are probably in the cache, accesses to objects on the stack will tend to be “cache friendly”. As a bonus, objects that are not allocated on the Java heap do not need to be garbage collected.

These “cache friendly” behaviors are already present in Java when using so called “primitive types”, like ints and chars. “Primitive types” are “inline types” and come with all of their advantages. So even though inline types may seem foreign in the beginning, you have worked with them before, you just might not have thought of them as objects. So when “inline classes” seem confusing, you could try to think: “What would an int do?”
