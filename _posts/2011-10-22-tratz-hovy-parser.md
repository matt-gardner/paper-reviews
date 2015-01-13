---
published: true
title: "A Fast, Effective, Non-Projective, Semantically-Enriched Parser, by Stephen Tratz and Eduard Hovy"
layout: post
author: Matt
tags:
- Dependency Parsing
---

I saw a talk by Eduard Hovy a week ago that I thought was really interesting. It was about merging
propositional and distributional semantics and was very close to some things I had already been
thinking about. So I went to Hovy's website and printed off all of his recent papers that looked
interesting. I was interested in this one because I thought "Semantically-Enriched" meant that the
parser used some form of semantics as input, which I thought would be really cool. Turns out it
doesn't, so that was disappointing, but the paper was still interesting.

So the gist of this paper is that they took a fast, easy-first dependency parsing algorithm and
made it a little bit better. "Easy-first" means that at each step of the algorithm you find the
best scoring attachment and do that one, so you can implement the parsing algorithm in O(nlogn)
time, which is really pretty good, considering standard constituency parsers are O(n^3). They have
a slightly inefficient, but easier, implementation that actually runs in O(n^2) instead of
O(nlogn), but it still can parse 75 sentences a second, with fully labeled dependencies, which is
really quite impressive (I've used the Stanford dependency parser, and it was 1 sentence per second
or two).

They made their baseline algorithm better by adding a step to handle non-projective dependencies
(about 8% of the sentences in their data - the Penn treebank - had at least one non-projective
link), by adding labels to the dependencies (the Stanford dependency labels plus some of their own
tweaks), and by adding more features. Sadly, they say, "One of the key aspects of the parser is the
complex set of features used," and then they don't actually describe their features in the paper,
making the reader download and browse through their code to figure out what they are actually
doing.

They train their model using a fairly typical structured perceptron, it looks like.

Their results are impressive - they unquestionably beat all other algorithms they presented, using
a fraction of the time. The Stanford dependency parser was noticeably missing from their
presentation, however, and it wasn't clear to me why that was. They ended up with 93.7% unlabeled
arc accuracy. The baseline was 91.2%, and almost all of the improvement came from the features that
they failed to describe in the paper - without using the non-projective addition, only the extra
features, they get 93.3%, only .4% lower than their full model. They do perform way better on
non-projective arcs, though, going from 21.1% to 67.7% accuracy.

The "Semantically-Enriched" part of their parser just meant, "and we can run some cool stuff at the
end, too, to give you more information about the sentences." That's nice, but it seemed really
orthogonal to the point of the paper, just taking up space that should have been devoted to
describing their features that did so well. Their presentation about that was basically, "We used
these other components that are explained in these other papers, and by the way, the accuracy is
about the same as it was then." It really didn't add anything to the paper, which was
disappointing, because that was the main reason I read it in the first place.

The paper was still interesting, and I'm glad I read it. It's good to know about a really fast,
pretty accurate, fully labeled dependency parser that's freely available to download.
