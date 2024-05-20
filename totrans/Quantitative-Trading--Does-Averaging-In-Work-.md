<!--yml
category: 未分类
date: 2024-05-12 19:04:44
-->

# Quantitative Trading: Does Averaging-In Work?

> 来源：[http://epchan.blogspot.com/2010/01/does-averaging-in-work.html#0001-01-01](http://epchan.blogspot.com/2010/01/does-averaging-in-work.html#0001-01-01)

Ron Schoenberg and Al Corwin recently did some interesting

[research](http://www.optionbots.com/DOE/does_averaging_in_work.pdf)

on the trading technique of "averaging-in". For e.g.:  Let's say you have $4 to invest. If a future's price recently drops to $2, though you expect it to eventually revert to $3\. Should you

A) buy 1 contract at $2, and wait for the price to

*possibly*

drop to $1 and then buy 2 more contracts (

*i.e.*

averaging-in); or

B) buy 2 contracts at $2 each;  or

C) wait to

*possibly*

buy 4 contracts at $1 each?

Let's assume that the probability of the price dropping to $1 once you have reached $2 is

*p*

. It is easy to see that the average profits of the 3 options are the following:

A)

*p*

*(1*$1+2*$2) + (1-

*p*

)*(1*$1)=1+4

*p*

;

B) 2; and

C)

*p*

4*$2=8

*p*

.

Profit A is lower than C when

*p*

> 1/4, and profit A is lower than profit C when

*p*

> 1/4\. Hence, whatever

*p*

is,  either option B or C is more profitable than averaging in, and thus averaging-in can never be optimal.

From a backtest point of view, the Schoenberg-Corwin argument is impeccable, since we know what

*p*

is for the historical period. You might argue, however, that financial markets is not quite stationary, and in my example, if the historical value of

*p*

was less than 1/4, it is quite possible that the future value can be more than 1/4\. This is why I never make too much effort to optimize parameters in general, and I can sympathize with traders who insist on averaging-in even in the face of this solid piece of research!