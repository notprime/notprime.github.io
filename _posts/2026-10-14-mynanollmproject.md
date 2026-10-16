---
layout: post
title: My nanollm project
date: 2026-10-14 00:00:00
description: my nanoGPT-like project, and it's going to be lots of fun!
tags: nanollm llm
#categories: sample-posts
#marimo: true
---

# My nanollm project

## 0. A very short introduction

So, here we are. I have never written a blog post before, but this project I'm working on definitely deserves to be narrated. There will be errors, issues, <span style="color: #c50808;">**catastrophes**</span> (ok, maybe that's a bit too much), but I think this will be a very rewarding and instructive journey.

As I'm writing this first post, my website (well, a simple GitHub Pages website built with [Jekyll](https://jekyllrb.com/) and [al-folio](https://github.com/alshedivat/al-folio)) is still a mess, with the tutorials provided by al-folio, pictures of Albert Einstein scattered around, and so on. Maybe by the time you read this post, the website will be all nice and tidy. But I had to tell you: it used to be a (or rather, **MY**) mess! Here is a picture of what the website used to look like:

<img src="/assets/img/2026-10-14-mynanollmproject/myoldwebsite.png" alt="My old website" style="width: 100%; max-width: 600px; height: auto;">

If you've made it here, you probably already know that this project will revolve around the LLM space. Still, I'd like to dedicate a couple of lines to the rules I'll follow in my blog posts, just to give you an idea of what to expect:
- This won't be a serious blog: I like memes, I like jokes, and you'll find plenty of both in my posts.
- I'll try to be as specific as possible without turning this blog into arXiv. I'll dig deep into topics I'm not very familiar with, but I'll focus on the most important bits, leaving you the task of reading the related papers and references (less work for me, more adventure for you).
- `writing_a_blog != knowing_everything`: this is also a learning journey for me, so if you spot an error or some 🐂💩 (spoiler: **bullshit**) I've written, don't hesitate to contact me through whatever means you can think of, so we can fix it!
- I also want to use this blog to do some networking, because I always love meeting new people!
- I'll use AI tools to improve **things**: correct grammar, provide code examples, and so on. AI is here, and it's pretty damn capable. And honestly, an AI researcher not using AI tools is a bit weird, and suspicious 🥷. Nevertheless, rest assured that everything you read here will ultimately come from my brain. So, if you read something cool: good! If not, sorry, my brain probably stopped working somewhere along the way 💥.

I'll update this list if I come up with any other rules, but for now, I think that's enough.

I said this would be a short introduction, and it seems pretty short to me. So, let's jump into the actual fun part.

## 1. A proper introduction

Now we can start talking about the project. 

I'm an AI researcher, but I've mainly worked on self-supervised learning (SSL) for vision tasks, applying it to remote sensing data and studying and training Geospatial Foundation Models. When it comes to LLMs, I've mostly used them as "final products." I've read plenty of papers over the years, so I'm quite comfortable with most of the theory, but I've never actually written the code that makes the magic happen. It's time to change that!

So, let's say I know the theory behind transformers quite well, and I understand the basics of LLM training. Now, I want to build my own small LLM from scratch (let's call it <span style="color: #3164f0;">**nanollm**</span>, for reasons you're about to discover) and work my way through every stage of the process.

To be <span style="color: #4ba5cc;">**crystal clear**</span>, I'd like to cover both:
- model definition and training, including pretraining and post-training (SFT, DPO, RLHF);
- systems and applications: inference and serving, RAG, and agents.

