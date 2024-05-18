<!--yml
category: 未分类
date: 2024-05-18 13:55:08
-->

# CDOs & Computational Intractability | Quantivity

> 来源：[https://quantivity.wordpress.com/2009/12/29/cdos-and-computational-intractabilit/#0001-01-01](https://quantivity.wordpress.com/2009/12/29/cdos-and-computational-intractabilit/#0001-01-01)

Readers with backgrounds in derivatives and theoretical computer science may find amusement in the recent working paper from Arora *et al.*: [Computational Complexity and Information Asymmetry in Financial Products](http://www.cs.princeton.edu/~rongge/derivative.pdf).

The article provides delightful juxtaposition of cross-discipline buzzword bingo: computational complexity (theoretical [computer science](http://en.wikipedia.org/wiki/Computer_science)), asymmetric information / lemon costs ([information economics](http://en.wikipedia.org/wiki/Information_economics)), and densest subgraph problem ([graph theory](http://en.wikipedia.org/wiki/Graph_theory)).

In short, the authors posit that *detecting fraudulent CDOs/CDSs is essentially computationally intractable* (p. 12). Needless to say, [the press](http://blogs.reuters.com/felix-salmon/2009/12/28/its-impossible-to-price-a-cdo/) is already having a field day with the article to blame [Goldman](http://www.goldmansachs.com/) (arguably rightfully so, to the demise of their counterparties); despite what I wonder may be limited capacity to fully comprehend the subtle theoretical details of the article.

A few more choice words from the authors (p. 3):

> What is surprising is that a computationally limited buyer may not have any way to distinguish such a tampered derivative from untampered derivatives…The paper suggests a surprising answer: in many models, even the problem of detecting the tampering *ex post* may be intractable.

The article is a pleasing practical application of computational complexity theory, which Arora and Barak cover nicely in their recent text, [Computational Complexity: A Modern Approach](http://www.cs.princeton.edu/theory/complexity/).