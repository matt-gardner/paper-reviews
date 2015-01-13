---
published: true
title: "Linguistic Structure Prediction, by Noah Smith."
layout: post
author: Matt
tags:
- NLP
---


Ok, this isn't actually a paper, it's a book. But I just finished it, and it's a really good book,
I thought.

The book, as you would expect from the title, explains methods for solving structured prediction
problems. This is in contrast to simple classification or regression problems, where the output is
a single random variable. In structured prediction problems the output space you are predicting
from is exponentially large and thus completely intractable without resorting to approximations,
except in some specific instances.

The book starts out with a description of the prediction task given a model, frequently called
"decoding," and then moves on to learning the parameters of the model, first from complete data and
then from incomplete data. And lastly he talks about the difference between decoding and inference
and gives a description of a few inference problems and how they're solved.

The book is very general, giving methods that apply to HMMs, CRFs, PCFGs, and similar kinds of
problems, and talking about all of them in a similar framework. I was familiar with all of those
models (at least at a cursory level), and this book solidified my understanding of them and helped
to put them in the context of the broader picture of structured prediction in general.
