<!--yml
category: 未分类
date: 2024-05-12 19:46:13
-->

# Automated trading 101 | Coding the markets

> 来源：[https://etrading.wordpress.com/2007/07/07/automated-trading-101/#0001-01-01](https://etrading.wordpress.com/2007/07/07/automated-trading-101/#0001-01-01)

## Automated trading 101

### July 7, 2007

When coding up an automated trading component for your etrading system, always give it a read only mode. Why ?  Because no matter how many automated tests, simulations and replays of live data you’ve done in your test environment, your code may still have failed to anticipate some anomaly in the live environment. And then you’ll find it trades in the wrong size, or at the wrong price, or on the wrong side etc…

How to avoid this ?  Code so you have a silent mode that doesn’t execute any trades, but does log the trades it would have done, and the market environment at that time. Then get your sponsor on the desk to look through the log, review & sign off. And only then, take a deep breath and push the big red button…