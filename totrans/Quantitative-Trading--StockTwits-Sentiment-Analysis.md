<!--yml
category: 未分类
date: 2024-05-12 18:55:59
-->

# Quantitative Trading: StockTwits Sentiment Analysis

> 来源：[http://epchan.blogspot.com/2017/09/stocktwits-sentiment-analysis_7.html#0001-01-01](http://epchan.blogspot.com/2017/09/stocktwits-sentiment-analysis_7.html#0001-01-01)

By Colton Smith

===

Exploring alternative datasets to augment financial trading models is currently the hot trend among the quantitative community. With so much social media data out there, its place in financial models has become a popular research discussion. Surely the stock market’s performance influences the reactions from the public but if the converse is true, that social media sentiment can be used to predict movements in the stock market, then this would be a very valuable dataset for a variety of financial firms and institutions.

When I began this project as a consultant for QTS Capital Management, I did an extensive

[literature review](https://quantoisseur.wordpress.com/2017/01/04/social-media-sentiment-analysis-and-trading-strategies/)

of the social media sentiment providers and academic research. The main approach is to take the social media firehose, filter it down by source credibility, apply natural language processing (NLP), and create a variety of metrics that capture sentiment, volume, dispersion, etc. The best results have come from using Twitter or StockTwits as the source. A feature of StockTwits that distinguishes it from Twitter is that in late 2012 the option to label your tweet as bullish or bearish was added. If these labels accurately capture sentiment and are used frequently enough, then it would be possible to avoid using NLP. Most tweets are not labeled as seen in Figure 1 below, but the percentage is increasing.

| [![](img/7b3d2799311510585b56d546e0526b71.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgp67F1EViuIBhtB_OWf3uNPt2XPud8zZigqjwElnSxShcfvfNd756PpXW3dmCS0rRWGd8tfZTKI5IP5Q1V-YLx2So_2QggYyLdA2vH3lQudFFMFpeGMg_714ESZfeufSFrc2kSMA/s1600/EPCHAN_F1.PNG) |
| Figure 1: Percentage of Labeled StockTwits Tweets by Year |

This blog post will compare the use of just the labeled tweets versus the use of all tweets with NLP. To begin, I did some basic data analysis to better understand the nature of the data. In Figure 2 below, the number of labeled tweets per hour is shown. As expected there are spikes around market open and close.

| [![](img/a091073fe987cacb18391eb08a37ce0d.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgI2SIwt9N0jQeFtCFE0cV1RFWm26UeB74-HFETC2G41x_nH4aEENIkX9ASU9YJblmgyPVFI9QcAMCpcWHyBfvtk9NFbMqKRIryQHL8NhG5Iq4LFlk1ak8eP5x1nM4CE0qXWIFvxQ/s1600/EPCHAN_F2.png) |
| Figure 2: Number of Tweets Per Hour of the Day |

The overall market sentiment can be estimated by aggregating the number of bullish and bearish labeled tweets each day. Based on the previous literature, I expected a significant bullish bias. This is confirmed in Figure 3 below with the daily mean percetage of bullish tweets being 79%.

| [![](img/1e43cb7b9c19d1bdcdaad477f27ffd41.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi4UckE-14HATB-Fa0vcc4E3Jh5fK0wedgV-iAqOGKYZSXhZPfhhwiT_v0yJIugfEc3iowyX49y9PfLf-1Rzkj3HiF0UJFibZcskwyW3RxJBjm2tntX212u68-Zf24EO-yM4eZe8Q/s1600/EPCHAN_F3.png) |
| Figure 3: Percentage of Bullish Tweets Each Day |

When writing a StockTwits tweet, users can tag multiple symbols so it is possible that the sentiment label could apply to more than one symbol. Tagging more than one symbol would likely indicate less specific sentiment and predictive potential so I hoped to find that most tweets only tag a single symbol. Looking at Figure 4 below, over 90% of the tweets tag a single symbol and a very small percentage tag 5+.

| [![](img/ef26f990ffe447348f7ec8744b3d1df3.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgv-iPZ41vfkHH6UpERLHqM0vPa27EYKFNF5iw-y_Tjhb0DpycJL4csiWBCSaTHnjFv_W6uJK4SpHF6KxSZUe1RtCMSWOkJ6pDMjLeSewKuQQWyneUsX4rXultgiWo8PRKHsB94nw/s1600/EPCHAN_F4.png) |
| Figure 4: Relative Frequency Histogram of the Number of Symbols Mentioned Per Tweet |

The time period of data used in my analysis is from 2012-11-01 to 2016-12-31\. In Figure 5 below, the top symbols, industries, and sectors by total labeled tweet count are shown. By far the most tweeted about industries were biotechnology and ETFs. This makes sense because of how volatile these industries are which hopefully means that they would be the best to trade based on social media sentiment data.

| [![](img/245b1f2d70de577bc136ceebba5becb2.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgl9DVhhRF_w498HGRmCdcgfjmDXxQMCI5z1r0GSOf_Q5ivg5WtqdZFSH0QaacYizzvWiIrcpt1dLxgrkZIsxWGvnUvGNtVPv2GDkuI_OO2d59Pxb7KZVwrwtjrKjlrz-SvIw4qCg/s1600/EPCHAN_F5.png) |
| Figure 5: Top Symbols, Industries, and Sectors by Total Tweet Count |

Now I needed to determine how I would create the sentiment score to best encompass the predictive potential of the data. Though there are obstacles to trading an open to close strategy including slippage, liquidity, and transaction costs, analyzing how well the sentiment score immediately before market open predicts open to close returns is a valuable sanity check to see if it would be useful in a larger factor model. The sentiment score for each day was calculated using the tweets from the previous market day’s open until the current day’s open:

S-Score =  (#Bullish-#Bearish)/(#Bullish+#Bearish)

This S-Score then needs to be normalized to detect the significance of a specific day’s sentiment with respect to the symbol’s historic sentiment trend. To do this, a rolling z-score is applied to the series. By changing the length of the lookback window the sensitivity can be adjusted. Additionally, since the data is quite sparse, days without any tweets for a symbol are given an S-Score of 0\. At the market open each day, symbols with an S-Score above the positive threshold are entered long and symbols with an S-Score below the negative threshold are entered short. Equal dollar weight is applied to the long and short legs. These positions are assumed to be liquidated at the day’s market close. The first test is on the universe of equities with previous day closing prices > $5\. With a relatively small long-short portfolio of ~250 stocks, its performance can be seen in Figure 6 below (click on chart to enlarge).

| [![](img/60a8d70b5813288728a130db4ed896e7.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEinEGmr3i2FmVbsWVUwb2EOlfcMLvp0GO2E6pSqcWin7cdJD8FNXsTHLCACsmNNTqgvG6b2OONY6-68EZmn4ELpV9YXRHYYnLfYN-nMRfX2aAcTQhqtHmIZIj3_v_S__51jZjTCdQ/s1600/Colton+Figure+6+new.png) |
| Figure 6: Price > $5 Universe Open to Close Cumulative Returns |

The thresholds were cherry-picked to show the potential of a 2.11 Sharpe Ratio but the results vary depending on the thresholds used. This sensitivity is likely due to the lack of tweet volume on most symbols. Also, the long and short thresholds are not equal in an attempt to maintain roughly equal number of stocks in each leg. The neutral basket contains all of the stocks in the universe that do not have an S-Score extreme enough to generate a long or short signal. Using the same thresholds as above, the test was ran on a liquidity universe which is defined as the top quartile of 50-day Average Dollar Volume stocks. As seen in Figure 7 below, the Sharpe drops to a 1.24 but is still very encouraging.

| [![](img/daadd0ef9562fd402fc8ed8383edd779.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhNhJ8CrcEgw_OLN686c1IA681rljDo0KjrxZqq7yX7d6oAaSgl57v1Y9Thb9mhEJbIMW-JtjiNPZJ7s7XXx5TVgOSghY7FZlCWFvlck1ZKYK6hCH7f-n9j53kAJH1wNCQKIo0tBw/s1600/Colton+Figure+7+new.png) |
| Figure 7: Liquidity Universe Open to Close Cumulative Returns |

The sensitivity of these results needs to be further inspected by performing analysis on separate train and test sets but I was very pleased with the returns that could be potentially generated from just labeled StockTwits data.

In July, I began working for

[Social Market Analytics](https://socialmarketanalytics.com/)

, the leading social media sentiment provider. Here at SMA, we run all the StockTwits tweets through our proprietary NLP engine to determine their sentiment scores. Using sentiment data from 9:10 EST which looks at an exponentially weighted sentiment aggregation over the last 24 hours, the open to close simulation can be ran on the price > $5 universe. Each stock is separated into its respective quintile based on its S-Score in relation to the universe’s percentiles that day. A long-short portfolio is constructed in a similar fashion as previously with long positions in the top quintile stocks and short positions in the bottom quintile stocks. In Figure 8 below you can see that the results are much better than when only using sentiment labeled data.

| [![](img/78ff019ea527fc7bc71ec726b0cb856f.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEirj_91_gg2auvfGtf12ZKnyJwNxnvBN6ntDO7BPUb1m7baJOSKcntX1LPLHDtkPgwTyLzrfTNjNNHTyVYLCAY0io8Gx6TGMGACUpQsqCOcbYaFvvwDeVEhmbt7Al_kHJ5LnUTVUQ/s1600/EPCHAN_F8.PNG) |
| Figure 8: SMA Open to Close Cumulative Returns Using StockTwits Data |

The predictive power is there as the long-short boasts an impressive 4.5 Sharpe ratio. Due to having more data, the results are much less sensitive to long-short portfolio construction. To avoid the high turnover of an open-to-close strategy, we have been exploring possible long-term strategies. Deutsche Bank’s Quantitative Research Team recently released a paper about strategies that solely use our SMA data which includes a longer-term strategy. Additionally, I’ve recently developed a strong weekly rebalance strategy that attempts to capture weekly sentiment momentum.

Though it is just the beginning, my dive into social media sentiment data and its application in finance over the course of my time consulting for QTS has been very insightful. It is arguable that by just using the labeled StockTwits tweets, we may be able to generate predictive signals but by including all the tweets for sentiment analysis, a much stronger signal is found. If you have questions please contact me at coltonsmith321@gmail.com.

*Colton Smith is a recent graduate of the University of Washington where he majored in Industrial and Systems Engineering and minored in Applied Math. He now lives in Chicago and works for Social Market Analytics. He has a passion for data science and is excited about his developing quantitative finance career. LinkedIn: [https://www.<wbr>linkedin.com/in/coltonfsmith/](https://www.linkedin.com/in/coltonfsmith/)*