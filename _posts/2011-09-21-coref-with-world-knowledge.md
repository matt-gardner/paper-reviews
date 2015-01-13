---
published: true
title: "Coreference Resolution with World Knowledge, by Altaf Rahman and Vincent Ng, ACL 2011"
layout: post
author: Matt
tags:
- Coreference Resolution
---

The premise of this paper is that systems that try to solve the coreference problem have typically
relied on linguistic knowledge encoded into the algorithms. However, they have largely ignored
world knowledge, which the authors argue is an important type of knowledge for determining the
antecedent of anaphoric noun phrases. The authors address this gap in the literature by augmenting
existing coreference resolution systems with features derived from several sources of world
knowledge.

I thought this paper was interesting, but it largely ignored the work of Haghighi & Klein (NAACL
2010) that presented a better approach to coreference resolution by learning about entities. I'm
curious to know how they would apply their methods for adding world knowledge to Haghighi & Klein's
approach. I have some ideas there, so we'll see how well that goes.

I thought that one of their types of "world knowledge" was a little strange. They had labeled
coreference data, they learned some features from it, and they called it "world knowledge" because
it captured things like "Barack Obama" and "president" are likely candidates for coreferent noun
phrases. Most people would just call that "supervised learning."
