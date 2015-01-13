---
published: true
title: "Coreference resolution in a modular, entity-centered model, by Haghighi and Klein, NAACL 2010."
layout: post
author: Matt
tags:
- Coreference Resolution
---

This won the best paper award at NAACL that year, and I saw the presentation. I was pretty excited
about the work then, and it looks like I still am, because I'm working on extending it. I have the
code that ran this system, and I'm working on getting it to run with my data, then I can add some
of my ideas to it.

I've posted about two coreference systems by H&K already. This one improves the unsupervised model
of the first system a little bit and adds the syntactic constraints of the second one. There are
two main improvements to the first model.

First, they change an HDP over entities to something a little more complicated. Instead of simple
multinomial distributions over heads in mentions, they have a multinomial for each of kind of
relationship you might have in a dependency parse (like, NN-MOD, GOV-SUBJ, and so on, to capture
which nouns typically modify this entity, what verbs it's the subject of, and others). It's a
complicated kind of distributional semantics for each entity, indexed by the dependency relation.
And it's actually not a multinomial distribution, either - each entity has a few special words that
it uses more frequently, and there's a parameter that weights between uniformly drawing from one of
those special words and a back-off multinomial over the entire vocabulary, learned for each entity
type. This sounds very much like an adaptor grammar, or something like it, though I need to think
more about exactly how they're related.

Second, they improve their "salience" model from the first paper by having a log-linear classifier
over antecedent positions, freely conditioning on the whatever they want to in the sentence and
parse tree to select the best antecedent position for a given mention.

They do some pretty complicated variational inference to learn their model; I need to look at their
code in more depth and read a bit more about variational inference in general before I'll feel
really comfortable with their learning algorithm.

Their results are quite impressive - they beat all previously reported unsupervised and supervised
results, with a system that has as its only input a few seed instances to start their entity model
out right.

UPDATE (01/2015): My experiments trying to continue this idea didn't turn out very well, and it
also turns out the code that I got from Aria didn't really work.  And lots of people have
complained about this particular paper not really being reproducible...
