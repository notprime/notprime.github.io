---
layout: post
title: My nanollm project
date: 2026-10-14 12:00:00
description: my nanoGPT-like project, it's going to be lots of fun!
tags: nanollm llm
categories: sample-posts
#marimo: true
---


# 0. A very short introduction

So, here we are. I have never written a blog post before, but this project I'm working on definitely deserves to be narrated. There will be errors, issues, catastrophes (ok, maybe that's a bit too much), but I think this will be a very rewarding and instructive journey.

As I'm writing this first post, my website (well, a simple GitHub Pages website built with [Jekyll](https://jekyllrb.com/) and [al-folio](https://github.com/alshedivat/al-folio)) is still a mess, with the tutorials provided by al-folio, pictures of Albert Einstein scattered around, and so on. Maybe by the time you read this post, the website will be all nice and tidy. But I had to tell you: it used to be a (or rather, **MY**) mess! Here is a picture of what the website used to look like:

![my old website *.*](/assets/img/myoldwebsite.png)

If you've made it here, you probably already know that this project will revolve around the LLM space. Still, I'd like to dedicate a couple of lines to the rules I'll follow in my blog posts, just to give you an idea of what to expect:
- This won't be a serious blog: I like memes, I like jokes, and you'll find plenty of both in my posts.
- I'll try to be as specific as possible without turning this blog into arXiv. I'll dig deep into topics I'm not very familiar with, but I'll focus on the most important bits, leaving you the task of reading the related papers and references (less work for me, more adventure for you).
- `writing_a_blog != knowing_everything`: this is also a learning journey for me, so if you spot an error or some 🐂💩 (spoiler: *bullshit*) I've written, don't hesitate to contact me through whatever means you can think of, so we can fix it!
- I also want to use this blog to do some networking, because I always love meeting new people!
- I'll use AI tools to improve **things**: correct grammar, provide code examples, and so on. AI is here, and it's pretty damn capable. And honestly, an AI researcher not using AI tools is a bit weird, and suspicious 🥷. Nevertheless, rest assured that everything you read here will ultimately come from my brain. So, if you read something cool: good! If not, sorry, my brain probably stopped working somewhere along the way 💥.

I'll update this list if I come up with any other rules, but for now, I think that's enough.

I said this would be a short introduction, and it seems pretty short to me. So, let's jump into the actual fun part.

# 1. A proper introduction

Now we can start talking about the project. 
I am an AI Researcher, but I have always mainly worked on SSL for vision tasks, applying SSL to remote sensing data, studying and training Geospatial Foundation Models. When it comes to the LLM field of AI, I have only used them as "final-products", I have read papers throughout the years, but never actually dig deep into how they actually works, trained, and used. So, let's say I know quite well the theory behind transformers, I know the basics of LLMs training, but I now want to build from scratch my own small LLM (let's call it **nanollm** for reasons you are about to discover), and go every possible stage an LLM has to go through.  So, to be crystal clear, I would like to span both:
- model definition and training, including pre- and post- (SFT, DPO, RLHF)
- systems and applications: inference/serving, RAG, agents.

To sum it up, the goal is to go from Karpathy's videos to a working, modern-ish decoder I understand line by line.
The LLM field is nowadays huge: lots of stages, theory, engineering and so on. I don't want to become proficient or an expert in everything, but at least I want to touch every single piece behind modern LLM systems: I think this is the only way to understand those topics. 
Hopefully, my experience will be beneficial to others as well, and I won't be the only one to understand what I've done line by line.



---
