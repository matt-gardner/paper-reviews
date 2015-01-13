---
published: true
title: "Distributed Representations of Words and Phrases and their Compositionality; Tomas Mikolov, Kai Chen, Greg Corrado, Jeffrey Dean; NIPS 2013"
layout: post
author: Matt
tags:
- Word Embeddings
- Neural Networks
- Skip-gram
---

The second word embeddings paper I'll discuss is the [second main skip-gram
paper](http://papers.nips.cc/paper/5021-distributed-representations-of-words-and-phrases-and-their-compositionality.pdf),
a follow on to the original ICLR paper that basically drops the CBOW model and focuses on scaling
up the skip-gram model to larger datasets.  This paper gives three main contributions, I would say.
First, they provide a slightly modified objective function and a few other sampling heuristics that
result in a more computationally efficient model.  Second, they show that their model works with
phrases, too, though they just do this by replacing the individual tokens in a multiword expression
with a single symbol representing the phrase - pretty simple, but it works.  And lastly, they show
what to me was a very surprising additional feature of the learned vector spaces: some
relationships are encoded compositionally in the vector space, meaning that you can just add the
vectors for two words like "Russian" and "capital" to get a vector that is very close to "Moscow".
They didn't do any kind of thorough evaluation of this, but the fact the it works at all was very
surprising to me.  They did give a reasonable explanation, however, and I've put it into math
below.

The probability of two words \\(i\\) and \\(j\\) appearing in the same context in this model is
proportional to \\(e^{v\_i \cdot v\_j}\\).  Now, if we have a third word, \\(k\\), and its
probability of appearing with _both_ word \\(i\\) and word \\(j\\) is proportional to \\(e^{v\_k
\cdot v\_i} e^{v\_k \cdot v\_j} = e^{v\_k \cdot (v\_i + v\_j)}\\).  So what you get when you add
the vectors for two words is something that is likely to show up in the contexts of _both_ of them.
Thus if you pick word \\(i\\) to be "Russian" and word \\(j\\) to be "capital", a word \\(k\\) that
has high probability might very well be "Moscow", because it tends to show up in the context of
both of those words.  So we can see that this method does have some reasonable explanation for why
it works, but I expect that it is very brittle - I would guess that adding "Russia" and "capital"
(instead of "Russian" and "capital") would not work nearly so well, for instance.  And this is
probably why the authors only gave a handful of token examples of this phenomenon, instead of a
more thorough evaluation.

Also, I'll point out an arXiv note that expounds a bit on skip-gram.  The equations in the original
papers are not motivated or explained very well, and this arXiv note ([word2vec Explained: Deriving
Mikolov et al.'s Negative-Sampling Word-Embedding Method, by Yoav Goldberg and Omer
Levy](http://arxiv.org/abs/1402.3722)) does a better job at explaining the technique.
