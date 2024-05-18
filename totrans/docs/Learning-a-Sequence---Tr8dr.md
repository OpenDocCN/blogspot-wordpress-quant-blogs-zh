<!--yml
category: 未分类
date: 2024-05-18 15:36:12
-->

# Learning a Sequence | Tr8dr

> 来源：[https://tr8dr.wordpress.com/2009/12/04/pattern-learning/#0001-01-01](https://tr8dr.wordpress.com/2009/12/04/pattern-learning/#0001-01-01)

I had been looking at predicting durations (or the intensity) to model price behavior and variance estimation.    As mentioned previously, the prevalent ACD models in the literature do poorly.   Before moving on to another topic wanted to revisit this, with an idea for future approach.

Here is a sample of durations for a high-frequency price series:

```
9.30, 0.26, 0.28, 4.21, 0.04, 0.21, 3.23, 0.04, 2.28, ...

```

I decided that rather than trying to regress for specific durations, where there are an infinite number of possible values (theoretically), transform this into a set of symbols so that there are a finite number of states say:

```
S1, S2, S3, ...
```

where S1 might represent durations in [0, 0.25], S8 durations in [3, 3.5], etc.   The sequence of states for the above durations might look like:

```
12 → 1 → 1 → 9 → 1 → 1 → 8 → 1 → 7 → 6 → 6 → 6 ...

```

This turned out to be useful.

**SVM** SVM on a radial basis kernel did a much better job of predicting the next symbol (duration) in a sequence than the ACD models.   It was still not  a suitable level of prediction however.

The problem with SVM and related approaches in general is that you either need to have a problem that can easily be categorized in high dimensional linear vector space.  A big part of this is finding the kernel that will map your (usually) non-linear vectors into a linearly separable space.    Also, SVM is arguably better suited to binary classification as opposed to multinary classification.

**ANNs** In theory, an ANN with enough neurons can asymptotically approximate any function.  There are many problems in arriving at a general solution though:

1.  **Calibration**
    Standard techniques of backpropagation (essentially gradient descent) solve for a local optimum, which depends on the starting configuration.   A global optimum can be found with meta-heuristic approaches such as GAs, however, at significant computational cost.
2.  **Overfitting**
    It is very difficult to come up with networks that generalize.   Part of the success in doing this involves choosing training sets and configurations carefully.

Nevertheless, this may be an approach worth exploring.

**Probabalistic Graph Models** As our duration pattern is essentially a transition from one state to the next, modeling as a probabalistic finite state machine appeals as model.  The idea with such an approach would be:

1.  empirically observe all chains of length ≤ some maximum
2.  determine the frequency of chains
3.  factorize into the smallest graph that reproduces those chains within some error

The chains, for instance:

[![](img/6ed0abd5fbfd1137d0c1fd0e86d5a365.png "Picture 4")](https://tr8dr.wordpress.com/wp-content/uploads/2009/12/picture-4.png)

A first approach to this problem is to consider whether can be modeled as a markovian state system.  It is, however, doubtful that the states {S1, S2, S3, …} can be modeled in a strictly markovian setting without the use of additional states.

For instance, is  P(S1|S2) the same as P(S1|S2, {prior states})?   The duration data shows dependence beyond the immediate prior state.    Therefore we have to expect that P(S1|S2, {S5,S1}) will differ from P(S1|S2, {S2,S3}), whereas in a markovian model, the probability of S1 can be conditioned purely on the prior state.

Such a markovian system might look like:

[![](img/00cbadb3eab8cde270dcd67753b38e0a.png "markov FSM")](https://tr8dr.wordpress.com/wp-content/uploads/2009/12/markov-fsm.png)

The HMM (Hidden Markov Model) combats this assumption by assuming that there is a hidden markovian process (usually with more states than the observed state system).   One can easily prove that a HMM of infinite size can exactly model all possible state chains (sequences) amongst a finite set of states.   Of course we are interested in a much smaller model that can reproduce most of the observed chains with limited error.

Here is a sample structure, where the black lines are edges between hidden states and the red edges indicate correspondence between hidden state and observed state.   The red edges are not traversed:

[![](img/050ec04f298d365e0a02857dea531f6c.png "HMM")](https://tr8dr.wordpress.com/wp-content/uploads/2009/12/hmm.png)

**Aliasing Issues**
Remember that we have arbitrarily subdivided durations (which are continuous) into N discrete states.   The idea was that the difference between say 0.25 seconds and 0.22 seconds is not important for our purposes.   One would think that less granular states will allow for  easier modeling of the state sequence.

The problem is that we are dividing these discretely.   We run into an **aliasing** problem where a specific duration *partially* belongs to the set represented by S(i) and S(i+1).   For instance for a sequence of length 3 we have 4 possible true state paths, each with associated probability.   Without compensating for aliasing we see the states (naively):

[![](img/943dabee4a3e8b19ca2cd6f8dcdc7b07.png "Picture 6")](https://tr8dr.wordpress.com/wp-content/uploads/2009/12/picture-61.png)

With aliasing we have the following possibilities:

[![](img/1e5807de1c43c8562802070bf18295e6.png "Picture 5")](https://tr8dr.wordpress.com/wp-content/uploads/2009/12/picture-51.png)

As our path length approaches N, we will have 2^(N-1) possible paths.  One possible implementation of this is train with the M highest probability paths.

**Fuzzy HMM** Aliasing is a kind of fuzzy set membership.   Aside from aliasing there are a number of reasons why we should consider fuzzy state membership:

1.  The data may be noisy, obscuring the pattern
2.  Discretisation error (aliasing)

Not surprisingly, other people have thought of fuzzy state membership in the context of HMM.   There are multiple fuzzy HMM models.   To be investigated …