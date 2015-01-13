---
published: true
title: "Simple coreference resolution with rich syntactic and semantic features, by Haghighi and Klein, EMNLP 2009."
layout: post
author: Matt
tags:
- Coreference Resolution
---

This is the second of H&K's coreference resolution papers. In a complete departure from their
previous work, the system in this paper is completely deterministic and works with just a few
syntactic and semantic cues. Basically, they come up with a candidate set of antecedents for each
mention and select the one that is closest in the parse tree.

The baseline they use is to only allow antecedents with exactly matching heads, and attach pronouns
to the closest mention in the sentence. It does surprisingly well on their metric, which probably
says that the metric isn't very good (it tends to under-penalize answers where no mention is
coreferent with any other).

They improve on this by allowing mentions with non-matching heads to be coreferent if they match
some simple syntactic constraints. The first thing they do is compute distance in the parse tree
instead of the word sequence, and that helps quite a bit. Then they constrain pronouns to agree in
number and gender with their antecedents, using some really simple rules. Lastly, they use simple
appositive constructions and predicate nominals and one other more technical rule to constrain
syntactic agreement.

To improve on the semantic constraints (loosening the requirement that lexical heads must match),
they learn pairs of acceptable coreferent words, like "president" and "Obama," or "president" and
"leader." They do this from a large collection of unannotated (but parsed) text, doing a little
bootstrapping from the original simple syntactic constraints mentioned previously (appositive
constructions and predicate nominals).

There is no learning in this model (apart from building the semantic constraint portion); it's all
a bunch of rules. It does surprisingly well, however. It outperforms all previous unsupervised
systems and comes very close to state-of-the-art supervised systems. Very impressive.
