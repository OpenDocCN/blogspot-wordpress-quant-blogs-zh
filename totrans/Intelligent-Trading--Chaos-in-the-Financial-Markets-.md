<!--yml
category: 未分类
date: 2024-05-18 04:45:16
-->

# Intelligent Trading: Chaos in the Financial Markets?

> 来源：[http://intelligenttradingtech.blogspot.com/2010/07/chaos-in-financial-markets.html#0001-01-01](http://intelligenttradingtech.blogspot.com/2010/07/chaos-in-financial-markets.html#0001-01-01)

Over the years I've had quite a few interested individuals ask me about Chaos and its applications towards trading. Well, as hidden markov models and speech processing were made popular by James Simons and his team at Renaissance Technologies, one could trace much of the popularity of Chaos theory and its financial applications to Norman Packard and Doyne Farmer, two former physicists working in the area of complex systems. Much of their story is discussed in the book, 'the Predictors,' by Thomas Bass. The two were on the forefront of new research in areas of complexity and chaos and had decided to parlay their knowledge into applications towards the financial markets as they founded the company called Prediction Company in Santa Fe, New Mexico. The company was swallowed by UBS systems in 2005.

Fig 1.   2D slice of Lorenz Attractor Phase Space signature A.K.A. The butterfly effect.

We could spend a lot of time discussing various facets of Chaos, as it is a very large field with many different related fields (such as fractals and complexity). But I want to focus on outlining a very simple understanding of why the field seemed so fascinating to traders and quants alike. Most experts in time series run a slew of tests to demonstrate that markets exhibit no predictable order.

However, what makes Chaos so fascinating is that certain time series may seem to pass a battery of common statistical tests for randomness, yet are perfectly deterministic.

Chaos is a field of science that is engaged in studying non-linear dynamical behavior of systems. A popular example might be how different planetary bodies exhibit forces upon one another (see Poincare), or turbulent flow of various particles. Those engaged in studying such systems often like to observe signatures in a domain known as phase space or state space. Rather than look at the time series unfold over time, they are looking for a type of order that underlies the trajectories of the system state dynamics as it unfolds over time. The plot of the trajectory may show structural order that may appear random in the time domain. One of the most popular attractor signatures is the well known Lorenz attractor, which is better known to popular literature as the butterfly effect. Fig 1, displayed earlier, shows a 2d slice of the phase space trajectory, that you can run over at

[chaos applet](http://www.cmp.caltech.edu/%7Emcc/Chaos_Course/Lesson1/Demo8.html)

. The famous signature displays a fascinating case of underlying order that relates to dynamic atmospheric convection in three dimensions.

A more simple and applicable model that we will look at for illustration purposes, is the well known Logistic Map (also known as quadratic map and Fiegenbaum map). This equation of a non-linear dynamical trajectory was investigated and attributed to Robert May, a biologist studying models of fish populations.

The recursive equation for the Logistic Map is: xnext = r*x(1-x)

Note that this is a feedback system which has some control over the dynamics of the system model by varying the value r. What you'll see if you plot it out vs. the control coefficient, r, is that the series moves from a stable system to one which bifurcates into periodic cycles; and as it approaches the value 4 it starts to behave chaotically. Chaotic behavior is aperiodic, which (like financial series) never repeats exactly; but (unlike financial series) has an underlying deterministic order. In order to see the beauty of chaos and how it exhibits determinism, let's first look at the time series.

Fig 2\. Time Series of Logistic Map Equation.

Notice the 1st plot, which shows the 1st differenced time series, shows no signs of periodicity or determinism, nor does the cumulative walk display on the 2nd. However, if we look at the phase space signature of the same series in phase space, we see a completely different picture.

Fig 3\. Phase State Plot of Logistic Map

Notice it is clearly deterministic in this figure. I.e. given any point on the x axis, we can easily determine the exact corresponding point one step into the future on the y axis.  This should be fairly obvious, since the equation we started out with xnext=r*x(1-x) = r*x-r*x^2 is a negative parabolic curve. However, many such time series do not have such a simple equation and must be tested in various ways to determine structural chaos. There are other issues to contend with as well, including sensitivity to initial conditions and divergent trajectories due to finite computational precision.

Ok, now that we understand all the hoopla about Chaos and a seemingly random signal having an underlying deterministic signature, what about a common financial time series?

Fig 4\. Typical Random Walk (Financial) Time Series.

The Random Walk shows no discernible order, nor periodicity; similar to the logistic equation series. But what about if we observe the phase space trajectory?

Fig 5\. Phase Space trajectory of random walk.

No Dice. Notice that the random walk shows zero determinism, hence the gaussian nature.  There are numerous methods to display higher order dimensional metrics as well (correlation lag plots, Lyapunav exponents, etc), and other than something called the compass rose, I've not personally seen much evidence of deterministic chaos in raw financial time series. Incidentally, the phase plot here is equivalent to a lag one scatterplot of returns for those more familiar with finance related statistics.

A last note on the Prediction Company, is that there is an often referenced paper on the mackey-glass equation

(a non linear dynamic model of blood flow) by Meyer and Packard, whereby they used genetic algorithms to find underlying conditional order rule sets for the series. 

I'll end with perhaps the best excerpt from 'the Predictors,' which echoes much of my own focus and discoveries over the last decade...

"One of the fundamental truths about the markets is that the dynamics are nonstationary," Norman explains. "We see no evidence for the existence of an attractor with stable statistical properties. This is what characterizes chaos -- having an attractor with stable statistical properties-- so what we are seeing is not chaos. It is something else. Call it an 'even-stranger-than-strange attractor,' which may not really be an attractor at all.

The market might enter an epoch where some structure coalesces and sits there in a statistically stationary pattern, but then invariably it disappears. You have clouds of structure that coalesce and evaporate, coalesce and evaporate. Prediction Company's job is to find those pieces of structure that have the strongest signal and persist the longest. We want to know when the structure is beginning to emerge or dissolve because, once it begins to dissolve, we want to stop betting on it."

...excerpt from the Predictors, Thomas A. Bass (1999).