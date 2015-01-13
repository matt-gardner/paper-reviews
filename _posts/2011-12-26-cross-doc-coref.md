---
published: true
title: "Collective Cross-Document Relation Extraction Without Labelled Data, by Limin Yao, Sebastian Riedel, and Andrew McCallum, EMNLP 2010."
layout: post
author: Matt
tags:
- Relation Extraction
---


This paper is really very similar to a lot of previous work in weakly supervised information
extraction, including several papers I've already posted here. They do the typical "find sentences
that mention two Freebase entities and learn a relation classifier from those sentences" business.
There were two things in this paper that I thought were worth mentioning.

The first was the main contribution of their paper, which is explicitly modeling the selectional
preferences of relations. That is to say, the relation "founded" normally takes a person and a
company as arguments. If you know which entities are people and which entities are companies, as
well as that particular selectional preference, you should do better at extracting instances of the
"founded" relation.

That by itself really isn't all that surprising; we do the same thing with NELL. They do it with a
weakly supervised factor graph, where we do it as part of a bootstrapped semi-supervised learning
system. In the end it's not all that different, though our modeling of relationships between
relations is more complex than theirs. But this addition to traditional CRF models of relation
extraction is why this paper was published.

The other interesting thing was just a short description of a method I wasn't familiar with,
SampleRank. Apparently you can learn the weights in a graphical model in the process of MCMC
inference. I had seen this method alluded to once in another paper, but this gave a description of
it. It looks like I need to read that paper (SampleRank: Learning preferences from atomic
gradients, by Wick et al., 2009).
