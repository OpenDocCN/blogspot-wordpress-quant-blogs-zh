<!--yml
category: 未分类
date: 2024-05-12 18:52:14
-->

# The DVI: Using the DVS Part 2 | CSSA

> 来源：[https://cssanalytics.wordpress.com/2009/08/02/the-dvi-using-the-dvs-part-2/#0001-01-01](https://cssanalytics.wordpress.com/2009/08/02/the-dvi-using-the-dvs-part-2/#0001-01-01)

Following up from the previous post  on the DVI, i will present some more data on the DVS (the “stretch” indicator) as a moderator of future returns. All data is on the SPY (S&P500 ETF) from 1995-present. First lets take a look separately at accuracy:

|   | **Accuracy (% positive) on next day returns** |   |   |
|   |   |   |   |   |
|   |   | **DVS reading** |   |   |
|   | **below .2** | **below .5** | **above .5** | **above .8** |
| **Up day** | 53.1% | 51.4% | 51.3% | 47.0%** |
| **Down day** |     59.2%@ |      57.3%** | 50.4% | 48.2%* |
| **Baseline** | **52.5%** |   |   |   |
|   |   |   |   |   |
| @ | 85%+ confidence using chi-squared test |   |
|  ** | 75%+ confidence using chi-squared test |   |
|  * | 60%+ confidence using chi-squared test |   |

In this test we are using a chi-squared test to determine if we can be confident that different contingencies result in predictive accuracy that is signficantly different from the baseline (S&P500 buy and hold). In this case, down days (today was a down day) with a DVS below .2 are generally followed by up days almost 60% of the time. This result is highly predictive with a confidence level of 85%. The opposite case, which are up days with a DVS above .8, is generally followed by an up day 47% of the time (53% of days were negative the following day). Again this result is very predictive with a confidence level of 75%. Down days with a DVS less than .5 were followed by up days roughly 57% of the time. Therefore, following down days even when the DVS reading is just below average  it is very predictive of next day returns with a confidence level of 75%. Down days with DVS readings above .8 are followed by an up day 48% of the time (52% are negative days) which is more predictive than chance would expect (60% confidence) but  not  that reliable as an indicator of accuracy. In summary, when the DVS is at extremes, and the short-term direction of the market is in the same direction, it is very predictive of mean reversion. This applies to both sides, whether predicting positive or negative returns. When looking at applying the DVS above and below the mean, there is a long-bias. If one were  to buy on short-term weakness when the DVS is below.5, we can confidently predict that the result will be positive returns the next day. In contrast, this effect is not as uniform on the short side (ie the DVS is above average and there is short term-strength).

Now lets take a look at the magnitude of returns:

|  

&#124;   &#124; **Magnitude (% gain next day)** &#124;   &#124;   &#124;
&#124;   &#124;   &#124;   &#124;   &#124;   &#124;
&#124;   &#124;   &#124; **DVS reading** &#124;   &#124;   &#124;
&#124;   &#124; **below .2** &#124; **below .5** &#124; **above .5** &#124; **above .8** &#124;
&#124; **Up day** &#124; 0.084% &#124; -0.010% &#124; -0.016% &#124; -0.118% &#124;
&#124; **Down day** &#124; 0.245% &#124; 0.139% &#124; -0.024% &#124; -0.016% &#124;
&#124; **Baseline** &#124; **0.029%** &#124;  &#124;  &#124;  &#124;
&#124;   &#124;   &#124;   &#124;   &#124;   &#124;
&#124;   &#124; **Relative Magnitude Expressed as a Multiple of the Baseline Return** &#124;
&#124;   &#124;   &#124;   &#124;   &#124;   &#124;
&#124;   &#124;   &#124; **DVS reading** &#124;   &#124;   &#124;
&#124;   &#124; **below .2** &#124; **below .5** &#124; **above .5** &#124; **above .8** &#124;
&#124; **Up day** &#124; 2.9 &#124; -0.4 &#124; -0.6 &#124; -4.1 &#124;
&#124; **Down day** &#124; 8.5 &#124; 4.8 &#124; -0.9 &#124; -0.6 &#124;
&#124; **Baseline** &#124; 1 &#124;   &#124;   &#124;   &#124;
&#124;   &#124;   &#124;   &#124;   &#124;   &#124;

 |

When we analyze performance in terms of multiples of the baseline (SPY) daily returns we get a clear picture of how strong the DVS is at separating the magnitude of performance. When looking at extremely oversold levels of the DVS  below .2 coupled with today being a down day, next day magnitude was a whopping 8.5 times the daily average return. Even more interesting is that when today was an up days  results are also highly positive when the DVS is below .2, with a next day return 2.9 times the daily average return. Even when the DVS was just below average (below .5), if today was a down day, the next day return was 4.8 times the daily average.  When the DVS was below average and today was an up day, returns were -.4 times the daily average.

Amazingly, when the DVS was above .5, returns were below average and negative in every contingency. This means that the DVS subsumes the signficance of daily follow through when the market is considered overbought. Even when the market was above its 200 day average, or any other major trend indicator, the next day returns were negative if the DVS was above .5\. (We will delve into analyzing the DVS and above and below major trend indicators in the next post. ) Incredibly, returns were -4.1 times below average when today was an up day and the DVS was above .8.

Putting it all together:

On balance, the DVS is a strong moderator of both magnitude and predicted direction, especially at extremes. The long side–when the DVS is oversold (below .5)– produces higher returns and more reliable predictions of market direction. While overbought levels of the DVS produce more mixed results in terms of predicting market direction, and magnitudes were comparatively lower, the direction of magnitude was more consistent than the long side. An investor would probably be better off staying in cash or t-bills when the DVS is overbought , and shorting only when the DVS is extremely overbought  (above .8), and today was an up day.

In the next post we will look at sharpe ratios and R-squared values for each contingency, and also look at how the DVS performs in bull and bear markets using major trend indicators. I will also demonstrate the power of combining the  DVS with the powerful DV2 instead of daily follow through (up or down days) . Finally I will then combine all three together  using quartile analysis to create the “Market Grid.”