<!--yml
category: 未分类
date: 2024-05-18 15:29:05
-->

# T-SNE | Tr8dr

> 来源：[https://tr8dr.wordpress.com/2014/12/13/t-sne/#0001-01-01](https://tr8dr.wordpress.com/2014/12/13/t-sne/#0001-01-01)

December 13, 2014 · 10:27 am

The T-SNE approach is a very intuitive approach to dimensional reduction and visualization of high dimensional features.  I Implemented this in F# recently and had used some implementations in R and python previously.  I have found this very useful in determining whether I have designed a feature set correctly, such that has a natural degree of separation with respect to labels.

The algorithm is elegant: determine the pairwise probabilities of points being neighbors in high dimensional space, find a distribution in  2-dimensional space that, to the extent possible, reflects the same distances (probabilities). with a bias towards preserving locality.   This is solved as an iterative gradient descent on the pairwise relationship across n points.

The problem is that it is an O(n^2) problem, equivalently solving the n-body problem.   My data sets are in the 100s of thousands or millions, so you can imagine, this is no longer feasible on a single processor.

Barnes-Hut is an approximation approach for n-body problems bringing the complexity to O(n log n), but can only be effective if ones partitioning of space is coarse.  For some of my problems, have found that cannot get appropriate separation with this sort of approximation.

In terms of parallelizing, n-body problems require fine-grained parallelism to solve efficiently.   Given that fine-grained parallelism is limited in scale (how many processors can you have on 1 machine or GPU), have been considering whether there is an iterative hierarchical approach that could be applied with distributed parallelism.  I would not expect that such an approach could get anywhere close to linear speedup, but perhaps can do better than a limited # of local nodes.

Another approach to this problem, which is easily distributed would be a meta-heuristic approach such as differential evolution.