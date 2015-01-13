---
published: true
title: "This is Watson"
layout: post
author: Matt
tags:
- Question Answering
---

[This is Watson](http://ieeexplore.ieee.org/xpl/tocresult.jsp?reload=true&isnumber=6177717), a
series of papers describing IBM's Watson system that beat Ken Jennings at Jeopardy.

I was just in a reading group where we each picked a paper from this journal issue and discussed
the various components of Watson. It was pretty interesting. What was most surprising was how
rule-based everything was. There were just a few parts that used machine learning systems (most
notably the final answer ranker, which took as input the scores given by lots of subsystems and
used logistic regression to give a final score). I read a paper on answering tri-bond style
questions (given three things, tell what is similar about them); their method for solving those
questions was brain dead simple - they just looked for a word that was in collocations frequently
with all three things, given a large 5-gram corpus.

Our final evaluation of the system was that it was an amazing engineering accomplishment that did
really well at factoring a big problem into smaller problems, and at consistently improving
performance at the overall objective. Their improvements were gradual, but given enough tuning,
they were able to take their system to championship level. This was quite an engineering
accomplishment. But there wasn't that much from a research perspective that came out of it (there
was some, I will grant that; just not much). Not to bag on engineering - they give us great
products - it's just a different line of work.﻿
