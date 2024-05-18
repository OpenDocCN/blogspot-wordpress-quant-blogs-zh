<!--yml
category: 未分类
date: 2024-05-18 15:05:22
-->

# Timely Portfolio: Best of Axys, R, d3.js, and HTML5

> 来源：[http://timelyportfolio.blogspot.com/2012/07/best-of-axys-r-d3js-and-html5.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/07/best-of-axys-r-d3js-and-html5.html#0001-01-01)

Axys, R, d3.js, and HTML5 all offer incredibly powerful tools for investment management and reporting, but they are not set up to synergistically interact to fill each other’s gaps and leverage each other’s strengths.  In my ideal scenario, Axys serves as the accounting system and performance calculator, R serves as the advanced financial/statistical engine, d3.js serves as the interactive reporting component, and HTML5 offers the user interface and ties everything together through websockets ([nicely demoed here](http://www.websocket.org/demos.html)).  After working and suffering with Axys for 12 years, I am amazed that it all seems to be coming together.  I provided a bare proof of concept for Axys to d3.js in my post [Axys to d3.js Error Catching and Formatting](http://timelyportfolio.blogspot.com/2012/07/axys-to-d3js-error-catching-and.html).  Now let’s extend that to R and websockets through the generously contributed [R websockets package](http://illposed.net/websockets.html).  I have borrowed very heavily from the author's Youtube example presented in

[http://www.youtube.com/embed/0iR8Fo0jwW8](http://www.youtube.com/embed/0iR8Fo0jwW8)

VIDEO

In this proof of concept, Axys will calculate performance and send to Excel through a graph macro which creates JSON and an html page (thanks Bruce [http://excelramblings.blogspot.com/](http://excelramblings.blogspot.com/ "http://excelramblings.blogspot.com/")).  The html page contains javascript and d3.js to produce a simple bar chart.  Now we add a button to take the JSON created by Excel and embedded in our html and send it to R.  R will produce a charts.PerformanceSummary chart and send it back as jpeg to the html page.  The html page will receive the image and replace the d3.js bar chart with the image.

[http://www.youtube.com/embed/xC1daKifHvw](http://www.youtube.com/embed/xC1daKifHvw)

VIDEO

Going forward I will only use R as the statistical engine and continue to rely on d3.js for the interactive reporting.  How far I go with this depends heavily on user response.  Please let me know if you would like me to continue down this path.

The list of acknowlegements is starting to get long.  I really appreciate all the fine work done by Mike Bostock on d3.js [https://github.com/mbostock/d3/wiki](https://github.com/mbostock/d3/wiki "https://github.com/mbostock/d3/wiki"), the dedicated authors of the R package PerformanceAnalytics [http://cran.r-project.org/web/packages/PerformanceAnalytics/index.html](http://cran.r-project.org/web/packages/PerformanceAnalytics/index.html "http://cran.r-project.org/web/packages/PerformanceAnalytics/index.html"), Brian the author of [http://illposed.net/websockets.html](http://illposed.net/websockets.html "http://illposed.net/websockets.html") and [the example](http://bigcomputing.com/PerformanceAnalytics.R), the author of RJSONIO [http://cran.r-project.org/web/packages/RJSONIO/index.html](http://cran.r-project.org/web/packages/RJSONIO/index.html "http://cran.r-project.org/web/packages/RJSONIO/index.html"), and Bruce McPherson at [http://excelramblings.blogspot.com/](http://excelramblings.blogspot.com/ "http://excelramblings.blogspot.com/") for the inspirational idea.

To work through on your own, you will need the Excel file [cdataset.xlsm](https://www.box.com/s/ec9ddf33cefd5fd7cf10), the Axys report [perhstsp.rep](https://www.box.com/s/yhdagoqpznif8248etc5), and the [R code from GIST](https://gist.github.com/3145541).