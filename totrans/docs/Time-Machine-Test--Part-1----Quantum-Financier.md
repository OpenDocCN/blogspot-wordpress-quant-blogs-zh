<!--yml
category: 未分类
date: 2024-05-18 14:03:15
-->

# Time Machine Test (Part 1) – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2010/05/10/time-machine-test-part-1/#0001-01-01](https://quantumfinancier.wordpress.com/2010/05/10/time-machine-test-part-1/#0001-01-01)

This series of post is based on [CSS Analytics’ Time-Machine post series](http://cssanalytics.wordpress.com/2009/09/14/busting-the-efficient-markets-hypothesis-the-adaptive-market-time-machine/). I recommend you read it, since I this is not my original idea. However, I do think that my implementation differs slightly from CSS Analytics’.

The following results represent backtests using my version of the algorithm on different equity indices on all free historical data available for each ticker. I used index data since the available data points go way further in history. I did test the algorithm on available ETFs with similar results. All results presented below are frictionless.

S&P 500

[![](img/0c36dd0f037829360b697f798e81844a.png "Time Machine Test - GSPC")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-gspc2.jpg)

RUSSELL 2000

[![](img/c5a9b873277ce6aafcd1e1fcdf27769e.png "Time Machine Test - RUT")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-rut.jpg)

NASDAQ 100

[![](img/e8d27f44f3d0f1472f6c68b3bb64aa60.png "Time Machine Test - NDX")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-ndx.jpg)

S&P/TSX Comp. (Can)

[![](img/51081aaba05c01a5d0838ab809539c06.png "Time Machine Test - GSPTSE")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-gsptse.jpg)

FTSE 100 (U.K.)

[![](img/da8df848c71a61706ea460bc84ff4fc1.png "Time Machine Test - FTSE")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-ftse.jpg)

NIKKEI 225 (JAP)

[![](img/ae0a439b133eb00467e55f41a663bd61.png "Time Machine Test - N225")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-n225.jpg)

HANG SENG (CHN)

[![](img/b0c24c1037521ba12b7528078247d43d.png "Time Machine Test - HSI")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-hsi.jpg)

Summary

[![](img/ea969a1a5bc0025274f88644bb7e8450.png "Time Machine Test - Results")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-results.jpg)

As the results above show, the algorithm is quite robust and does adapt fairly well to different market regimes as well as to the differences in market behavior for all these indices. Regardless, I think this is a very nice and simple concept that can still be improved.

I will try several modifications to the algorithm in the next few posts or so. For now you can expect tests on different asset classes: commodities, futures, currencies, etc. I also want to try to replace the t-test with a non-parametric Wilcoxon signed-rank test and see how the strategy performs when we get rid of the normality assumption when testing for significance. I also have other ideas in mind to improve the algorithm, stay tuned!

QF