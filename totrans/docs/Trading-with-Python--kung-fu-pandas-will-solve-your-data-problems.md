<!--yml
category: 未分类
date: 2024-05-18 15:43:16
-->

# Trading with Python: kung fu pandas will solve your data problems

> 来源：[http://tradingwithpython.blogspot.com/2011/10/kung-fu-pandas-will-solve-your-data.html#0001-01-01](http://tradingwithpython.blogspot.com/2011/10/kung-fu-pandas-will-solve-your-data.html#0001-01-01)

I love researching strategies, but sadly I spend too much time on low-level work like filtering and aligning datasets. In fact, about 80% of my time is spent on this mind numbing work. There had got to be a better way than hacking all the filtering code myself, and there is!

Some time ago I've come across a data analysis toolkit

[pandas](http://pandas.sourceforge.net/)

especially suited for working with financial data. After just scratching the surface of its capabilities I'm already blown away by what it delivers. The package is being actively developed by

[Wes McKinney ](http://wesmckinney.com/blog/)

 and his ambition is to create the most powerful and flexible open source data analysis/manipulation tool available. Well, I think he is well on the way!

Let's take a look at just how easy it is to align two datasets:

```
from tradingWithPython.lib import yahooFinance

startDate = (2005,1,1)

# create two timeseries. data for SPY goes much further back
# than data of VXX
spy = yahooFinance.getHistoricData('SPY',sDate=startDate)
vxx = yahooFinance.getHistoricData('VXX',sDate=startDate)

# Combine two datasets
X = DataFrame({'VXX':vxx['adj_close'],'SPY':spy['adj_close']})

# remove NaN entries
X= X.dropna()
# make a nice picture
X.plot()

```

Two lines of code! ( this could be even fit to one line, but I've split it for readability)

Here is the result:

Man, this could have saved me a ton of time! But it still will help me in the future, as I'll be using its DataFrame object as a standard in my further work.