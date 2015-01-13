---
published: true
title: "Toward Completeness in Concept Extraction and Classification, by Eduard Hovy, Zornitsa Kozareva, and Ellen Riloff, EMNLP 2009."
layout: post
author: Matt
tags:
- Relation Extraction
---

This paper deals with automatically constructing an ontology, or hierarchy, of concepts from a
corpus. Their whole approach is essentially to use the phrase "such as" in a couple of ways to find
hyponyms and hypernyms of words in a bootstrapping approach starting with two seed words. They
start with "animals such as lions and _ ", and go from there to get other instances of animals.
Once they've done that, they use all pairs of these animals that they have found and look for the
phrase " _ such as lions and [other animal, like tiger]." Maybe that returns "felines" or "cats,"
so you use that as a new initial search term, in "felines such as tigers and _ ." If you do this
enough times, you can get some idea of what kinds of groupings there are among words and what
things fit into each grouping.

This isn't all that dissimilar from what we're doing with NELL, except we are interested in finding
instances of categories in a known ontology, and we use many more features than "such as." We do
restrict ourselves to binary data, so their use of three things (animal, lion, and the unknown)
does help to anchor what you're looking for a little bit better. Instead of the third noun phrase,
we use relationships between categories.

NELL also does a little bit of proposing new categories on its own, but I think that is still
pretty early and isn't nearly as extensive as this.

Their evaluation isn't exactly compelling, but it's really hard to get good ground truth data to
compare against in this space. I know we don't have that much that's very good, either.
