<!--yml
category: 未分类
date: 2024-05-18 15:29:14
-->

# Money Management | Tr8dr

> 来源：[https://tr8dr.wordpress.com/2012/09/29/money-management/#0001-01-01](https://tr8dr.wordpress.com/2012/09/29/money-management/#0001-01-01)

It has been almost a year since my last post.  I have been far too busy getting a new trading desk up and running.   I  thought to discuss money management, since am revisiting right now.

## Overview

It is easy to think that trading signal is the most important aspect of a trading strategy, but money management (and execution) can be even more important.   Loosely defined, money management is a mechanism for position-level risk management.  The mechanism attempts to regulate, accomplishing a number of things:

1.  ride out a profitable signal as long as there is continued profit potential
    1.  close out a profitable position when the p&l is drifting sideways
    2.  close out a profitable position, alternatively when there is a drawdown
    3.  otherwise, allow the position to continue to profit, even through transient negative noise
2.  close out our losing positions as quickly as possible
    1.  close position once we have a view that it is unlikely to be profitable
3.  close out strategy if seems unstable
    1.  for example keeps hitting stop-loss
    2.  risk measures indicative of unstable market situation for strategy

A desirable feature of a money manager is that when pairing the money manager and signal together, we have a return distribution with positive skew and very limited negative tails.   We can even have a signal with < 50% wins, but because of the generated bias in + returns / – returns, have an overall positive equity curve.   Of course I would advocate for much a much higher win ratio than 50% 😉

## Signal → Position

I take the approach of having a trading signal that scales between [-1,1] or [0,1] on a continuous basis.   In my trading systems the money manager not only works as a risk manager, but also decides how to scale the signal into a desired position.

For example, if our maximum position is $5 million, we might scale our desired position from 0 to $5 million (if the signal reaches full power at 1).  The 0 or close to 0 level would indicate being out of market, 0.5 being at 1/2 strength or 2.5 million in.   Here is an example signal from 0 to 1:

Trading signals can be noisy, though we do our best to provide smooth signals.   Without regulation of how we map the signal to position size, the up and down dips in the signal would imply thrashing in and out of position, which would be costly.

Hence, we should try to enforce direction monotonicity, so as to avoid thrashing.

## Types of stop-loss

There are a number of stop-loss types we should consider:

1.  stop-loss:
    1.  stop when (smoothed) equity curve has reached a negative return threshold
2.  stop-profit:
    1.  exit an up-to-current profitable trade, but one that has lost some % from the high
3.  stop-drift
    1.  a time and slope based stop that closes out a position whose equity curve is drifting more-or-less sideways for a significant period

## Risk Reentry Avoidance

On a stop-loss not only want to close the position, but also have to “back away” from the signal, such that we do not immediately get back into an undesirable situation.   Depending on why we exited the position, we may want to:

1.  disable market entry until the signal has gone to zero
2.  impose a time penalty
3.  impose a market reentry restriction (wait for the market regime to reach a certain stage)

## A FSM

Here is a finite state machine that illustrates a possible state system guiding position scaling and money management:

[![](img/bc4f3fa4e34c116d4b6d8eaf254dbed5.png "Money Management FSM")](https://tr8dr.wordpress.com/wp-content/uploads/2012/09/screen-shot-2012-09-29-at-4-49-18-pm.png)

The state system expresses some of the above money management features.   To make it effective, one needs to be clever about deciding on whether a negative movement is a sign to get out or a transient movement.   One can use a combination of signal, smoothed series, and aspects of order book and trade data to have a better read on this.