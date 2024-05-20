<!--yml
category: 未分类
date: 2024-05-18 14:54:27
-->

# Timely Portfolio: R as a Publishing Engine | CPI Components Use Case

> 来源：[http://timelyportfolio.blogspot.com/2014/04/r-as-publishing-engine-cpi-components.html#0001-01-01](http://timelyportfolio.blogspot.com/2014/04/r-as-publishing-engine-cpi-components.html#0001-01-01)

R was certainly not designed to be a publishing engine, but in my workflow, R is the primary method of content creation.  With that in mind, I have been thinking about a very different use case of rCharts in which we might want to include inflexible and not really reusable custom javascript components in our document.  As a quick example after updating my CPI component graph using d3.js and angular, I want to plug it into a document and really only need to modify a couple of parameters.  While someone might want to use this for different data, I doubt it.

rCharts seamless integration with knitr/slidify/Rpres makes this very easy.  I just wonder how popular this will become.

[![image](img/52a444b6a2755a80ef09cf1650fcc643.png "image")](http://timelyportfolio.github.io/rCharts_d3_cpi/index.html)