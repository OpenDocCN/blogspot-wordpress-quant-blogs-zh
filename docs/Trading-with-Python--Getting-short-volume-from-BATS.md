<!--yml

分类：未分类

日期：2024-05-18 15:42:47

-->

# 使用 Python 交易：从 BATS 获取短期交易量

> 来源：[`tradingwithpython.blogspot.com/2013/08/getting-short-volume-from-bats.html#0001-01-01`](http://tradingwithpython.blogspot.com/2013/08/getting-short-volume-from-bats.html#0001-01-01)

在我上一篇文章中，我详细介绍了从 BATS 交易所获取短期交易量数据的步骤。提供的代码属于快速且简陋的类型。现在我将所有内容打包在一起。

[bats.py](https://code.google.com/p/trading-with-python/source/browse/trunk/lib/bats.py)

可以在谷歌代码上找到的模块（运行 bats.py 还需要 TradingWithPython 库的其他部分）。

使用方法：

```

import tradingWithPython as twp # main library
import tradingWithPython.lib.bats as bats # bats module

dl = bats.BATS_Data('C:\\batsData') # init with directory to save data
dl.updateDb() # update data
s = dl.loadData() # process zip files

```
