<!--yml
category: 未分类
date: 2024-05-18 15:38:46
-->

# The “Mean” in the context of a mean-reverting process | Tr8dr

> 来源：[https://tr8dr.wordpress.com/2009/11/03/the-mean-in-the-context-of-a-mean-reverting-process/#0001-01-01](https://tr8dr.wordpress.com/2009/11/03/the-mean-in-the-context-of-a-mean-reverting-process/#0001-01-01)

We know that price processes exhibit mean reversion on multiple timescales.   Supposing one wants to measure the distance between the price X[t] and the mean E[X[t]].   The mean of a price process is particularly difficult to model as the process is non-stationary.    The standard approach in options modeling has been to model in terms of a near-stationary process such as log returns .

I am interested in the empirical price distance to the mean.   One could look at the sum of log returns as a proxy to price, but empirical returns are very noisy and the mean-reversion aspect would be lost.    This works out in a continuous model, but wold require some smoothing to make sense in an empirical model.

**The “Mean”**
Focusing again on the mean, in a non-stationary process, we can take different views on the mean depending on the timescale of mean reversion we are interested in focusing on.   Here is an example of different means through a price series (taken ex-post as a penalized least squares regression):

![](img/3f17d26d400bcdfb179b10d54d94b0b3.png)

![Picture 1](img/33200a0b44635757846c3b6b66014d18.png "Picture 1")

The mean for a random variable is defined as the expectation of the variable E[X].  That’s fine, except that E[x] is model dependent and also dependent on our desired mean-reversion timescale.  In the example above all of the regression lines represent reasonable values for the mean and are optimal in a least squares sense, so which “mean” do we choose and what process generates it?

**Modeling Issues**
Ultimately would like to come up with an empirical, discrete, state system that allows me to estimate the mean as a hidden state from a maximum likelihood point of view.   Just as with “volatility”, the mean is not truely observable.  The model needs express the following:

1.  represent mean reversion timescale of interest
2.  deal with jumps / regime change in the mean
3.  mean is a function of time
4.  variance is a function of time

**Models**
A common place to start with mean-reversion models is the *Ornstein-Uhlenbeck process*:

![Picture 11](img/da56ebee70966c930b7e40d82609f3ab.png "Picture 11")

Note that this is expressed in terms of a long-run mean (constant) μ, a mean-reversion coefficient (constant) κ, and standard deviation (constant) σ.  Also note that this is a process modeling the change in price (usually log change).

The *Hull-White model* went a step further to allow the mean and standard deviation to be a function of time.   Finally the *extended Vasicek model* allows for the mean-reversion constant to vary with time:

![Picture 5](img/85b070c0cc4751f9b97f94c99002c3db.png "Picture 5")

Ok, a few problems.   We have not addressed the jump aspect of price movement and also need to convert this into a discrete empirical process.   One way of introducing a jump component is modifying the above formulation to include a jump process dQ (note that I have adjusted the mean-reversion process to be a constant to allow us to solve for μ(t) later:

![Picture 7](img/17489a8fd671fded670db6315bc35eb2.png "Picture 7")

This is not the most sophisticated model, however, for the purposes of modeling the mean should prove useful.

**Discrete form** Let’s ignore the jump component for the moment, and arrive at a discrete formulation for the Gaussian component in the mixture.   A general gaussian markov process has the form:

![Picture 1](img/fa4a990ad02244e48c642e90f3d365b7.png "Picture 1")

we get the following solution:

![Picture 2](img/b5cd4359ad4d0686383a127872b3b260.png "Picture 2")

For our equation this works out to:

![Picture 3](img/ac786c2681ca8db657a63164b32657eb.png "Picture 3")

or between times t-Δt and t:

![Picture 4](img/be1c78bf4b395d3424938e71a2d806a4.png "Picture 4")

We now have enough to formulate a state system.   We will assume the change in volatility or mean over Δt to be small enough so that can assume volatility and mean are constant over the integral for Δt.

First we need to decide on a process to express variance.   For daily returns we can use GARCH(1,1), and for intraday will need an alternate model:

![Picture 7](img/206d06c3a48648caef946ff80dbe92f3.png "Picture 7")

Within the context of a discrete increment Δt within our mean reverting SDE, the volatility scales as:

![Picture 8](img/320300c6c550324a2ee6479812947c2f.png "Picture 8")

We express the mean as an AR(2) process, but within the larger state system so that it accepts “innovations” from the mean reversion process (via recursive feedback):

![Picture 9](img/b8c4aab91b2289bee7bf00cb8fdb22f0.png "Picture 9")

We can easily express this state system in a particle filter to find the ML parameters (assuming constant κ).

**Handling Jumps** Given that we are not using this SDE in a predictive fashion, we can introduce jumps as a point process or alternatively as a cumulator variable as we observe jumps in the market.   So for instance, could reexpress the mean process as:

![Picture 10](img/d85c2f4363cff999ce82dc8bc325cf00.png "Picture 10")

**Conclusion**
Our goal here was to determine an accurate measure of the mean, one that we can consider optimal from a model / maximum likelihood point of view.   I now need to implement this state system in a particle filter and determine how effective it is.   Some enhancements may be required.    This is a work in progress, look for further updates …