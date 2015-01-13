---
published: true
title: "Filling Knowledge Gaps in Text for Machine Reading, by Anselmo Peñas and Eduard Hovy, COLING 2010."
layout: post
author: Matt
tags:
- Common-sense reasoning
---

I mentioned that I saw a talk by Ed Hovy, and so I put a bunch of his papers on my reading list.
This was one that he mentioned in his talk, and I think it's pretty fascinating.

The gist is that there is a lot going on in real-world sentences that is does not just fall out of
simple constituency or dependency parses. For example, in the phrase "a seven-yard Young touchdown
pass," those parsers would just give you a bunch of noun-noun or adjective-noun constituents.
That's nice, but it doesn't tell you the semantics of the phrase. On the flip side, semantic role
labelers might just skip over the noun "pass" as not needing further analysis. What this paper
does, essentially, is recognize when phrases (noun-noun compounds, specifically) are in need of
further semantic analysis and try to fill in the blanks. Their system turns the phrase "a
seven-yard Young touchdown pass" into something more like this: "a seven-yard pass that Young threw
for a touchdown." That's obvious to a human reader, but very difficult for computers, and it's
pretty impressive that they were able to do it.

They accomplish this by building up a big database of distributional semantics over words and part
of speech labels. This database consists of sequences of coarse part of speech tags, like N:V:N,
along with counts for each set of words seen with that part of speech sequence (they actually do a
dependency parse and then simplify it down to those sequences, so it's not as naive as just running
a POS tagger).

When they come across a noun-noun compound that they want to enrich, like "touchdown pass," they
look in their database of counts for sequences that use those two nouns that make sense. In this
instance they come up with a N:P:N sequence, pass:for:touchdown. They can get as specific as there
are counts for, so they can do queries like "Young:throw:pass:?:touchdown." They also do some
hierarchy and category instance learning, so that they know "Young" is a "quarterback,"
"quarterbacks" are "players," and "players" are "people." If they don't have enough evidence at one
level, they can go up the tree until they reach a point where they can make some conclusion.

I think all of this is really exciting, and it's very similar to something I'm currently working
on. Why should you stop with part of speech sequences? You should get down to semantic roles, and
keep your counts at that level, and then you should use the output of this system to augment your
counts that come from the coarser semantic parser. I think this has some nice potential for
bootstrapping, and a propositional knowledge base could also be added to do some additional cool
stuff.
