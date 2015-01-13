---
published: true
title: "Integrating Semantic Frames from Multiple Sources, by Namhee Kwon and Eduard Hovy, CICLing 2006"
layout: post
author: Matt
tags:
- Semantics
---

[Integrating Semantic Frames from Multiple
Sources](http://www.isi.edu/natural-language/people/hovy/papers/06CICLing-frames-hovy.pdf), by
Namhee Kwon and Eduard Hovy, CICLing 2006 (I had never heard of that conference before; this was a
keynote talk that year by Ed Hovy, incidentally).

The gist of this paper is that there are several difference resources for defining semantic roles
of verbs: FrameNet, PropBank, VerbNet, and the LCS database (which I hadn't ever heard of, though
apparently it is similar in some respects to VerbNet). Each of these resources will tell you,
essentially, what different arguments can go with a verb, and have some amount of data with real
sentences and labeled arguments (e.g., "give" has a giver, a recipient, and a thing given. "I gave
the book to John" would be an example sentence, with giver="I", recipient="John", and thing
given="book"). The problem is that they don't have identical labeling or an easy mapping between
them. This paper tries to create such a mapping, and they do a somewhat decent job (accuracy of
around 75%, depending on what exactly you're measuring).

I got this paper from Ed Hovy's website after I heard a talk by him that I really liked. Given
where it was published and that it only has 5 citations, I doubt I would have come across it any
other way. I know that I need to become more familiar than I am with these resources, so it was
interesting to read a bit about them. There may be easier ways to learn about PropBank, however, so
I'm not sure this is the most helpful paper out there for anyone reading this.
