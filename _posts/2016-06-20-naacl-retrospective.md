---
published: true
title: "Quick NAACL 2016 Reactions"
layout: post
author: Matt
tags:
- NAACL
- Semantic parsing
- Cloze
---

I had a good time at [NAACL](http://naacl.org/naacl-hlt-2016/) last week.  I got to catch up with
a lot of old friends, and made some new ones.  I had two main takeaways from the actual content of
the conference: (1) the science questions we're focusing on at AI2 are similar to the cloze-style
questions many reading comprehension datasets use, and (2) a lot of people are interested in
learned execution models for semantic parsers.

### Cloze-style evaluations

I work on the [Aristo](http://allenai.org/aristo/) team at AI2, trying to answer multiple-choice
4th grade science questions.  Most of these questions are fill-in-the-blank kinds of questions
(e.g., "Cells contain genetic material called \_\_\_."), or, if there's not an explicit blank in
the question, can be converted to this form by removing the wh-phrase (e.g., "Which gas is given
off by plants?" --> "\_\_\_ is given off by plants.").  This is also the format of many reading
comprehension datasets that use a cloze-style evaluation.  I hadn't made that connection before,
and wasn't really familiar with the term "[cloze](https://en.wikipedia.org/wiki/Cloze_test)".
Typically, cloze tests are more about language modeling than they are about question answering,
but the approach I'm taking to answering these science questions is very similar to a structured
language model trained on a large corpus of science text.  So, I discovered that I need to read a
lot more about what datasets are available for cloze-style evaluations, and what methods have been
used on them.  Look for reviews of some of these papers soon.

### Learned execution in semantic parsers

One of the best papers at NAACL this year was "[Learning to Compose Neural Networks for Question
Answering](https://www.semanticscholar.org/paper/Learning-to-Compose-Neural-Networks-for-Question-Andreas-Rohrbach/7784d715bb3a4243ea18e4cd603d565a8b0c58aa)".
Though Jacob describes this work in terms of "neural modules" that are composed on the fly to
answer a particular question, I think the paper is best viewed as a semantic parser with a learned
execution model.

Semantic parsers typically map language onto statements that are directly executable against some
fixed schema, such as Freebase.  For example, "Where was Obama born?" might get mapped to something
like \\(\lambda(x).\mathrm{/people/person/born\_in}(\mathrm{Obama}, x)\\), which you could execute
as a query against Freebase to return Honolulu.

These execution models don't have to be restricted to database queries, however.  You can also map
language to a set of actions you can take from a phone, for instance, or movements that a robot can
make.  If you had some kind of execution operation against images that included things like
telling which objects are in the image, or how the objects in the image are related, you could
also map language onto this set of operations.  People have built semantic parsers to do all of
these things.  The last of these is particularly interesting, however, as typically operations
against images are learned systems, not simple database queries.  The question then becomes, can I
learn the semantic parsing model (which maps language onto executable statements) jointly with the
execution model (which tells me, e.g., whether there is a sheep in this image)?

There have been a few papers that have tried to do this (one that comes to mind is a [2013 TACL
paper](https://www.semanticscholar.org/paper/Jointly-Learning-to-Parse-and-Perceive-Connecting-Krishnamurthy-Kollar/0ec1a840e6895101b7040f7b32093785d4a0c0ef)
by my colleague Jayant Krishnamurthy).  What's novel about this paper is that the learned
execution models are deep convolutional neural networks, and this is evaluated on a large visual
question answering dataset.  The way they got this joint training to work, with reinforcement
learning, is also pretty different from how previous systems tried to do this.  The actual results
aren't that much better than other systems on the VQA dataset ([59.4 vs.
58.9](https://www.semanticscholar.org/paper/Learning-to-Compose-Neural-Networks-for-Question-Andreas-Rohrbach/7784d715bb3a4243ea18e4cd603d565a8b0c58aa/figure/1)),
but I think their approach to the problem is really cool.

One pretty big drawback with the approach, though, is how impoverished the execution models are.
There are only 5 or 6 predicates that the parser can map language onto, so you get obviously
deficient parses like
[mapping](https://www.semanticscholar.org/paper/Learning-to-Compose-Neural-Networks-for-Question-Andreas-Rohrbach/7784d715bb3a4243ea18e4cd603d565a8b0c58aa/figure/5)
"What is the man dragging?" to `(describe[what] find[man])` (telling the network to find the
person, then describe what it sees - shouldn't this just return "man"?).  It's impressive to me
that the model is able to do as well as it does with such a restricted execution language.

Overall, though, this is a really nice piece of work.  It's also very much related to things we're
working on at AI2, so I was happy to see interest in this line of research.
