<!--yml
category: 未分类
date: 2024-05-18 14:03:32
-->

# (Part 3) Time Machine Test – Currencies – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2010/05/13/part-3-time-machine-test-currencies/#0001-01-01](https://quantumfinancier.wordpress.com/2010/05/13/part-3-time-machine-test-currencies/#0001-01-01)

*Edit: This is a repost of the previous version of the post for currencies and commodities. When adapting my code for Datastream data, I made an error, the code was peeking which explains the ridiculously straight equity curve. Here is the corrected version of the post. I sincerely apologize to readers for the inconvenience. I also want to assure you that the previous results on equity indices are correct; I had a couple colleagues take a look at it to confirm that there were no bugs left.*

CAD
[![](img/e9a4e6a056b7363e913e8515ba813561.png "Time Machine Test Wilcox - CAD")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-wilcox-cad1.png)

EUR
[![](img/b8e868c95bdf4d911348047b9613f03e.png "Time Machine Test Wilcox - EUR")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-wilcox-eur1.png)

GBP
[![](img/5245e6cf1bb0ef6022d99bf1a03f7615.png "Time Machine Test Wilcox - GBP")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-wilcox-gbp1.png)

Results
[![](img/ffe9ada7e6fc42728b04b318ace7cea6.png "Time Machine Test Wilcox - ResultsCur")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-wilcox-resultscur1.png)

First thing I notice looking at these results is difference between the usefulness of run analysis on currencies. It makes sense since currencies are related in good part to macroeconomics factors. It is also much harder for the algorithm to find significant strategies, the time in the market for the strategy is much less than with equities.. Because of this, it becomes harder to squeeze out alpha out of the strategy with a high confidence level in the analysis.

QF