---
published: true
title: "A survey of the current state of reading comprehension"
layout: post
author: Matt
tags:
- Reading comprehension
---

Reading comprehension is a really hot topic in deep learning for NLP right now.  It's a high-level
NLP problem, and so is interesting just from a scientific perspective (how do we build statistical
models that can reason about a passage of text?), and it has some potential product applications.
There have been over 10 datasets released related to this task just this year, and dozens of
papers publishing methods for solving this problem.  The field is moving _fast_.

I'm working on applying reading comprehension techniques to answering science questions.  There are
some important differences between science questions and reading comprehension questions, but also
some broad similarities that make studying current methods and datasets for reading comprehension
useful.  I recently gave a talk at AI2 with a survey of all of the currently-popular reading
comprehension datasets, and some of the more popular methods that are used for this task.
Converting the slides for that talk into a blog post would be too much work, but I think others
might find the slides themselves useful.  You can find them
[here](https://docs.google.com/presentation/d/1Y5y7xXmWBPkxEzOhP_PrV40FpLxEPXo41SGYzw8zKcA/edit?usp=sharing).
There's also a
[spreadsheet](https://docs.google.com/spreadsheets/d/1CC9a96nLhOFf7O6uJIyv_E8frHpUa7ciwKZlpmcUtmc/edit#gid=0)
that has links to actual papers.

Datasets I mentioned:

* MCTest
* bAbI
* SNLI
* LAMBADA
* WikiReading
* WikiSuggest
* WikiMovies
* MS MARCO
* ROCStories
* CNN / Daily Mail
* Who Did What
* Children's Book Test
* BookTest
* SQuAD
* NewsQA

Methods I (briefly) described:

* Memory networks
* Attentive Reader
* Attention Sum Reader
* Gated Attention Reader
* Bi-directional attention flow
* Bilinear annotation re-encoding boundary

There are a _lot_ of methods I left out - there is a pretty clear story going from one of these to
the next, so it was easy to give a brief outline of the progression of these models using these
examples.
