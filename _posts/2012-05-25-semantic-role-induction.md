---
published: true
title: "A Bayesian Approach to Unsupervised Semantic Role Induction, by Ivan Titov and Alexandre Klementiev. EACL 2012"
layout: post
author: Matt
tags:
- Semantic Role Labeling
---

Semantic role labeling is the task of determining what the arguments of a verb are. For instance,
in "The lion ate the deer," the verb "ate" has two semantic roles: the agent (the lion) who does
the eating, and the patient (the deer) who was eaten. The roles stay the same even if the syntax
changes; in "the deer was eaten by the lion," the deer is now the syntactic subject of "was eaten,"
but it is still the patient in terms of semantic roles.

This paper takes as input a bunch of parsed sentences and essentially does some clustering on all
of the verb arguments to try to figure out which ones correspond to the same semantic role. They
arguments that they cluster have two components: the syntax in which the argument appeared (for
instance, they use "ACT:LEFT:SBJ" to mean "governed by an active verb, on the left of the verb, and
the parse tells me this is the subject"), and the head word of the argument (which hopefully tells
you something of the semantics). Separating the syntactic decision from the semantic one like this
seems to be a pretty good idea.

In the first model they presented, they used a CRP to do the clustering, modeling each predicate
independently. They also presented a version that uses a distance-dependent CRP, and they induce
the distances using block coordinate ascent between the partitioning and the distance matrix
(inducing the distances was pretty cool).

Their results were quite good for an unsupervised system (though so was previous work - I suppose
semantic role labeling is an easier problem than I thought it was?). Using "purity" and
"collocation" as unsupervised surrogates of precision and recall, they report an F1 of 83 (the best
previously published result was 80.1).
