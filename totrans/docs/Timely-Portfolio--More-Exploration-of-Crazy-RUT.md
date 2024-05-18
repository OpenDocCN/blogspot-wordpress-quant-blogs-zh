<!--yml
category: 未分类
date: 2024-05-18 15:05:34
-->

# Timely Portfolio: More Exploration of Crazy RUT

> 来源：[http://timelyportfolio.blogspot.com/2012/07/more-exploration-of-crazy-rut.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/07/more-exploration-of-crazy-rut.html#0001-01-01)

Unintentionally while playing with the lawstat package in R, I started trying to build systems (STANDARD DISCLAIMER: NOT INVESTMENT ADVICE AND WILL LOSE LOTS OF MONEY SO PROCEED WITH CAUTION) based on the Jarque Bera test of normality ([entry in Wikipedia](http://en.wikipedia.org/wiki/Jarque%E2%80%93Bera_test) or the research paper [http://scholar.google.com/scholar?cluster=18293285759900281575&hl=en&as_sdt=0,1](http://scholar.google.com/scholar?cluster=18293285759900281575&hl=en&as_sdt=0,1 "http://scholar.google.com/scholar?cluster=18293285759900281575&hl=en&as_sdt=0,1")).  Since I was only playing around, I sort of deliberately curve fitted a system to work on the Russell 2000.  After a lot of experimentation, I came up with something very interesting, which led me to test on multiple other indexes.  It seemed to only really work well on the Russell 2000 and mainly over the last 5 years, which of course led me right back to the question posed in [Crazy RUT](http://timelyportfolio.blogspot.com/2011/07/crazy-rut.html) and explored again in [Crazy RUT in Academic Context Why Trend is Not Your Friend](http://timelyportfolio.blogspot.com/2012/06/crazy-rut-in-academic-context.html), which is “Why don’t most momentum systems work over the last decade on the Russell 2000 when they work on almost all other indexes?”  Please let me know if you have a good explanation, or if you want to test for regimes. Here is the result. I apologize that I spent little time on making these pretty.

Even more strange is that the system applied to Kenneth French’s small classification shows different results.

Here is how the system looks on the S&P 500, and again certainly nothing special.

[R code from GIST (do raw for copy/paste):](https://gist.github.com/3056379)