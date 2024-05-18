<!--yml
category: 未分类
date: 2024-05-18 15:00:53
-->

# Timely Portfolio: One Pager Performance Report with knitr, R, and a Different Font

> 来源：[http://timelyportfolio.blogspot.com/2013/03/one-pager-performance-report-with-knitr.html#0001-01-01](http://timelyportfolio.blogspot.com/2013/03/one-pager-performance-report-with-knitr.html#0001-01-01)

Although I suffer from complete ignorance of typography, with a little help from a [post from Hyndsight](http://robjhyndman.com/hyndsight/xelatex/) and [post from mages' blog](http://lamages.blogspot.com/2011/10/using-sweave-with-xelatex.html), I wanted to try a different font on the one-pager performance report that we created in [Onepager Now with knitR](http://timelyportfolio.blogspot.com/2013/02/onepager-now-with-knitr.html). I do not think [Open Sans Light](http://www.google.com/webfonts/specimen/Open+Sans) is the best choice for this report, but since it is the most popular font on Google I figured I could not be criticized too heavily by those more knowledgeable than me in typography.

> ```
> options(tikzDefaultEngine = "xetex")
> 
> require(knitr)
> 
> knit2pdf("onepager_text_graphics-knitr.rnw", compiler = "xelatex")
> 
> ```

And the result ([go to Box](https://www.box.com/s/4nftk6qpa0cugapmncsn) if the embed does not appear below):

<embed src="https://www.box.com/embed/21h288ynrh19eh5.swf" wmode="opaque" type="application/x-shockwave-flash" allowfullscreen="true" allowscriptaccess="always">

[R code from GIST:](https://gist.github.com/timelyportfolio/5189615)