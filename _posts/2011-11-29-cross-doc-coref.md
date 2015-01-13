---
published: true
title: "Large-Scale Cross-Document Coreference Using Distributed Inference and Hierarchical Models, by Sameer Signh, Amarnag Subramanya, Fernando Pereira, and Andrew McCallum, ACL 2011."
layout: post
author: Matt
tags:
- Coreference Resolution
---

I thought this paper was really interesting. They did things that are very similar to what I'm
currently working on. So, this is a bit longer than most of my posts about research papers.

This paper deals with coreference resolution, but instead of only dealing with one document at a
time, they want to model coreference relations across an entire corpus. Coreference resolution
amounts to partitioning a set of "mentions" in a document (typically noun phrases, but also
possessive and other kinds of adjectives). The number of partitions of the elements of a set is
enormously large (the Bell number, which is worse than exponential). When you get to cross-document
coreference on large corpora, the number of mentions can be in the millions or billions, and thus
an exact search over partitions of them is completely intractable.

So how do they solve this problem? They start with a good guess at a partition and then use MCMC to
sample one mention at a time and find a good approximate solution. That's not very surprising or
interesting by itself; the interesting part is the set of tricks they use to make MCMC work better
on really large collections of documents (and this is work done while Singh was a Google intern -
we're talking about really large sets of documents).

Their model is essentially a really large factor graph over all of the mentions in the corpus;
every mention has two factors connecting it to every other mention, one of which falls out of the
equations (if the mentions are coreferent, one of them fires, if they aren't, the other one does).
All they say about those factors is that it's a cosine similarity function over the mention context
pairs. This model would be really hairy, but they use Metropolis-Hastings sampling, and all they
have to compute is a likelihood ratio between the current state and the proposed state. In that
equation all factors except those between mentions in the old and new entity cancel each other out.

Their resulting system, then, looks like this. At every step of the algorithm, pick a mention. Draw
a new entity for that mention from a proposal distribution (they start out with this as a uniform
distribution). Calculate the likelihood ratio and do the typical Metropolis-Hastings accept or
reject (they throw some annealing in, as well). Keep this up for long enough, and you're done.

The problem with this naive system is that the proposal distribution almost never actually gives
you a good proposal, so it has to run for a really long time. In order to fix it they introduce two
kinds of latent variables. The first are sub-entity variables, that collect similar mentions to
each other (these could, for instance, collect all of the coreferent mentions in a single
document). These variables can then be sampled to move the entire collection from one entity to
another at a time, similar (in desired outcome, at least) to Percy Liang's type-based MCMC paper.
The second kind of variables are super-entity variables that group similar entities together onto a
single machine, so that proposed swappings are more reasonable and more easily calculated. They
resample assignments to these latent variables as part of their inference process.

There isn't really a good dataset for this kind of task, so they created one. They crawled the web
and found pages that linked to Wikipedia, and they considered all mentions that link to the same
Wikipedia article to be coreferent. They did some filtering of the links they founds to try to
improve the accuracy of their data a bit, as it was understandably noisy. When they ran their
(unsupervised) system on the data, they got a score that was really pretty high. I wonder, though,
if that has to do with how they cleaned the links to Wikipedia - the way the guaranteed high
precision in their testing labels was to throw away the hard cases, essentially, so of course their
performances on those mentions should be relatively high. Still, it's pretty impressive to have
such high performance on such a difficult problem on a really large dataset.

I'm also working on cross-document coreference, but I'm approaching it a little differently.
Instead of modeling it as one big partition problem, I have a known set of real-world entities that
I'm trying to match mentions to (and perhaps propose new ones, but I haven't gotten there yet). The
mentions give additional information about the entities that is used in sampling, so there are
aspects of the partition problem, but the entities exist independent of the corpus, and I think
that simplifies things a bit. But it's harder for me, because I'm trying to match every noun phrase
to a concept in NELL, instead of just a subset of those noun phrases that refer to people or
organizations, or something similar.
