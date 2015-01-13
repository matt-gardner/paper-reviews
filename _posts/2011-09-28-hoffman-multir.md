---
published: true
title: "Hoffmann et al, ACL 2011. Knowledge-Based Weak Supervision for Information Extraction of Overlapping Relations"
layout: post
author: Matt
tags:
- Relation Extraction
- Distant Supervision
---

The point of this paper is to use a knowledge base to learn a classifier for mapping sentences to
relations over entities, very similar in purpose to what +Justin Betteridge has been working on.
They use markov random fields to model possible facts in a database. They use some amount of known
relations from Freebase to learn the weights for the factors in their MRF, then use the learned
model on new sentences (and with more entities? that part wasn't exactly clear to me) to extract
more relations.

There were a couple of things I thought were particularly interesting. First, they use the terms
"aggregate extraction" and "sentential extraction" to refer to what we call "macro reading" and
"micro reading." They try to do both in their paper, but most of their work is on sentential
extraction, getting aggregate results only by a simple OR over all sentences. I think that puts a
little too much confidence in the sentence extractors, and some aggregate classifier (like NELL's
macro reading) would be more appropriate. But they do it that way because it greatly simplifies
learning and inference, and still gives them better performance than previous methods.

The other thing I thought was interesting was the setup of their model. The took all pairs of
entities and predicted a yes-no for every relation that they were considering. That could be
really, really big, but I guess their domain was small enough that it still worked. They did some
preprocessing to get (for each pair) all sentences in which the pair of entities appeared together,
so I suppose that limited the entity pairs considerably.
