<!--yml
category: 未分类
date: 2024-05-18 15:41:53
-->

# Trading with Python: Yahoo is dead, long live Yahoo!

> 来源：[http://tradingwithpython.blogspot.com/2017/05/yahoo-is-dead-long-live-yahoo.html#0001-01-01](http://tradingwithpython.blogspot.com/2017/05/yahoo-is-dead-long-live-yahoo.html#0001-01-01)

On 18 May 2017 the ichart data api of yahoo finance went down, without any notice. And it does not seem like it is coming back. This has left many (including me) with broken code and without a descent free end-of-day data source. Something needs to be done. Now.

Apparently Yahoo! does not want us to download free data automatically, but it is still possible to download it by hand, clicking the 'download' button on the

[ticker webpage](https://uk.finance.yahoo.com/quote/SPY/history?p=SPY)

. Automatic downloading is made more difficult by using a

*cookie-crub*

 pair, but luckily still possible.

I'm now working on updating the

*tradingWithPython.yahooFinance *

library and as a part of that work I've created a proto script that shows how to get the data. Because so many are now  scrambling to get their code working, I'm sharing this as soon as possible.

[The notebook can be found on Github,](https://github.com/sjev/trading-with-python/blob/master/scratch/get_yahoo_data.ipynb)

enjoy!

**Update:** *[yahooFinance.py](https://github.com/sjev/trading-with-python/blob/fix_yahoo/lib/yahooFinance.py)*

has been fixed!

*Note:*

the data provided seems to be adjusted for splits, but not for dividends.