---
published: true
title: "Unsupervised Coreference Resolution in a Nonparametric Bayesian Model, by Aria Haghighi and Dan Klein, ACL 2007."
layout: post
author: Matt
tags:
- Coreference Resolution
---

Haghighi and Klein (H&K) have four papers on coreference resolution, and I read all of them in the
last couple of days. It turns out that those four papers also comprise Haghighi's entire
dissertation, minus a little introduction and an appendix. The reason I read these papers is that
I'm using H&K's final coreference system in some research I'm doing, looking to expand on what they
did. I'll write a little bit about each paper here, starting with the first.

Previous (and many still current) coreference resolution systems take an approach where each
mention in text (roughly corresponding to noun phrases) linked in a pairwise or clustering fashion
to the mentions previous to it, using mostly discourse cues and syntax features, trained
discriminatively. This approach instead opts to model the text generatively, unsupervised, and
answer coreference questions by relying on a set of entities and their properties that are learned
from text.

They essentially have a hierarchical Dirichlet process over entities, with a multinomial
distribution for each entity that determines what head words are used in nominal mentions of that
entity. They then enrich the model for some fancy things for pronouns that aren't too important to
describe here, and they add a "salience" term that biases pronouns to have close antecedents and
proper nouns to be new entities (those parameters are learned from text, by the way).

To learn the model they do some fancy Gibbs sampling with some (additional) approximations and a
kind of annealing.

They report results comparable to (though slightly worse than) state-of-the-art supervised systems
of the day, which is pretty impressive for an unsupervised system.
