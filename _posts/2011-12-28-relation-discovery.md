---
published: true
title: "Structured Relation Discovery using Generative Models, by Limin Yao, Aria Haghighi, Sebastian Riedel, and Andrew McCallum, EMNLP 2011."
layout: post
author: Matt
tags:
- Relation Extraction
- LDA
---

This paper exemplifies my problems with LDA and unsupervised learning in general. Basically what
they did was tweak LDA to model relations instead of words, with each "topic" having a set of
multinomial distributions over features for an observed relation (e.g., the Gamma Knife, made by
the Swedish medical technology firm Elekta, is a "word" in this LDA model, with a set of features
that are used when predicting the relation between the two entities, corresponding to the "topic"
in LDA). At its heart, this isn't very different from what Haghighi and Klein did for coreference
resolution, or what I am planning on doing with entity resolution in NELL. The models look almost
identical if you squint a little bit. But they have relations as their "topic" instead of entities,
as in H&K's coreference model, with different features that are intended to be better suited to
relations.

Well, you can imagine that inference for this model is straightforward (they use variational EM).
And, if you're familiar with the topic model literature, you already know the result. They pick a
few topics that look particularly good to show you in the paper, and make some arguments based on
those hand-picked topics. Their models had 100 topics, but they used 5 in their evaluation, because
they looked the closest to actual relations in Freebase. Forgive me if I'm a little skeptical, it's
just all too familiar from every other LDA paper I've read. Their paper is titled "Structured
Relation Discovery using Generative Models." I contend that they didn't actually do that; they
found clusters that in a few instances look a little bit like what people consider to be relations,
but in most instances don't. If they had some way to automatically determine what relation was
represented by each of their clusters with a high precision, I would be much more impressed.

If their paper had ended there, I would have been completely unconvinced that their model was
useful for anything, even if it was an interesting thing to try. But, to their credit, they did try
an external evaluation of their model, by using the clustering output as a feature in a distantly
supervised relation extraction approach (these are the same people that have done a number of
distant supervision papers, so that's an obvious application of this). The problem here is that the
model that they thought was better when looking at the clustering performed worse than the
clustering model they thought was pretty bad. And all of the results were really pretty close to
the baseline; I wished there had been some sort of significance testing.

Using LDA to model relations was an interesting thing to try, I'll give them that. It's also pretty
similar to things that I'm looking at right now (an LDA-like model with several features per
"word"), so it was interesting to see what they did. I'm just not really convinced by their results
that the method is worth pursuing any further.
