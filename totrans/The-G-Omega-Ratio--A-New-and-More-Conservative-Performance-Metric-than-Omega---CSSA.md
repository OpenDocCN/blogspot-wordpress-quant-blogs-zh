<!--yml
category: 未分类
date: 2024-05-12 18:06:25
-->

# The G-Omega Ratio: A New and More Conservative Performance Metric than Omega | CSSA

> 来源：[https://cssanalytics.wordpress.com/2012/03/19/the-g-omega-ratio-a-new-and-more-conservative-performance-metric-than-omega/#0001-01-01](https://cssanalytics.wordpress.com/2012/03/19/the-g-omega-ratio-a-new-and-more-conservative-performance-metric-than-omega/#0001-01-01)

The Omega ratio [http://en.wikipedia.org/wiki/Omega_ratio](http://en.wikipedia.org/wiki/Omega_ratio) is a relatively new performance metric  invented by Keating and Shadwick. It was designed to be a better way to capture all moments of the distribution to give a fair accounting of the upside versus the downside risk that is superior to the Sharpe Ratio. From a semantic perspective it does truly capture the notion of “reward versus risk” in terms that most investors are familiar with. The Omega uses a threshold or some level of required return to calculate the upside above the threshold versus the downside below the threshold. My own testing shows that the Omega is in fact competitive or superior to the Sharpe ratio in many applications. It is often better for use in ranking assets, strategies or portfolio managers- especially those that have non-normal distributions. Winton Capital provides an interesting white paper on the topic [http://www.performance-measurement.org/Winton2003.pdf](http://www.performance-measurement.org/Winton2003.pdf) of using the Omega for performance evaluation.

The calculation of the Omega statistic is actually quite simple–don’t let the fancy notation deter you.  The calcuation boils down to a few simple steps:

1) identify a threshold, T– lets say it is zero for this example

2) calculate the excess returns > T, or take the sum of the returns >0 in this example minus the threshold (subtract zero for all returns above zero and take the sum)

3) calculate the excess returns< T, or take the sum of the returns <0 in this example minus the threshold (subtract zero for all returns below zero and take the sum)

4) take the sum in step 2 divided by -1* the sum in step 3……….this is the Omega Ratio

The conventional Omega Ratio suffers from a few minor flaws. First, it is skewed by outliers because it simply takes the ratio of the sum above versus the sum below the threshold. Any extreme observations will lead to an Omega Ratio that does not correctly capture the true nature of the distribution. Second, the use of a sum measurement fails to account for the true ratio of upside versus downside return potential in the absence of a difference in frequency between the two. That is, assuming that the frequency of returns above the threshold versus below were to change dramatically, what would be the effective upside versus downside. Third, the Omega does not account for the impact of compounding returns–it simply takes the sum of returns versus the threshold. This does not address the fact that compounding requires a low variance around returns to comparably match the sum or arithmetic mean of returns.

The “G-Omega” is a simple modification to the above ratio that addresses these concerns. The simple difference is that the G-Omega uses the geometric average of returns above the threshold versus the geometric average of returns below the threshold instead of the sum subject to a maximum value of 10 and a minimum value of 0\. This ratio is purely focused on the evolution of upside compounding potential versus downside compounding potential. The G-Omega is indifferent to the frequency of returns above the threshold versus the frequency below the threshold. It is also less sensitive to outliers since it is taking the average of several values. The G-Omega can potentially have a value of less than 1 even when there are mainly positive observations versus negative observations. This is because the average returns below the threshold can exceed the average returns above the threshold when tail risk is high. From this perspective, the G-Omega can provide a very conservative view of an asset, strategy or portfolio. It is potentially a nice complement to the original Omega metric.