<!--yml
category: 未分类
date: 2024-05-18 15:43:08
-->

# Trading with Python: Plotting with guiqwt

> 来源：[http://tradingwithpython.blogspot.com/2011/12/plotting-with-guiqwt.html#0001-01-01](http://tradingwithpython.blogspot.com/2011/12/plotting-with-guiqwt.html#0001-01-01)

While it's been quiet on this blog, but behind the scenes I have been very busy trying to build an interactive spread scanner. To make one, a list of ingredients is needed:

gui toolkit: pyqt -check.

data aquisition: ibpy & tradingWithPython.lib.yahooData - check.

data container: pandas & sqlite - check.

plotting library: matplotlib - ehm... No.

After tinkering with matplotlib in pyqt for several days I must admit its use in interactive applications is far from optimal. Slow, difficult to integrate and little interactivity. PyQwt proven to work a little better, but it had its own quirks, a little bit too low-level for me.

But as it often happens with Python, somebody, somewhere has already written a kick-ass toolkit that is just perfect for the job. And it looks like 

[guiqwt](http://packages.python.org/guiqwt/index.html)

 is just it. Interactive charts are just a couple of code lines away now, take a look at an example here: 

[Creating curve dialog](http://code.google.com/p/trading-with-python/source/browse/trunk/cookbook/guiqwt_CurveDialog.py)

 . For this I used guiqwt example code with some minor tweaks.

And of course a pretty picture of the result:

...If only I knew how to set dates on the x-axis....