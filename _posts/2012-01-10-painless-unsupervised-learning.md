---
published: true
title: "Painless Unsupervised Learning with Features, by Taylor Berg-Kirkpatrick, Alexandre Bouchard-Cote, John DeNero, and Dan Klein, NAACL 2010."
layout: post
author: Matt
tags:
- Unsupervised Learning
- NLP
---

I was at NAACL 2010 and saw [this paper](https://www.aclweb.org/anthology/N/N10/N10-1083.pdf)
presented, and a lot of it went over my head. Now, having taken a course and read a textbook on
structured prediction, it was a lot easier than I seemed to remember it being. The beginning is a
little math heavy, understandably, but the entire second half of the paper is just a list of models
you can apply this technique to, with results for each one.

There isn't that much more to explain here than the title - typically, unsupervised learning has
been done with generative multinomial models, because that's what people know how to do. In
supervised learning it has recently been made abundantly clear that the ability to use arbitrary
(though hopefully locally factored) features in a model gives it much better performance than
simple multinomial models. This paper shows a general method for using those same kinds of features
in unsupervised learning, replacing locally-normalized multinomial models with locally-normalized
logistic regression models.

It turns out you can still use EM in this case. The E step is the same (with a minor detail I won't
go into here), and in the M step where you would normally do a simple, closed form calculation to
maximize your model parameters given expected counts from the E step, instead you take a step down
the gradient using LBFGS, because there is no closed form solution anymore. You can also just
calculate the gradient of the log likelihood function and optimize it directly, bypassing EM and
giving better performance in the process, for some of their experiments.

For their results they give four examples (POS tagging, dependency parsing, word alignment and word
segmentation), and on all of them they present state-of-the-art unsupervised results. Very
impressive. This is an important paper to know about and understand, I think.

