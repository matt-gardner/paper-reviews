---
published: true
title: "Efficient Estimation of Word Representations in Vector Space; Tomas Mikolov, Kai Chen, Greg Corrado, Jeffrey Dean; ICLR 2013"
layout: post
author: Matt
tags:
- Word Embeddings
- Neural Networks
- Skip-gram
---

I'm a bit late to the word embeddings party, but I just read a series of papers related to the
skip-gram model proposed in 2013 by Mikolov and others at Google.

The idea underlying these papers is that instead of representing a word as just an indicator vector
in some vector space (where the dimension of the vector space is the number of words in your
vocabulary; this is the same as simply using a symbol for each word), we can use a more dense
representation that hopefully encodes something useful.  For instance, we might hope that distance
between words in this new encoding corresponds to similarity in meaning between those words (or
similarity in syntactic function, or both).  This is a very old idea, going back at least to
Firth's [distributional
hypothesis](http://en.wikipedia.org/wiki/Distributional_semantics#Distributional_Hypothesis).

Traditional ideas for generating these vector space representations of words look at the
distribution of contexts the words appear in.  For example, you might observe that the word "candy"
appears in the context of "sweet" \\(x\\) times; the context "candy" would be one of the dimensions of
your vector space, and \\(x\\) would be the value of that dimension for the word "sweet".  A relatively
recent alternative approach is to train a neural network to predict something using the vectors
for each word (such as the next word in a document).  The skip-gram model follows this second
approach.

So, then, we arrive at the first paper in this group: the original skip-gram paper ([Efficient
Estimation of Word Representations in Vector Space; Tomas Mikolov, Kai Chen, Greg Corrado, Jeffrey
Dean; ICLR 2013](http://arxiv.org/abs/1301.3781)).  Mikolov and co-authors present two new models
for producing vector representations of words in a corpus.  They call the first CBOW ("continuous
bag-of-words"), and the second skip-gram (I'm not sure on the motivation for this name...).  The
CBOW model takes the vectors representing each of the words in the context of the index in
question, sums them, and uses the resultant vector to predict the word (so, for instance, you might
take the four preceding words, sum their vectors, and from that vector predict the next word).
This is similar to a traditional bag-of-words model that would use all of the context words as
features to predict the word, but instead of symbolic features, each context word has a vector -
hence the C in CBOW.  The skip-gram model flips this around; instead of using context to predict
the word, this model uses the word to predict each context word.  This forces each word to try to
explain the presence of every other word in its context, while the CBOW model might get away with
only some subset of the context vectors explaining the presence of the word.

Both of these models are very simple, leaving out the non-linearities common in neural network
architectures, which allows them to be trained very efficiently on massive datasets.  And they
work surprisingly well.  The authors evaluated the models on a task they came up with: predict the
missing item in an analogy, like "France is to Paris and England is to London".  They assume that
the relationship between France and Paris is encoded linearly in the vector space, which leads
them to a simple equation: vec(France) - vec(Paris) + vec(London) = vec(England) (hopefully).  So
they created almost 20,000 such analogy questions and saw how many their vector space correctly
modeled.  It was surprisingly high - almost 60% in the best model they tested.  It's not intuitive
at all that such a linear relationship should hold in these vector spaces, particularly over so
many different kinds of analogies (including both semantic, as above, as well as syntactic
analogies).  Fortunately, a later paper (the GloVe paper, which I'll write about soon) provides
some reasonable intuition for why this works.
