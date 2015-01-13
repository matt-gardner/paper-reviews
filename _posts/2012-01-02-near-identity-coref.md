---
published: true
title: "A Typology of Near-Identity Relations for Coreference (NIDENT), by Marta Recasens, Eduard Hovy, and M. Antonia Marti, LREC 2010."
layout: post
author: Matt
tags:
- Coreference Resolution
---


I thought this paper was interesting. They argue that many cases in coreference resolution are more
complicated than simple binary decisions, and so they introduce "near-identity" relations,
somewhere in between saying two entities are coreferent and not coreferent. I thought they had some
good examples, but in the end I found their typology not incredibly persuasive. I would have said
most of them were not coreferent and dealt with the subtlety another way. I'll give some of their
examples below, with the entities that are coreferent or near-identity in italics.

Last night in Tel Aviv, Jews attacked a restaurant that employs Palestinians. " We want war," the
crowd chanted.

The Clinton campaign is circulating a fake photo of Barack Obama in Muslim clothes to damage his
reputation. In the photo, Obama wears a long sari-like garment.

The Clinton campaign is circulating a fake photo of Barack Obama in Muslim clothes to damage his
reputation, but Obama never wore Muslim clothes.

The above two contrasting sentences are particularly interesting, because a simple analysis would
have the two being actually coreferent in the first sentence, leading to the erroneous conclusion
that Obama wore a long sari-like garment, when in fact he did not; the fake Obama did.

There are some other interesting examples in the paper where pronouns are used, which would make
you think that the entities are coreferent, but in fact they are only near-identity. For example:

In France, the president is elected for a term of seven years, while in the United States he is
elected for a term of four years.

Language is much more complicated than speakers tend to think it is, and it's really hard to get
all of these things right when a computer is processing the language. Studying linguistics in more
depth the last few months has been really eye-opening for me.
