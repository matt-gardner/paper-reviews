---
published: true
title: "An Entity-Level Approach to Information Extraction, by Haghighi and Klein, ACL 2010."
layout: post
author: Matt
tags:
- Relation extraction
---

[This](http://dl.acm.org/citation.cfm?id=1858896) is the last of H&K's coreference resolution
papers, and as you can see, it's not actually about coference resolution, per se. I include it in
the group because essentially all they do is take their NAACL 2010 system and modify it slightly to
perform a template-filling task for information extraction. That's very similar to the kind of
extension I'm looking at, though I'm taking a pretty different approach than they used.

This was a short paper (5 pages) and the bulk of it is describing their model, which is incredibly
similar to the NAACL 2010 paper. There's not a lot new in this paper, except that instead of the
type hierarchy they had in their previous system, they have a set of roles as the underlying types.
There's an odd one-to-one correspondence that they mention between entities in a document and roles
which I don't think they explained very well (probably due to their space constraints). They say
that each role can be filled by at most one entity, but if that's actually the case, they don't
have any reasonable way to learn the back-off multinomial for each role. I think they instead meant
that in each document there can be at most one entity filling a particular role, but that still
seems like an overly-limiting assumption.

Anyway, I wasn't particularly thrilled with this paper, because the method seemed at least a little
contrived. They do report the best results so far on their dataset, but they didn't compare against
other IE papers that I'm familiar with on datasets I know about, so I'm not sure how convinced I am
by the results they report. It was at least interesting to see the approach that they took to using
their coreference system to aid in information extraction.
