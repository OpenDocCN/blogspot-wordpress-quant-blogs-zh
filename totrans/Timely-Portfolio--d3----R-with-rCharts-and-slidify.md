<!--yml
category: 未分类
date: 2024-05-18 15:00:13
-->

# Timely Portfolio: d3 <- R with rCharts and slidify

> 来源：[http://timelyportfolio.blogspot.com/2013/04/d3-r-with-rcharts-and-slidify.html#0001-01-01](http://timelyportfolio.blogspot.com/2013/04/d3-r-with-rcharts-and-slidify.html#0001-01-01)

I believe that the NY Times interactive feature [512 Paths to the White House](http://www.nytimes.com/interactive/2012/11/02/us/politics/paths-to-the-white-house.html?_r=0) is one of the best visualizations of all time.  It is even better when we have details on the [process of creating this marvel](http://chartsnthings.tumblr.com/post/35616801795/some-sketches-from-the-times-scenario-builder).   Although the graphic is not suited for other data sources (please tell me if this is not correct), I just could not resist using the amazing R packages [slidify](http://slidify.org) and [rCharts](https://github.com/ramnathv/rCharts) from [Ramnath Vaidyanathan](https://github.com/ramnathv) to build it from R.  I wouldn’t have even thought it possible until I saw his tutorial [Replicating NY Times Interactive Graphic](http://ramnathv.github.io/rChartsNYT/) and his demo [Visualizing the Reinhart and Rogoff Public Debt Study](http://glimmer.rstudio.com/ramnathv/rChartsRogoff/).

> I have a feeling that nearly every R user of lattice or ggplot2 will be familiar with Ramnath’s brilliance by the end of the year 2013\. He might even convince some d3 users to try a little R.

Even more amazing is the entire tutorial embedded below (click [here](http://timelyportfolio.github.io/rCharts_512paths/) if it does not appear) is created in R with [slidify](http://slidify.org), so it is entirely reproducible.  rCharts is early in development, but I urge you to try it out.