<!--yml
category: 未分类
date: 2024-05-18 15:42:47
-->

# Trading with Python: Getting short volume from BATS

> 来源：[http://tradingwithpython.blogspot.com/2013/08/getting-short-volume-from-bats.html#0001-01-01](http://tradingwithpython.blogspot.com/2013/08/getting-short-volume-from-bats.html#0001-01-01)

In my last post I have gone through the steps needed to get the short volume data from the BATS exchange. The code provided was however of the quick-n-dirty variety. I have now packaged everything to

[bats.py](https://code.google.com/p/trading-with-python/source/browse/trunk/lib/bats.py)

module that can be found on google code. (you will need the rest of the TradingWithPython library to run bats.py)

Usage:

```

import tradingWithPython as twp # main library
import tradingWithPython.lib.bats as bats # bats module

dl = bats.BATS_Data('C:\\batsData') # init with directory to save data
dl.updateDb() # update data
s = dl.loadData() # process zip files

```