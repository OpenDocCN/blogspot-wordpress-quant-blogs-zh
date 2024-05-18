<!--yml
category: 未分类
date: 2024-05-18 13:51:54
-->

# Manifold Learning | Quantivity

> 来源：[https://quantivity.wordpress.com/2011/05/08/manifold-learning-differential-geometry-machine-learning/#0001-01-01](https://quantivity.wordpress.com/2011/05/08/manifold-learning-differential-geometry-machine-learning/#0001-01-01)

One of the perennial quant guessing games is speculating on [RenTech](https://www.renfund.com/vm/index.vm) (*e.g.* see amusing *5-year* [NP thread](http://www.nuclearphynance.com/Show%20Post.aspx?PostIDKey=4851&PageIndex=12)), particularly given the fascinating background of [Jim Simons](http://en.wikipedia.org/wiki/James_Harris_Simons) (see his [arXiv](http://arxiv.org/find/math/1/au:+Simons_J/0/1/0/all/0/1) for recent work on differential cohomology). Ignoring public commentary, whose veracity is obviously questionable, careful consideration of historical hiring trends and corresponding employee backgrounds are suggestive. While such speculation is amusing, potential relevance arises in *assisting in filtering the exploration of research*.

Specifically, several themes are consistent:

*   Infrastructure / execution: computer scientists speaks to the mundane realities of large-scale offline and online data management, risk management, multi-venue execution, and the usual collection of optimal execution concerns (particularly relevant for liquidity providing and statarb)
*   Applied mathematics: “natural scientists”, with an emphasis on modern physics (much of which is built upon [differential geometry](http://en.wikipedia.org/wiki/Differential_geometry) and [statistical mechanics](http://en.wikipedia.org/wiki/Statistical_mechanics)), seems reasonable given heavy mathematical and statistical modeling
*   High dimensionality: analysis and signal generation from high-dimensional spaces, which seems reasonable given many trading problems can elegantly be formulated in such a context; plus a deep well exists of both pure and applied math built by academia over the past 20 years; further, this makes obvious sense given Jim’s academic background (*e.g.* see [Chern-Simons](http://en.wikipedia.org/wiki/Chern%E2%80%93Simons_theory))
*   Mixing models: RenTech grew through a combination of small acquisitions and internal development, suggesting “the predictive model” (historically referred to as “Basic System”) is not one but rather a collection of heterogeneous models which are dynamically overlaid and mixed; seems reasonable, given [market regimes](https://quantivity.wordpress.com/2010/02/15/trading-the-unobservable/) and consistent Medallion performance over the past 20 years
*   [Computational linguistics](http://en.wikipedia.org/wiki/Computational_linguistics) / [NLP](http://en.wikipedia.org/wiki/Natural_language_processing): numerous high-profile folks originated from speech recognition, of which numerous advancements over the past 30 years are based upon applied [signal processing](http://en.wikipedia.org/wiki/Signal_processing) and [statistical information theory](http://en.wikipedia.org/wiki/Information_theory) (*e.g.* [Mathematics of Statistical Machine Translation](http://acl.ldc.upenn.edu/J/J93/J93-2003.pdf), by Brown, Pietra, and Mercer); a particularly consistent theme is [HMM](http://en.wikipedia.org/wiki/Hidden_Markov_model) (going back to the [Dragon system](ieeexplore.ieee.org/iel6/29/26109/01162650.pdf?arnumber=1162650) by Baker in 1975), which naturally support mixing via [HHMM](http://en.wikipedia.org/wiki/Hierarchical_hidden_Markov_model), and [causal filtering](http://en.wikipedia.org/wiki/Causal_filter) (see also [Berlekamp](http://math.berkeley.edu/~berlek/bus.html), who worked with [Kelly](http://en.wikipedia.org/wiki/John_Larry_Kelly,_Jr.))

Given this context, let’s return to the point: [Partha Niyogi](http://people.cs.uchicago.edu/~niyogi/) has presented numerous times over the past few years (prior to his untimely death) on the topic of *manifold learning*. For example, he presented [A Geometric Perspective on Learning Theory and Algorithms](http://sms.cam.ac.uk/media/545) at the [AMS/MAA/SIAM joint meeting](http://jointmathematicsmeetings.org/meetings/national/jmm/2124_intro.html) (with collaborator [Mikhail Belkin](http://www.cse.ohio-state.edu/~mbelkin/)).

Manifold learning is particularly interesting as it lies at the intersection of many of the above themes. Specifically, the presentation theme is: *“Geometrically motivated approach to learning: nonlinear, nonparametric, high dimensions”*. This should ring bells.

The abstract tells more:

> Increasingly, we face machine learning problems in very high dimensional spaces. We proceed with the intuition that although natural data lives in very high dimensions, they have relatively few degrees of freedom. One way to formalize this intuition is to model the data as lying on or near a low dimensional manifold embedded in the high dimensional space. This point of view leads to a new class of algorithms that are “manifold motivated” and a new set of theoretical questions that surround their analysis. A central construction in these algorithms is a graph or simplicial complex that is data-derived and we will relate the geometry of these to the geometry of the underlying manifold. Applications to embedding, clustering, classification, and semi-supervised learning will be considered.

In other words, *formulating machine learning within the context of differential geometry*. One of the most common applications is [non-linear dimensional reduction](http://en.wikipedia.org/wiki/Nonlinear_dimensionality_reduction). This is relevant to quantitative modeling for obvious reasons.

For readers wanting to brave the mathematics, consider the following:

Depending upon reader interest, subsequent post(s) may explore this topic further.