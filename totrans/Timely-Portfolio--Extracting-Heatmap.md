<!--yml
category: 未分类
date: 2024-05-18 14:49:45
-->

# Timely Portfolio: Extracting Heatmap

> 来源：[http://timelyportfolio.blogspot.com/2015/03/extracting-heatmap.html#0001-01-01](http://timelyportfolio.blogspot.com/2015/03/extracting-heatmap.html#0001-01-01)

Inspired by this tweet, I wanted to try to do something similar in JavaScript.

Fortunately, I had this old post [Chart from R + Color from Javascript](http://timelyportfolio.blogspot.com/2014/07/chart-from-r-color-from-javascript.html) to serve as a reference, and I got lots of help from these links.

In a couple of hours, I got this crude but working [rendering](http://timelyportfolio.github.io/rCharts_color_thief/index_jsfeat.html) complete with a d3.js brush to get the scale.  Then since this is sort of a finance blog, I imagined we found an old correlation heatmap like the one in [Pretty Correlation Map of PIMCO Funds](http://timelyportfolio.blogspot.com/2012/06/pretty-correlation-map-of-pimco-funds.html).  Although, we could guess at the correlation values, I thought it would be a lot more fun to get live values.  Try it out below.

1.  Brush over the scale / legend
2.  Input scale min and max
3.  Mouseover color areas in the chart

As I said, it is rough, but it works. It needs a little UI work :)