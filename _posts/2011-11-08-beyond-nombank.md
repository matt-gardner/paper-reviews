---
published: true
title: "Beyond NomBank: A Study of Implicit Arguments for Nominal Predicates, by Matthew Gerber and Joyce Y. Chai, ACL 2010."
layout: post
author: Matt
tags:
- Semantics
---

This paper deals with semantic role labeling. That is, verbs take arguments, like "The lion ate the
monkey" - ate has "the lion" as its "agent" argument and "the monkey" as its "patient" argument.
(Verbal) Semantic role labeling is the process of determining what parts of a sentence correspond
to the arguments of verbs. You can do this for nouns that are derived from verbs, as well, such as
"shipping costs" - "shipping" has an entity that ships and an entity that was shipped, even though
it's not even the head noun of the noun phrase its in. If you really want to understand text, you
need to be able to determine these arguments for any kind of predicate that you encounter.

There are resources of labeled data for these tasks (PropBank for verbal predicates and NomBank for
nominal predicates). However, as this paper points out, they are sometimes limited in the kind of
information they give you. In the example containing "shipping costs," NomBank just labels
"shipping" as a predicate, without giving its arguments. Part of the reason for that is that the
arguments are distant in the text, occurring in previous sentences sometimes very far away. That's
what these authors call "implicit arguments" - essentially, "arguments not labeled in NomBank, most
often because they are not in the same sentence."

So, the authors labeled all of the arguments for a small set of very frequent nominal predicates in
the Penn Treebank (the same dataset that NomBank is built on), then learned classifiers for those
arguments. There results were decent, and considering that this is a very hard problem that no one
has really tried to solve before, decent results are actually really good.

I think this kind of stuff is fascinating, and I really want to use a knowledge base like NELL to
improve performance on these kinds of problems.
