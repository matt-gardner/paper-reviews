---
published: true
title: "Coreference resolution across corpora: languages, coding schemes, and preprocessing information, by Marta Recasens and Eduard Hovy (ACL 2010)"
layout: post
author: Matt
tags:
- Coreference Resolution
---

This paper discusses problems with evaluating coreference resolution systems. There are three
standard metrics used (B^3, MUC, and CEAL); Recasens and Hovy did a controlled comparison of these
evaluation metrics across a number of different scenarios. The problem is that they all produce
different rankings of algorithms, sometimes in really bad ways (the highest scoring B^3 algorithm
was the lowest scoring MUC algorithm, for instance).

They also found that it was better to leave out syntax features than to get syntax from the Malt
Parser, because the noise made the features harmful instead of helpful. Maybe that was because
their data was relatively sparse - only about 300 documents. One noisy parse might have a big
impact for a particular feature in that case.
