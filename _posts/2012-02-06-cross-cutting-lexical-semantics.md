---
published: true
title: "Cross-Cutting Models of Lexical Semantics, by Joseph Reisinger and Raymond Mooney, EMNLP 2011."
layout: post
author: Matt
tags:
- Semantics
---

The premise of this paper is that current distributional measures of word similarity are deficient.
Topic models and context vectors only give a single measure, and intuitive measures of similarity
using these models do not satisfy the triangle inequality ("bat" is similar to "club," and "club"
is similar to "association," but the sum of those two distances is less than the distance from
"bat" to "association"). Also, measuring similarity between each pair of words might require using
different features for each pair ("wine" and "vinegar" are similar, as are "wine" and "bottle," but
each pair is similar for different reasons).

To try to solve these problems, they use an interesting model that clusters word features into
"views," then clusters words within each "view." The feature clusters are found using a topic
model, and allow for the same feature to appear in multiple views. The idea is that each view
represents a particular kind of similarity, and words in each cluster in that view are similar in
the way determined by the view (they show past tense verbs as one cluster in a syntax-driven view,
for instance).

I thought the idea was interesting, as was the model. As much as I am averse to qualitatively
driven results sections in topic model papers, I would have liked to see more of it here. They did
a nice "Reading Tea Leaves"-esque evaluation (and I was happy that they did), but they focused on
it so much that I didn't end up feeling like I had a good idea of the actual output of their model.

The main reason I'm writing about this paper here, though, was because of something I thought of as
I was reading the paper. How are "wine" and "vinegar" similar? Think about that for a minute.
Chances are you said something like, "they are both liquids," or "you can drink both of them," or
"they are both used in cooking," or "vinegar is made from wine." Those are statements of
propositional semantics, not distributional semantics. Distributional semantics are good for some
things, but it seems to me that humans use propositions to determine word similarity. And you could
measure that similarity by doing a random walk over NELL's knowledge base from one word to the
other, seeing what paths get you there.
