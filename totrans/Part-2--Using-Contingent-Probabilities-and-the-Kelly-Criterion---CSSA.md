<!--yml
category: 未分类
date: 2024-05-12 18:51:28
-->

# Part 2: Using Contingent Probabilities and the Kelly Criterion | CSSA

> 来源：[https://cssanalytics.wordpress.com/2009/08/09/using-contingent-probabilities-and-the-kelly-criterion-part-2/#0001-01-01](https://cssanalytics.wordpress.com/2009/08/09/using-contingent-probabilities-and-the-kelly-criterion-part-2/#0001-01-01)

In Part 1 we discussed the procedure for estimating how much to bet using MDVK with a baseline strategy to identify bull and bear markets.  Now we should look at how to use this information when combined with new information–ie we are trying to calculate how much to bet using  contingent probability data. There are two ways to go about this: 1) ***“back of the envelope”*** – estimation using both historical data, and some adjustments based on human logic 2) ***using advanced statistical forecasts:***  forecasting using  conditional probabilities where the correlation and interaction between independent variables are considered.

We  will focus on “back of the envelope” estimation in this article, as the reality is that most traders are not equipped, or knowledgeable enough to effectively use #2 on a day-to day basis. There is a big difference between the ideal world of numbers and the rough and tumble world of trading*.* I would compare #1 and 2 using the following analogy: you wouldn’t want to send a soldier into war with a new weapon that was complicated or difficult to use without adequate training. Besides, good human judgement combined with basic historical data (properly used) can produce solid results that are more robust than poorly-executed quantitative models.

One of the best sources to generate  useable contingent probability data  is Rob Hanna’s ***Quantifiable Edges*** [http://quantifiableedges.blogspot.com/](http://quantifiableedges.blogspot.com/) . In general, Rob usually presents a specific situation that is directly comparable to the current environment. He then presents historical data for what you would have made or lost by trading under this specific contingency. Suppose our primary trading vehicle is the SPY, here is a practical example:

[http://2.bp.blogspot.com/_931wANibTqw/SnGgh-ybdJI/AAAAAAAABS4/ksKrIMBsfnQ/s1600-h/2009-7-30+png.png](http://2.bp.blogspot.com/_931wANibTqw/SnGgh-ybdJI/AAAAAAAABS4/ksKrIMBsfnQ/s1600-h/2009-7-30+png.png)

Lets assume from the example in Part 1, that we are in a bull market and the VIX is 15\. Our baseline bet should be 47% using the previous calculation based on MDVK.  Lets assume that we are not able to obtain the conditional probability of what the specific results are when we are in a bull or bear market. We have to combine our new information to figure out how much to bet. Let’s further assume that we trade one week at a time, making our decisions and holding for 5 trading days. In this contingency, Rob presents the historical results for trading when ” the SPY closes higher in the last hour of trading  4 days in a row , sell “x” days later.” This is the only data that we need:

|   |   | **all: total** | **all: %** | **All: Win/Loss** |
| **x days** |  | ** trades** | **profitable** | **ratio** |
| 5 |   | 85 | 45.88% | 0.82 |

Now, using the MDVK we can figure out how much to bet in this situation–let’s revisit the calculation. This time I also simplified the Kelly Criterion so that is easier to follow:

***B***= ***T ***x *20/(the current vix level)*

***MDVK***= (B x 1/2 x (100/(1-f)))*max(300%)*

*note that if “f” is <0, than the  formula becomes:    -1*(B x 1/2 x (100/(1-abs(f)))*max(-300%)**

*where **T**= *100% trend bet going long in bull markets/short in bear markets**

*where **B**=  *baseline bet going long in bull markets/short in bear markets**

*where Kelly Criterion= f = W – [(1 – W) / R       and   R= win/loss ratio and W= the % profitable trades*

*B= 20/15 x (100%)= 1.333*

*f= 46%-((1-46%)/.82))= -20%*

*MDVK=-1 x 1.333 x .5 x (100/80)= -83% or “short” 83% of your portfolio*

To calculate the combined “f” in this case we need to utilize the previous baseline estimate of 47% with the current contingency estimate of -83%.  Ideally we would want to know what the conditional probability is, because we do not we can solve our “back of the envelope” problem as follows:

combined(*f*)= ( Baseline *f + (confidence)x contingency (f))/2*

*where confidence=  t-score confidence  OR the  rough adjustment for your own confidence that this probability is reliable given the sample size and the situation. If the sample size is under 20, i recommend at best 50% confidence. Another adjustment includes if you feel that the current situation does not fully match the historical situations. Perhaps the market is abnormal, or there is a seasonal influence to take into account.*

In this case, to keep things simple we will assume 100% confidence:

combined f= (47%+(-83%))/2= -18%

In this case, we would close out our long position and go net short 18% of our portfolio. As you can see, the above methodology is practical because it allows us to quantify how much to bet, and also can incorporate adjustments based on our own judgement of the situation. Often traders struggle with determining how much to bet and whether or not to take profits, or switch positions. Using the MDVK to calculate a combined “f”, gives you a concrete answer as to the current position that you should be taking. While it is not meant to be highly precise, it is far better than a “seat of the pants” decision made under pressure close to the closing bell. It is a highly structured framework to take into account the 1) the current long term trend 2) volatility 3) risk/reward ratios and 4) contingent situations.

I will try to make a spreadsheet available to the readers by the end of the week so that it can be used for real-life trading. In part 3 we will look at using statistics to make more precise conditional forecasts. This is a topic that we will build upon slowly as I introduce various statistical procedures and their applications as well as  pros/cons. On Tuesday we will look at  how to perform  “back of the envelope” robust optimization procedures to figure out how to trade pairs. However this method is applicable to optimizing any trading system without overfitting.