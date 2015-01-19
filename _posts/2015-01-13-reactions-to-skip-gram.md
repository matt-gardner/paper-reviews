---
published: true
title: "Reactions to the skip-gram model (three papers)"
layout: post
author: Matt
tags:
- Skip-gram
- Word Embeddings
- Neural Networks
---

Finishing up (for now) my reading about skip-gram, I'll summarize three papers that provide
different reactions or follow-ons to the skip-gram papers, all of which deal with the difference
between traditional distributional models (that produce representations by looking at word-count
statistics in a corpus) and the new neural-network based models (that directly train
representations to make predictions about the corpus).

The first paper, [Don't count, predict! A systematic comparison of context-counting vs.
context-predicting semantic vectors; by Marco Baroni, Georgiana Dinu, German Kruszewski, ACL
2014](http://www.aclweb.org/anthology/P14-1023), does a very thorough comparison of a number of
traditional word vector techniques with the vectors obtained by the skip-gram method.  The
conclusion is that skip-gram handily beats them all, and thus we should be focusing on methods that
predict things about the corpus instead of counting things about the corpus in order to obtain good
vector representations of words.  One part of their paper gives me pause about the strength of
their conclusion, however - they mention in passing that a different kind of neural network model
fails to outperfrom the traditional (count-based) methods, so if they had done this comparison with
that model instead, their conclusion would have been reversed.  So what they really should be
concluding is that _this particular_ "predict" technique outperforms all _prior_ "count"
techniques.  The next two papers I'll discuss give "count" techniques that outperform (or at least
match) skip-gram, and thus show as incorrect the authors' general conclusion that predicting is
better than counting.

The second paper, [Linguistic Regularities in Sparse and Explicit Word Representations, by Omer
Levy and Yoav Goldberg, CoNLL
2014](http://levyomer.files.wordpress.com/2014/04/linguistic-regularities-in-sparse-and-explicit-word-representations-conll-2014.pdf),
tries to give some better intuition for why the skip-gram models work on analogy tasks - it seems
surprising that they should, as you wouldn't a priori expect that relationships between words are
consistently encoded as linear translations in the vector space learned by these models.  Levy and
Goldberg show that these relationships still exist in what they call the "explicit" vector space
(what Baroni et al. called "count" models), so they are not a product of the neural network
embedding, just preserved by it.  But it turns out that you need to slightly change the similarity
equation to match the performance of skip-gram with an explicit vector space - instead of adding
together the similarities of the words in the analogy, you have to multiply them.  They have some
interesting discussion in their paper that is quite worth reading.

But while Levy and Goldberg only tried to give intuition for why the vector arithmetic works for
analogies in vector space models, the third paper, [GloVe: Global Vectors for Word Representation,
by Jeffrey Pennington, Richard Socher, Christopher D Manning, EMNLP
2014](http://www.aclweb.org/anthology/D/D14/D14-1162.pdf), fully succeeded.  The GloVe paper starts
with a simple observation that relationships between words can be discovered by _ratios of
co-occurrence statistics_.  The example they give is with the words "ice" and "steam".  We can
represent each word by the counts of other words it appears with (a traditional "count" model).
When we want to know what relation "ice" has with "steam", we can look at the ratios of their
co-occurrence statistics with other words.  Both of them will appear frequently with "water", and
infrequently with unrelated words, like "fashion".  "Ice" will appear more with "solid", and less
with "gas".  If we look at the _ratios_ of these statistics, both "water" and "fashion" will have a
value close to 1 (because both "ice" and "steam" occur with those words with similar frequency),
and the words that express the _relationship_ between "ice" and "steam" will have values that are
much higher or lower than 1 ("solid" and "gas", in this example).  It's quite a nice insight.  And
further, ratios of co-occurrence statistics translate to vector differences in log space.  So if
your model looks at log probabilities of co-occurrence, vector addition should be sufficient to
recover analogies, as done in the skip-gram papers.  The authors go on to construct a "count" model
based on these ideas, and show that it outperforms skip-gram (so, it appears, Baroni et al. are
wrong).

Two small notes on this last paper.  First, I think this explains why Levy and Goldberg had to
switch to a multiplication of their similarities in order to get reasonable performance on the
analogy task - they were using PPMI to construct their word vectors, a metric that is a simple
transformation of co-occurrence statistics, not _log_ co-occurrence statistics, so they needed
multiplication instead of addition to recover the relationships (UPDATE: actually, PPMI _does_ have
a log after computing a ratio of counts, so I'm wrong here...  The connection does still seem
interesting to me, but it would need some more exploration in order to really explain this).
Second, Goldberg [wrote a
note](https://docs.google.com/document/d/1ydIujJ7ETSZ688RGfU5IMJJsbxAi-kRl8czSwpti15s/) on the
original (pre-camera-ready copy, I believe) version of the GloVe paper, criticizing its evaluation
(fairly, I think).  The paper was updated in the camera-ready copy to respond to his points, but
the note is still informative, and contains some additional experiments that are worth seeing, if
you're interested in this line of work.

Also, Hal Daume [wrote a blog
post](http://nlpers.blogspot.com/2014/07/reading-group-notes-pointcounter-point.html) on the first
two of these papers that might also be of interest.
