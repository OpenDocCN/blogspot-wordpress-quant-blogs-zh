<!--yml
category: 未分类
date: 2024-05-18 15:05:10
-->

# Timely Portfolio: Hi R and Axys, I’m d3.js “Nice to Meet You” (On the Iphone)

> 来源：[http://timelyportfolio.blogspot.com/2012/07/hi-r-and-axys-im-d3js-nice-to-meet-you.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/07/hi-r-and-axys-im-d3js-nice-to-meet-you.html#0001-01-01)

I am still definitely in the proof of concept stage, but as I progress I get more excited about the prospects of combining d3.js with R and Axys through Bryan Lewis’ really nice R websockets package (even nicer now that he has added the daemonize function).  In this iteration, I will add a cumulative growth line chart, some animation and transitions, and then javascript will ask R to calculate drawdowns.  Instead of R returning a chart like last time, R will send the results of the drawdown calculations through JSON through the websocket.  We will then use d3.js to draw a line chart of drawdowns.  This becomes really powerful when we consider the existing and [thanks to Google Summer of Code soon to be added](http://www.google-melange.com/gsoc/project/google/gsoc2012/matthieu_ensimag/26001) risk/return calculations offered by the R PerformanceAnalytics package.

As one last bonus at the end of the video you will see that we can get this interactive reporting experience and websocket communication all on our Iphone and Ipad.

As a quick review of what is happening

1.  Axys runs a report called perhstsp.rep.
2.  Axys calls the cdataset.xlsm testd3axys macro and sends performance information.
3.  Excel cdataset.xlsm testd3axys macro does some very basic formatting, converts the data to JSON, creates a webpage, and opens the webpage in the default browser.
4.  Browser opens the webpage and d3.js generates a bar graph of performance and then a cumulative growth line chart.
5.  Browser provides a button to open a websocket with R and send the performance information originally calculated in Axys.
6.  R receives the performance data through the websocket, calculates drawdown, and then sends the drawdown calculations as JSON back to the browser.
7.  Browser receives the drawdown calculations and d3.js plots them as a line chart.

[http://www.youtube.com/embed/jz0cpO3Kp4Q](http://www.youtube.com/embed/jz0cpO3Kp4Q)

VIDEO

The next set of iterations will focus on cleaning up the d3.js charts and adding interactivity.

So far I have received no comments.  Please let me know what you think about this.

The list of acknowlegements is starting to get long. I really appreciate all the fine work done by Mike Bostock on d3.js [https://github.com/mbostock/d3/wiki](https://github.com/mbostock/d3/wiki "https://github.com/mbostock/d3/wiki"), the dedicated authors of the R package PerformanceAnalytics [http://cran.r-project.org/web/packages/PerformanceAnalytics/index.html](http://cran.r-project.org/web/packages/PerformanceAnalytics/index.html "http://cran.r-project.org/web/packages/PerformanceAnalytics/index.html"), Bryan the author of [http://illposed.net/websockets.html](http://illposed.net/websockets.html "http://illposed.net/websockets.html") and [the example](http://bigcomputing.com/PerformanceAnalytics.R), the author of RJSONIO [http://cran.r-project.org/web/packages/RJSONIO/index.html](http://cran.r-project.org/web/packages/RJSONIO/index.html "http://cran.r-project.org/web/packages/RJSONIO/index.html"), and Bruce McPherson at [http://excelramblings.blogspot.com/](http://excelramblings.blogspot.com/ "http://excelramblings.blogspot.com/") for the inspirational idea.

To work through on your own, you will need the Excel file [cdataset.xlsm](https://www.box.com/s/ec9ddf33cefd5fd7cf10), the Axys report [perhstsp.rep](https://www.box.com/s/yhdagoqpznif8248etc5), and the [R code from GIST](http://bl.ocks.org/3190664).