To sum it up, the goal is to go from [Karpathy's videos](https://www.youtube.com/@AndrejKarpathy) to a working, modern-ish decoder that I understand line by line.

The LLM field is huge nowadays: there are countless stages, theoretical concepts, engineering challenges, and so on. I don't want to become proficient in or an expert on everything, but I do want to explore every major component behind modern LLM systems. I think this is the only way to develop a solid understanding of how everything fits together. Hopefully, my experience will be beneficial to others as well, and I won't be the only one who understands what I've built, line by line.

I'll upload everything I do, every single bit of code, to the project repository, [nanollm](https://github.com/notprime/nanollm). I'll also try to be as clear as possible with the code, comments, and hyperlinks throughout the posts. I don't want you to feel lost in a jungle (even if jungles are pretty cool).

Oh yes, now's the perfect time to tell you why I chose to call the project <span style="color: #3164f0;">**nanollm**</span>: I'm compute- and hardware-constrained, and I thought it would be interesting to train a small LLM on my own hardware. Obviously, this means we'll have to make some budget-conscious decisions, but it'll also push us to explore scaling laws, LoRA/QLoRA, and so on.

I also think it's only fair to give my little PC a heroic name, and we'll use that name every time I mention it. For consistency, we'll call it the <span style="color: #a821b5;">**nanobeast**</span>!

What incredible components does the <span style="color: #a821b5;">**nanobeast**</span> pack?
- **CPU**: AMD Ryzen 7 7800X 🔥
- **GPU**: RTX 3060Ti 8GB VRAM (pls don't die, I love you ❤️)
- **RAM**: 16GB RAM 💀

According to <span style="color: #c26603;">**Claude**</span>, this is what I can do with this fantastic rig:
> <span style="color: #c26603;">**Claude**</span>: Given your hardware (16GB RAM, RTX 3060Ti 8GB VRAM), the ceiling for local training from scratch is small models (tens of millions of params, maybe up to ~150M with heavy tricks). For fine-tuning, quantized LoRA/QLoRA gets you to 1B–3B models comfortably, maybe 7B at 4-bit if you’re patient. For inference, quantized 7B–8B models run fine via llama.cpp; vLLM will be tighter on VRAM but workable for small models.

**Obviously**, these are rough estimates, not guarantees. Actual limits will depend on the architecture, sequence length, batch size, and memory optimizations.

Brace yourselves, because I'm ready to destroy everything (`insert evil laugh here`)(hopefully not the <span style="color: #a821b5;">**nanobeast**</span>)!

I've also asked Claude to give me a roadmap that I'll try to follow closely, to keep my brain from going off on tangents and getting lost. I'll dedicate a blog post to each phase of each project in the roadmap, whenever possible.

In the following sections, I'll briefly introduce each project. Each project will be divided into multiple phases, which we'll explore in the actual posts. No need to fill this post with too many details!

## 2. Projects

### 2.1 Project 1: Build a GPT from scratch  
🎯**Goal**: go from Karpathy's videos to a working, modern-ish decoder we can understand line by line.

Here, we'll establish the general pipeline, covering a debugging dataset and tokenizer, a baseline transformer, and a test training run to check that everything works. Finally, we'll explore some architectural extensions.


### 2.2 Project 2: Pretraining and scaling

🎯**Goal**: experience the actual pretraining loop and develop some intuition about scaling laws.

We'll start by implementing a reproducible pretraining pipeline, then train a baseline model on the <span style="color: #a821b5;">**nanobeast**</span>! We'll train three model sizes, compare them, and run some scaling-law experiments. Everything should work if we haven't made any mistakes, but who knows 😛.

### 2.3 Project 3: Post-training

🎯**Goal**: go from supervised fine-tuning to preference optimization, and then RL.

You already know the deal. We'll first prepare the datasets, then start experimenting with SFT (Supervised Fine-Tuning), comparing full fine-tuning with LoRA. Next, we'll move to DPO (Direct Preference Optimization), and finally, RLHF with PPO.

### 2.4 Project 4: Efficient inference and serving

🎯**Goal**: understand how tf we can serve those LLMs to lots of people!

This project might take a while (Project 3 might take a while too). We'll dive into inference fundamentals, implement a KV-cache, deal with quantization and llama.cpp, and finally play around with vLLM and serving internals.

### 2.5 Project 5-7: RAG, agents, a capstone project

🎯**Goal**: understand how tf we can build amazing things with those LLMs!

Nothing fancy here. We'll play around with RAG and agentic AI. Finally, we'll work on a capstone project. I have a few ideas, but knowing myself, I'll probably come up with new and interesting ones over the coming months. No need to reveal anything just yet (again, `insert evil laugh here`).

---

More or less, this concludes my first blog post. I'll add all the hyperlinks as I go, and over time, this post will become even prettier. I'll try to force myself to publish a post every week, but that might be difficult given how hard some of these topics are.

This isn't how you're supposed to end a blog post, but my creativity isn't working right now, so I'll just leave it here.

See you soon, friends!


**Yours, <br>
Riccardo "notprime" Musto**

<img src="/assets/img/2026-10-14-mynanollmproject/handshake.jpg" style="width: 100%; max-width: 600px; height: auto;">