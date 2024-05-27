<!--yml

分类：未分类

日期：2024-05-18 15:43:16

-->

# 用 Python 交易：功夫熊猫将解决你的数据问题

> 来源：[`tradingwithpython.blogspot.com/2011/10/kung-fu-pandas-will-solve-your-data.html#0001-01-01`](http://tradingwithpython.blogspot.com/2011/10/kung-fu-pandas-will-solve-your-data.html#0001-01-01)

我喜欢研究策略，但遗憾的是我花太多时间在像过滤和校准数据集这样的低级工作上。事实上，我大约 80%的时间都花在这上面。一定有比我自己编写所有过滤代码更好的方法，确实有！

以前不久，我遇到了一个数据分析工具包

[pandas](http://pandas.sourceforge.net/)

特别是适用于处理金融数据。仅仅触及到它的功能表面，我就已经被它所提供的功能所震撼。这个包正在由

[Wes McKinney ](http://wesmckinney.com/blog/)

他的野心是创建最强大、最灵活的开源数据分析/操作工具。嗯，我认为他已经走在正确的道路上！

我们来看看把两个数据集对齐是多么简单：

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

两行代码！(这本来可以缩减到一行，但我为了可读性而将其拆分)

以下是结果：

哎呀，这本来可以节省我大量的时间！但它仍然会在将来帮助我，因为我会将其 DataFrame 对象作为我在未来工作中的标准。
