<!--yml
category: 未分类
date: 2024-05-18 15:37:34
-->

# Variance Estimators Revisited | Tr8dr

> 来源：[https://tr8dr.wordpress.com/2009/11/17/variance-estimators-revisited/#0001-01-01](https://tr8dr.wordpress.com/2009/11/17/variance-estimators-revisited/#0001-01-01)

I need to have a reasonably accurate measure of intra-day variance for a strategy I am working on.    In a previous post I indicated that while GARCH(1,1) fits daily returns well, it fits intra-day returns poorly.   In fact so poorly, that it was not possible to arrive at a non-zero maximum likelihood.

The failure of the GARCH model for intra-day is multifold.   Intraday (squared) returns exhibit:

1.  random large jumps followed by sharp drop-off
2.  microstructure noise
3.  apparent gaps in return as a smooth AR process

**Garch Revisited** I decided to take another look at GARCH;  Perhaps with some modification could make it useful as a rough measure, short of a more sophisticated model.

The “jumps” present in intra-day data have a near 0 probability in a gaussian error model.   To combat this, added a component to the GARCH model to absorb jump shocks:

[![](img/45a2f36c70d923b4a3093c803feecb32.png "Picture 1")](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-17.png)

The added component is **J**, which absorbs the excess return above a threshold.   The above basically says that the jump has no predictive value for subsequent measures of the squared return (though this is not strictly what is observed).   More likely, the jumps should be considered as a largely independent random process contributing to overall variance.

The threshold was determined heuristically as:

[![](img/d76c1ed5b11b43727513cc0c8abd676a.png "Picture 1")](../files/2009/11/picture-18.png)

With the above formulation was able to calibrate to a relatively high likelihood and R^2 of around 0.90 in sample and 0.85 out of sample, that is with truncated jumps.

[![](img/b5f887c70a0c65ce88ff80c31cec9ff3.png "Picture 9")](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-92.png)

**Duration Based Approach**
For a Brownian motion based process, we know that increments Δ**r** over time interval Δ**t** scale as follows, and that one implies the other:

[![](img/3f2fac43c125bdab2c41b82ab32cd252.png "Picture 3")](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-37.png)

Basically implying that we can estimate the amount of time it will take for Δ**r** to be realized in the price (returns) process.   Engel and Russell developed a well regarded model for price duration, called the Autoregressive Conditional Duration model (ACD).   The model expresses price movements in terms of duration (or alternatively intensity), though does not explicitly provide a variance estimate.

For the purposes of this model, let us assume a granularity constant Δ**r**.  We then let **D**[t] denote the effective span of time took for the process to move by Δ**r** between [t, t-1].  This is calculated as Δ**r** divided by the change in return (approximately).   For example if Δ**r** is the return represented by 1 pip, and a 3 pip return is seen over a period of 1 second, D[t] would be 1/3rd.

In terms of intensity we can model this as:

[![](img/3b83952b7a42edbbc9705f7533528029.png "Picture 4")](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-43.png)

We would like to get variance into a form were it can estimated in terms of intensity.   Given that variance is expressed as the expectation on square of returns, we can formulate this probabilistically:

[![](img/030d71ade5f2bee5c7290ed458520dc8.png "Picture 7")](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-72.png)

We can use the Poisson pdf to model p(k jumps | λ), and evaluate the discrete integral up to some maximum jump size m.

**Handling Jumps**
Empirically, it would seem that jumps follow a different process from non-jump price movements.   To address this I’ve added a separate process for jumps, with a single factor guiding exponential decay.   The two processes are combined when the expectation is calculated:

[![](img/22e0875f089461a3ba79241260aaf394.png "Picture 8")](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-82.png)

The messy bit is deciding, given a return, whether to consider a jump **J** or a standard return **D** (both as a durations).   We can decide that:

D = max (*price duration for [t-1,t]*, *jump threshold*)
J = max (*price duration for [t-1,t] – D, 0*)

or decide to categorize the whole return as a jump or normal return.

**Seasonality**
We might also want to adjust the constant **Dμ** to adjust to different levels depending on the prevalent level for a given period of the trading day.   Durations will be short (variance high) at the opens and closes for instance.   This would require building a seasonality curve for the trading day.

In the FX markets, different trading sessions offer varying degrees of liquidity.   With reduced liquidity we can see periods with very little price action and large (often temporary) jumps in price.  The autocorrelation of intensities is likely to differ in these sessions, not to mention the base intensity.   A markov switching model  may be the way to go to specialize for the different market conditions.

**Results**
I am now implementing this.   Will see how it compares to the modified GARCH process.   May also look at some variants for the jump process.