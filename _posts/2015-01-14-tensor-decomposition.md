---
published: true
title: "Tensor Decompositions and Applications; Kolda and Bader, SIREV 2009"
layout: post
author: Matt
tags:
- Tensors
---

[Link to paper](http://www.sandia.gov/~tgkolda/pubs/pubfiles/TensorReview.pdf).

I have been working on knowledge base inference recently, and a lot of recent methods for KB
inference are centered on viewing the KB as a tensor and running a decomposition algorithm on the
tensor, to find a low-dimensional representation of it that can be used to infer missing elements.
In reading some of these papers I decided I needed more background on tensor math in general and
tensor decomposition in particular, and this paper was a good overview (assuming you're already
familiar with matrix math and matrix factorization methods like PCA and SVD).

After some helpful overview of notation for tensor math (and some theoretical issues dealing with
determining the rank of a tensor, which I didn't pay too much attention to), the bulk of the paper
is spent describing the two dominant algorithms for performing tensor factorization: CP and Tucker.

The CP decomposition (also called CANDECOMP, PARAFAC, and a few other things) is essentially an
extension of SVD into tensors.  Though it's not generally formulated this way, SVD decomposes a
matrix into a weighted sum of rank-one matrices (rank-one here meaning that the matrix is the outer
product of two vectors).  The SVD decomposition of a matrix \\(X\\) is given as \\(X = U \Sigma
V^T\\), where \\(U\\) holds the left singular vectors, \\(V\\) holds the right singular vectors,
and \\(\Sigma\\) is a diagonal matrix containing the singular values.  We could rewrite the matrix
product as a sum that makes explicit the fact that this is a weighted combination of rank-one
matrices: \\(X = \sum\_i \sigma\_i \mathbf{u}\_i \cdot \mathbf{v}\_i\\), where \\(\sigma\_i\\) is
the \\(i^\mathrm{th}\\) singular value, and \\(\mathbf{u}\_i\\) and \\(\mathbf{v}\_i\\) are the
\\(i^\mathrm{th}\\) columns of \\(U\\) and \\(V\\).  The CP decomposition simply extends this to
higher-order tensors, so that you decompose a tensor into a sum of rank-one tensors (and here an
order-\\(n\\) tensor is "rank one" if it is the outer product of \\(n\\) vectors).  It turns out
there is an alternating least squares algorithm to find this decomposition, which iteratively
solves for each mode of the tensor (in terms of SVD, this would be finding \\(U\\) given a fixed
\\(V\\), then finding \\(V\\) given a fixed \\(U\\), and so on).

The Tucker algorithm is similar, but instead of a diagonal inner tensor (the \\(\Sigma\\) in SVD),
Tucker allows an arbitrary tensor.  This is obviously a more expressive decomposition, but it is
also more difficult to compute.  The Tucker decomposition is called the higher-order analogue of
PCA, though the connection between Tucker and PCA is less clear to me than the connection between
CP and SVD.  Perhaps it's because the inner tensor in the Tucker deomposition can be viewed as a
compression of the original tensor, much like PCA is a kind of compression of an original data
matrix (and there might even be a stronger formal connection there, but if there is, I don't
remember seeing it discussed in this paper).
