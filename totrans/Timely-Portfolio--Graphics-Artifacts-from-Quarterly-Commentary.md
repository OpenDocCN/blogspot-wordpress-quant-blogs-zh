<!--yml
category: 未分类
date: 2024-05-18 15:05:38
-->

# Timely Portfolio: Graphics Artifacts from Quarterly Commentary

> 来源：[http://timelyportfolio.blogspot.com/2012/07/graphics-artifacts-from-quarterly.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/07/graphics-artifacts-from-quarterly.html#0001-01-01)

For my Q2 2012 commentary, I tried multiple graphs to illustrate the disconnect of the US stock markets with the rest of the world.  I think I finally settled on this simple Excel bar graph populated by Bloomberg data, but I thought some might like to see some of the R graphical artifacts as I explored how best to illustrate my point.

Although I settled on a 1 year performance chart, I really wanted to show more history, but without all the noise of a daily, weekly, or even monthly chart.  I tried a chart connecting the 200 day max/min points, but it still seemed noisy and difficult to follow. One big letdown was Yahoo! Finance not providing DJUBS, E1DOW, or P1DOW any more.

I then thought connecting the end of year points might offer a nice simplification, and I probably liked this best of the R charts.  This shows enough of the path to see the universal move up to 2010, and then the disconnect.

Even one R base graphics chart. Thanks again [Josh](http://blog.fosstrading.com/) for the fork.

As one other option, I thought I would try to just connect beginning, middle, and end since December 2008.  This certainly shows the huge disconnect between the U.S. and the rest of the world, but I found it difficult to describe the methodology within the chart.

I hope this helps someone somewhere.  As always, I very much enjoy comments and opinions.

[R code in GIST (do raw for copy/paste):](https://gist.github.com/3035700)