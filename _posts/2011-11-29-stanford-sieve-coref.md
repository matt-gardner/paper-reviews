---
published: true
title: "Stanford's Multi-Pass Sieve Coreference Resolution System at the CoNLL-2011 Shared Task, by Lee, Peirsman, Chang, Chambers, Surdeanu, and Jurafsky."
layout: post
author: Matt
tags:
- Coreference Resolution
---

This system had the highest coreference resolution performance on the shared task, and this paper
is a write up describing the system.

There were two interesting things about this paper. The first is that it is a state-of-the-art
system that is purely deterministic and rule-based. Thus there is no training of the system
required, and prediction is probably very fast. The second is the nature of their rule-based
system. The idea is that they apply each of their rules one at a time, going from highest precision
to progressively lower precision and higher recall, hoping to pick up coreferent mentions that
earlier rules (or "sieves") missed. One of their sieves uses information from Wikipedia or
Freebase, which I thought was interesting, but it actually hurt performance a little bit in the end
and was disabled for their final submission.
