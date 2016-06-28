---
published: true
title: "Sequence-to-sequence models for semantic parsing"
layout: post
author: Matt
tags:
- Semantic parsing
---

There were two papers accepted at ACL 2016 that use sequence-to-sequence models for performing
semantic parsing, where phrases in natural language are mapped to logical forms in some formal
schema:

- [Data recombination for neural semantic parsing](https://arxiv.org/abs/1606.03622), by Robin Jia
and Percy Liang.
- [Language to Logical Form with Neural
  Attention](https://www.semanticscholar.org/paper/Language-to-Logical-Form-with-Neural-Attention-Dong-Lapata/4fef246fb4a26eb8f35c5d5645711d396a3a12c4),
by Li Dong and Mirella Lapata.

What is most surprising to me about both of these papers is that seq2seq models work at all for
generating logical forms, which are essentially trees.  Both papers present results that roughly
match state-of-the-art methods that use much more complicated formalisms (though they generally
don't really surpass the state-of-the-art, just match it).  I guess I shouldn't be too surprised,
given that character-level LSTMs are able to [generate balanced source
code](http://karpathy.github.io/2015/05/21/rnn-effectiveness/), and Jia and Liang's paper does say
that they need to balance parentheses after the fact in some cases.

Both papers recognized the need to handle entities and numbers in special ways, so that a seq2seq
model doesn't have to learn generate entities at test time that it never saw in training.  The
Dong and Lapata paper used a pre- and post-processing hack to fix this, replacing entities and
numbers with special identifiers, while the Jia and Liang paper included a copy mechanism as part
of the decoder, which I thought was pretty interesting.

Other than the special handling related to entities, both papers presented largely vanilla seq2seq
models with attention.  In addition, each paper had a separate twist on top of these vanilla models
that made the paper stand out a little more.  Dong and Lapata, recognizing that logical forms are
trees, also tried a novel seq2tree model that I thought was pretty cool.  Basically, the LSTM can
generate a special non-terminal symbol, which then causes the decoding to recursively generate from
the non-terminal.  Jia and Liang used a data augmentation technique to get more and better
training data, fitting a synchronous context free grammar on the training data that generates both
sentences and logical forms.  They then did some transformations on this grammar to "recombine"
the training data in compositional ways, by generalizing entity types and phrases, and
concatenating sentences.  That last one was surprising to me, but their explanation of forcing the
attention model to become more crisp made sense to me - if a large part of the input is irrelevant
to decoding a large part of the output, the attention model will learn to focus better.  I wonder
what would happen if you flipped the order of the logical forms when you did the concatenation?

It's really interesting to see work in this direction, though it is pretty limited in requiring
labeled logical forms for each training input.  Most recent work I've seen on semantic parsing has
moved past this, only training on question-answer pairs or using distant supervision.  It's not
clear to me how to extend this work to be applicable to cases with more limited training data.
