---
published: true
title: "Three More Word Embeddings Papers"
layout: post
author: Matt
tags:
- Neural Networks
- Word Embeddings
---

Ok, one last round of word embeddings papers, then I'm on to research that's a lot more relevant
to my current work.  Here I'll look at three papers, all of which are again related to skip-gram.
Two of them look at giving more or different information to neural embedding models, and one looks
a little more deeply at the objective function optimized by skip-gram.

The first paper, [Dependency Based Word
Embeddings](http://www.cs.bgu.ac.il/~yoavg/publications/acl2014syntemb.pdf), by Levy and Goldberg,
ACL 2014 (short paper), trains a skip-gram model using dependency edges instead of a bag of words
as contexts.  They show that this captures functional similarity better than the traditional
skip-gram model, which tends to capture domain similarity.  This is pretty much exactly what you
would expect, so I'm not surprised by those results at all.  It was a little surprising to me that
using dependency edges instead of close words performs much worse on the analogy task used by
Mikolov and others - I would have thought that it could perform better on the syntactic analogies
than the original skip-gram.  I wish I understood what was going on with that task better than I
do.

The second paper, [Not All Neural Embeddings are Born Equal](http://arxiv.org/abs/1410.0718), by
Hill and others, NIPS workshop 2014, has another seemingly obvious result: using neural network
language model from a translation system performs better than using a monolingual language model.
Well, it has twice as much data, even if half of it is in another language, so it's not really
surprising to me that the translation model does better (this is evaluated on some standard word
similarity tasks; on anaologies, the translation model does better with syntactic analogies, worse
with semantic analogies).  The experiment is confounded a bit by the fact that there are two
things varying here at the same time, and neither can be easily isolated: the architecture of the
model is different (skip-gram and GloVe vs. a neural translation model), and the data is different
(one half of a bilingual corpus, or all of it).

The last paper, [Neural Word Embedding as Implicit Matrix
Factorization](http://papers.nips.cc/paper/5477-neural-word-embedding-as-implicit-matrix-factorization),
by Levy and Goldberg, NIPS 2014, is the most interesting (to me) of these three.  It looks at the
objective function optimized by skip-gram, and shows that it is implicitly factoring a (shifted)
PMI matrix.  That's a really interesting (and non-obvious) connection.  They further show that they
can optimize the objective directly, either by just constructing the shifted PMI matrix, or by
using a truncated (and thus sparse) version of that.  And, instead of implicitly factorizing this
shifted matrix, once you know what skip-gram is doing, you can just directly factor the matrix
yourself using SVD.  They show that for several tasks (all that they tested except for syntactic
analogies), these more direct techniques outperform skip-gram.

I guess what I get from all of this is that there are a lot of different tasks you could do with
word embeddings, and performance on those tasks depends a lot on the specifics of how you create
your embeddings.  There are also a lot of information sources that could help you create word
embeddings.  I know people have looked at model architectures where you have several hidden layers
in a neural network, then several tasks that all need to be explained by the output, and you train
this large model jointly.  I wonder if anyone has done something like that with word embeddings...
A quick search didn't turn up anything particularly promising, but I might not have looked in the
right place.
