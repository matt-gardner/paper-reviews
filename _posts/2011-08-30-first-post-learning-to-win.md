---
published: true
title: "First post! Learning to Win by Reading Manuals in a Monte-Carlo Framework, by Branavan, Silver, and Barzilay"
layout: post
author: Matt
---

I'm going to be reading a lot of research papers here soon, and I thought I might try sharing what
I've been reading here, for two reasons.

First, I suppose that most of the people who see these posts probably won't be interested in them,
but some of you will be. I'm hoping that sharing these papers with those who are interested will
spark some discussion that will be helpful for me and for you, about related papers that I should
be reading and how the ideas apply to problems we're working on.

Second, I'm also sharing them with a private circle that I've created (an idea that was originally
created (probably) by +Arun Shroff), so that I can keep track of the papers I've read. We'll see if
that ends up being useful or not.

So, for my first research paper: "Learning to Win By Reading Manuals in a Monte-Carlo Framework,"
by Branavan, Silver, and Barzilay at MIT. Their goal is to use the text from the game manual to
Civilization II as a means to building a better AI for the game. If you can read the book, the
thinking goes, you can get strategy out of it to help with gameplay. Pretty cool idea. I originally
saw this paper mentioned on Ars Technica a few months ago, but I went back to it at the
recommendation of +Jon Clark and some others.

So how do they do it? They model the game as a Markov Decision Process (MDP), where at each state s
you can take an action a from some possible set of actions. They extract features from the states
and actions and from each sentence in the book to try to classify which sentence is most relevant
to the current state. For example, the state could be "in a square with a river and hills," the
action is "build a city," and the sentence from the manual says, "Try to build cities in
grasslands, preferably with a river running through it." They do some fancy simulation to learn
this classifier actively, and it turns out to work pretty well at getting high-level strategy from
the manual.

They present some evidence that shows you can get a similar effect by just using random text (that
was shuffled from the original game manual), though not as pronounced. So maybe their AI model just
needed to be able to learn a little bit of non-linearity that the additional state space (the
associated text) gave them. The random text doesn't perform quite as well as the actual manual, so
they take that as a good sign. But the random text did way better than their baseline and only a
little bit worse than the manual, so I wasn't quite as impressed.

So why do I care about this? I think it would be really cool to have a computer read a reference
grammar for some low-resource language and use the information found there to improve performance
on an unsupervised NLP task, like morphological analysis. So seeing how they get information out of
the game manual is pretty relevant to my research interests.
