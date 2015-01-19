---
published: true
title: "Reducing the Rank in Relational Factorization Models by Including Observable Patterns; Nickel, Jiang, and Tresp, NIPS 2014"
layout: post
author: Matt
tags:
- Tensors
- Knowledge Base Inference
---

I really enjoyed [this
paper](http://papers.nips.cc/paper/5448-reducing-the-rank-in-relational-factorization-models-by-including-observable-patterns),
and it had a significant impact on my research direction.  I am looking at combining compositional
models of KB inference with models based on factorizing a KB tensor (or otherwise producing
relation embeddings).  That's what this paper does too, though it does it in a different way than I
was planning.  The key insight of this paper is that some patterns in a KB tensor are very
difficult to capture with a low-rank factorization, but are easy when a model has access to the
original tensor.  This paper solves that issue by making a factorization only capture those things
that are not captured by features extracted from the original tensor.

The paper begins with a theorem that gives upper and lower bounds on the rank required to recover
an adjacency tensor with a factorization model (KB tensors are adjacency tensors).  They show the
necessary rank depends on certain properties of the graph - the more strongly connected components
there are of any particular edge type in the graph, the higher the rank of the factored model must
be.  While this proof is interesting and provides some motivation for the rest of the paper, they
don't evaluate anything to do with the theorem after stating the proof, nor do they even
explicitly tie the methods they introduce to the theorem they proved.  It seems intuitive that
using features derived from the full-rank tensor will help to reduce the rank of a factored model
explaining the residual, but if you're just relying on intuition for this, why give a proof at
all?  Anyway, the proof is interesting, I just thought it could have been better integrated with
the rest of the paper, by calculating the bounds on the tensors they tested with, for instance.

After the proof, the authors introduce their model (additive relational effects, or ARE).  It is
an extension of the RESCAL factorization model that only requires the model to explain what can't
be explained by features from the non-factored tensor.  The RESCAL model approximates the tensor
as:

\\(\mathbf{X} \approx \mathbf{R} \times\_1 A \times\_2 A\\)

where \\(\mathbf{X}\\) is the KB tensor, with dimension \\(N \times N \times K\\), \\(N\\) is the
number of entities in the KB, \\(K\\) is the number of relations, \\(\mathbf{R}\\) is a \\(r \times
r \times K\\) tensor, with an \\(r \times r\\) matrix for each of the \\(K\\) relations, and
\\(A\\) is a \\(N \times r\\) matrix with a vector of length \\(r\\) representing each entity.
Basically, this models each entity with a vector, and each relation with a matrix, and computes
the probability of an entity pair belonging to a relation by multiplying the relation matrix on
either side with the entity vectors.

The ARE model augments RESCAL with another tensor \\(\mathbf{M}\\):

\\(\mathbf{X} \approx \mathbf{R} \times\_1 A \times\_2 A + \mathbf{M} \times\_3 W\\)

\\(mathbf{M}\\) is an \\(N \times N \times P\\) tensor, with \\(P\\) features per entity pair,
extracted however you wish from the original tensor (these could be PRA or horn clause features,
for instance).  \\(W\\) is a \\(K \times P\\) matrix with weights saying how predictive each
feature is for each relation.  With the addition of the \\(\mathbf{M} \times\_3 W\\) term, the
RESCAL factorization model now only has to account for the things that the observable features
cannot model.

The result is that the model is more expressive, and it gives good performance with a lower rank
than RESCAL, which means there are many fewer parameters to learn, as well (along with faster
runtimes).  They show some nice improves on a few datasets, though none of them are what I would
consider large, and they didn't try using much in the way of PRA features for \\(\mathbf{M}\\).

This paper, both their proof and the method they introduce, made me rethink the utility of trying
to do a PRA composition operator in a latent space, as I was planning on doing.  I'll still run
the experiment (and thus give some more details on this later), but I'm not very hopeful anymore
that it will work well, and I don't think it's worth trying to do a joint model between PRA and
factorization in the way I was thinking, because I think this model is better than what I was
planning.
