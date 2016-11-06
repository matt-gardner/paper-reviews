---
published: true
title: "Takeaways from EMNLP 2016"
layout: post
author: Matt
tags:
- Conference takeaways
---

This is lightly edited from an email I sent to colleagues at AI2, so it's somewhat AI2-specific in
places.  But, here's what I thought about EMNLP.

## My main takeaway:

Things are moving _fast_.  This was epitomized for me in one of the presentations (I think it was
the EpiReader paper, mentioned below), which had a slide about "posterior work" at the end of the
talk, discussing four papers that have since surpassed the EpiReader, after the EpiReader paper was
posted on arxiv.  Similarly, I'm sure most of you are familiar with the [SQuAD
dataset](https://www.semanticscholar.org/paper/SQuAD-100-000-Questions-for-Machine-Comprehension-Rajpurkar-Zhang/8e766b965042e369e45f3fa3062a1a016eee2100),
as [Minjoon Seo](http://seominjoon.github.io/) built a system for it during his internship at AI2,
and his state-of-the-art performance has since been surpassed a couple of times.  But did you know
that the SQuAD paper was an EMNLP submission?  It was just officially presented two days ago,
getting the best new resource award.  It feels like old news, with system performance already in
the 80s (human performance is low 90s).  That's how a lot of the conference felt to me - the action
is all happening on arxiv now (and twitter, I guess, where people announce things, but I don't
follow that as much).

Another nice takeaway was that AI2 seems to be getting some good traction in the community - the
SQuAD presentation mentioned AI2 as having the state-of-the-art on the dataset for a while, and in
several questions at various papers, AI2 was mentioned.

## Some area-specific observations:

### Dialogue / conversational agents:

All three of the invited talks dealt with conversational agents of various kinds:

- Christopher Potts talked about using Gricean principles to build pragmatic, rational speakers and
  listeners (similar to what Jacob Andreas talked about when he came to visit AI2 a few weeks ago -
also an [EMNLP
paper](https://www.semanticscholar.org/paper/Reasoning-About-Pragmatics-with-Neural-Listeners-Andreas-Klein/f3df66caf651c04061aa7afef3d44b129a0df402)).
- Stefanie Tellex talked about human-robot collaboration, with some cool videos including a robotic
  forklift that you could talk to, a quadcopter, and a furniture-building collaboration between a
person and a robot, where the robot would ask for help using a pragmatic process similar to what
Christopher Potts mentioned.
- Andreas Stolcke talked about detecting machine-directed speech in human-human-computer
  interactions.  His finding was that we've adapted our speech to speak to computers, and so
computer-directed speech is pretty easy to spot with acoustic signals alone.  I guess we'll have to
find new methods when the computers get better at speech recognition, and we stop adapting our
speech so much when we speak to them.

### Reading comprehension / memory networks:

- [Key-value memory
  networks](https://www.semanticscholar.org/paper/Key-Value-Memory-Networks-for-Directly-Reading-Miller-Fisch/e2007ef0d8575ae1315030125d607eddeaa4c3a2):
a slight modification on the original memory network idea, where you have separate vectors for
addressing and reading from memory (except the original memory network did this too, only in a much
more hacky way).  They also released a large dataset focused on question answering with both a KB
and text.  The problem is that the questions are generated using templates.  Daniel Marcu got up
during QA for this talk and basically said that the dataset was garbage, because it was
procedurally generated, and Facebook AI Research should stop generating datasets like this (I'm
inclined to agree).
- [EpiReader](https://www.semanticscholar.org/paper/Natural-Language-Comprehension-with-the-EpiReader-Trischler-Ye/758a86e06d02922789e648843292321433deb66f/figure/0):
  a new reading comprehension method, evaluated on CNN/Daily Mail and Facebook's Children's Book
test datasets, that adds a separate hypothesis-testing step after performing an initial extraction
similar to what prior reading comprehension models do.
- [Who Did What
  dataset](https://www.semanticscholar.org/paper/Who-did-What-A-Large-Scale-Person-Centered-Cloze-Onishi-Wang/fa7d9d2ee4fbbf2021e8578a3c0011112520096b/figure/0):
an improvement on top of the CNN / Daily Mail datasets that uses two news articles for each
question, instead of an article and a summary.  System performance is quite a bit lower on this new
dataset, and human performance is higher.  Human performance has basically been reached already on
the CNN datasets, but not on this one.

### Structured prediction:

- There were a ton of papers that used the [REINFORCE
  algorithm](https://www.semanticscholar.org/paper/Simple-Statistical-Gradient-Following-Algorithms-Williams/ded7af18ccd67c0d2ab780d996a2078e911fb849)
to do a simple kind of reinforcement learning for structured prediction models.  I need to learn
more about how this works...
- There was a [workshop on structured prediction for NLP](https://structuredprediction.github.io/)
  with some pretty interesting presentations.  Dhruv Batra had a talk about diversity in beam
search that I thought was really cool.  Basically, you time-delay subsequent particles in the beam,
and impose a penalty for later particles using the same predictions as earlier particles.  This
lets you find several different modes of the posterior distribution, instead of just several
particles all from the same mode.  He had some nice demos on image segmentation and image
captioning presented from http://cloudcv.org/, but I couldn't find his demos there - they might not
be ready for public consumption yet.
- Jason Eisner had a [tutorial paper](https://structuredprediction.github.io/final/11/11_Paper.pdf)
  at this workshop on the connection between the inside-outside algorithm and backprop, which I
thought was a helpful insight.

### DyNet tutorial:

I went to a [tutorial](https://github.com/clab/dynet_tutorial_examples) by Chris Dyer, Yoav
Goldberg, and Graham Neubig on DyNet, a neural net library for dynamic computation graphs, instead
of the static computation graphs compiled by more common neural net libraries (like theano,
tensorflow, caffe, torch, etc.).  Structures in language vary across instances much more than they
do in images, so dynamic computation graphs are a lot more useful.  For example, sentences have
varying length, and you might want to gives words their own embedding sometimes, but treat rare
words as sequences of characters; this is hard in static computation graphs, but easy in DyNet.
You should think of DyNet as a neural net library written by NLP people for NLP problems, whereas
most of the other libraries are written by vision people for vision problems.  The main drawback of
DyNet is that it's hard to do batching - to do batching you pretty much have to build a static
graph anyway, so you lose a lot of the benefits that DyNet gives you.  And without batching, DyNet
is significantly slower than other frameworks that have static computation graphs.

Another benefit of DyNet is that it should be easier to do structured prediction.  Also, Jayant and
Oyvind are looking into producing scala bindings for DyNet.

### Sentence compression / summarization:

There were a number of papers on sentence compression and abstractive / extractive summarization.
This is relevant to [Johannes'](https://www.semanticscholar.org/author/Johannes-Welbl/1851564)
internship project, so I went to these talks.

- There was a
  [paper](https://www.semanticscholar.org/paper/Language-as-a-Latent-Variable-Discrete-Generative-Miao-Blunsom/28196eb5d53a1129133b2977b7613c277596ccc6)
by some folks at DeepMind that does sentence compression with discrete latent variables (using
language as the compressed representation, instead of some continuous representation).  The
methodological innovation for this was pretty interesting.
- Kristina Toutanova had a
  [paper](https://www.microsoft.com/en-us/research/publication/dataset-evaluation-metrics-abstractive-sentence-paragraph-compression/)
releasing a dataset for abstractive summarization.
- There was a lot of mention of [Sasha
  Rush's](https://www.semanticscholar.org/paper/A-Neural-Attention-Model-for-Abstractive-Sentence-Rush-Chopra/468b9055950c428b17f0bf2ff63fe48a6cb6c998)
[papers](https://www.semanticscholar.org/paper/Abstractive-Sentence-Summarization-with-Attentive-Chopra-Auli/7a67159fc7bc76d0b37930b55005a69b51241635)
as baseline state-of-the-art models for this work.
- Kristina told me that Greg Durrett had some [code and
  models](https://github.com/gregdurrett/berkeley-doc-summarizer) available that would be a good
thing to try for Johannes' project.

### Other interesting papers:

- Chloe Kiddon (a recently-graduated UW student) had [an interesting
  paper](https://homes.cs.washington.edu/~yejin/Papers/emnlp16_neuralchecklist.pdf) on generating
recipes given an ingredient list and a recipe title.  The interesting innovation here was keeping
track of which ingredients had been used already in a soft way, with neural techniques.  This
reminded me of the used/free vector for memory cells in the [differential neural
computer](http://www.nature.com/nature/journal/v538/n7626/full/nature20101.html) by DeepMind.  I
wonder if you could get this kind of general framework to perform similarly to the specific model
that Chloe used.

### Some papers and notes that are relevant for [Semantic Scholar](semanticscholar.org):

- I was able to find S2 links for most of the papers I mentioned here, but not for workshop papers,
  and not for papers that weren't already posted on arxiv, it seemed like.
- All EMNLP talks are recorded, this year and last year (and maybe earlier, and maybe other
  conferences too).  Can we find these videos and link to them?  I tried to find videos from last
year, and found a [vimeo playlist](https://vimeo.com/emnlp) that didn't look easy to automatically
scrape.  But maybe talking to the program chairs would get us better access to indexing and linking
these videos?
- Feature request that came up during a conversation: why can't we select multiple venues at the
  same time?  E.g., I might want to filter search results to only papers that have appeared in
EMNLP, ACL, NAACL, or EACL.  You can't do this in the current UI.
- There were a
  [couple](https://www.semanticscholar.org/paper/All-Fingers-are-not-Equal-Intensity-of-References-Chakraborty-Narayanam/a59cafd1b42dd3b6e7442933a5390bd70616ab91)
of [papers](http://www.aclweb.org/anthology/W/W16/W16-6109.pdf) related to our "highly influential"
citation classification.
