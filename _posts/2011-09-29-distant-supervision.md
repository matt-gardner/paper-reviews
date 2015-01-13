---
published: true
title: "Mintz, Bills, Snow, Jurafsky, ACL-IJCNLP 2009. Distant supervision for relation extraction without labeled data."
layout: post
author: Matt
tags:
- Distant Supervision
- Relation Extraction
---

[Link to paper](http://web.stanford.edu/~jurafsky/mintz.pdf).

This is very similar to the last paper that I posted; that other paper based a lot of what they did
on this paper, and addressed some of this one's limitations. But this paper had a different focus
and a different method, both of which are worth talking about.

This paper uses Freebase to get training data for a classifier that maps entity pairs to relations.
They take a few hundred thousand instances of relations from Freebase, find the entities involved
in a pile of unstructured text, then assume that the sentences they found probably encode the
relation in some way. That's certainly not true for every sentence, but if you average over
millions of sentences, you should be fine. But once they have these sentences, they extract
features from them, aggregate them over the whole unlabeled corpus, and use them to learn a
classifier.

This paper, then, is only doing aggregate information extraction, though they get their data from
lots of individual sentence. It is, in fact, very much like NELL's macro reading, except they use
additional kinds of features. Because they classify individual entity pairs, also, each pair can
only ever be involved in a single relation, which is clearly suboptimal.

Some of their features are very similar to NELL's. What they call lexical features amount to CPL's
context features (though they only deal with relations, not categories, so it's a subset of CPL).
But they also add syntactic features, drawn from a dependency parse. They aggregate that parse
information over their whole corpus, and it turns out to help them most of the time, sometimes by
quite a bit.
