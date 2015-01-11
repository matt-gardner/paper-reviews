---
published: true
title: "Conditional structure versus conditional estimation in NLP models; Klein and Manning, EMNLP 2002."
layout: post
author: Matt
tags:
- NLP
---

[Link to paper](http://dl.acm.org/citation.cfm?id=1118695)

This was actually for a class and not research, but it seemed important enough to share here
anyway. It explains the difference between model structure and parameter estimation methods, which
I didn't really understand until recently (through reading Noah Smith's dissertation and this
paper). I had conflated model structure with the objective function being optimized. Certainly some
model structures are better suited for certain objective functions, but you can optimize whatever
objective function you want to when you are estimating parameters.

The take away point from this paper is that optimizing conditional likelihood generally works
better than optimizing joint likelihood of the data. That makes sense, because at test time it's
really a conditional probability that you want, anyway. But you can optimize conditional likelihood
with a generative model just fine; generative models do not have to be tied to joint likelihood
parameter estimation methods.

The other take away point is that conditionally structured models are actually worse than
generatively structured models in some (most?) cases, all else being equal. But what conditional
models give you is the ability to use richer features, and that's why maxent markov models worked
so much better than HMMs when they were introduced.

So, this was a 2002 paper, and maybe it's old hat to all of you (the two people who actually got
this far...). But I thought it was enlightening.
