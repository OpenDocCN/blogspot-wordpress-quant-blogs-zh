<!--yml
category: 未分类
date: 2024-05-18 14:03:56
-->

# SVM Classification using RSI from Various Lengths – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2010/06/10/svm-classification-using-rsi-from-various-lengths/#0001-01-01](https://quantumfinancier.wordpress.com/2010/06/10/svm-classification-using-rsi-from-various-lengths/#0001-01-01)

First of all, I want to apologize for the lack of posting on the blog these days. I have been insanely busy with work (still am) and had trouble squeezing full posts in.

Today, I thought I would follow up on the [previous post on SVM learning](https://quantumfinancier.wordpress.com/2010/05/21/application-of-svms/). In this post I did exactly what I talked about in the post; the only input in the system is the RSI values for lengths 2 to 30 days associated with their respective results (up vs. down). The SVM algorithm is from the R package kernlab, and the parameters for the SVM itself are nu = 0.2, and C = 10\. Those are arbitrarily chosen and absolutely no optimization has been performed, the idea being only to give an example. Furthermore, I by no means suggest that this is the best setup or anything of the sort, I thought this would be a good example since it was previously discussed on the blog. Anyhow, here are the equity curves and some numbers compared to classic MR with RSI 2 50/50 as a proxy and buy and hold.

[![](img/9e85d9f49ebd5b06e753872baa0c4252.png "SVM - RSIs")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/06/svm-rsis1.png)

[![](img/5d364c644b776d6dd99d00a88e2fdd1f.png "SVM - RSIs results")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/06/svm-rsis-results.png)

Just eyeballing the chart, one can see that the SVM strategy adapt better to the the presence of a trend and outperform RSI 2 during the bull market, it also adapted fairly well to the recent turmoil, performing slightly worse than the short term MR strategy. I plan to share some code but don’t want to clutter the blog with lines and lines of code, so once I figure out the best way to do this, (I am thinking a downloadable file or something like it) I will proceed. Finally, if readers have played around with SVM I welcome suggestions and comments as always !

QF