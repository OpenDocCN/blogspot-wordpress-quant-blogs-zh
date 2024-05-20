<!--yml
category: 未分类
date: 2024-05-18 15:11:19
-->

# Timely Portfolio: Generosity of Asian Central Banks

> 来源：[http://timelyportfolio.blogspot.com/2011/10/generosity-of-asian-central-banks.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/10/generosity-of-asian-central-banks.html#0001-01-01)

The only thing that separates the United States from Europe and the notorious PIIGS is the generosity of Asian Central Banks who have been consistently quantitatively easing since 1998 ([Join the Reserves](http://timelyportfolio.blogspot.com/2011/07/join-reserves.html)).

Without this generosity, the United States could very easily have entered a death spiral (see [Death Spiral of a Country](http://timelyportfolio.blogspot.com/2011/03/death-spiral-of-country.html) and [Death Spiral Warning Graph](http://timelyportfolio.blogspot.com/2011/03/death-spiral-warning-graph.html)) in 2008 and still might fall into this disastrous trap.

Deliberately attacking this very tenuous thread seems foolish, but this foolish action has found support with our fine politicians [Washington Post "Senate approves China currency bill"](http://www.washingtonpost.com/blogs/2chambers/post/senate-approves-china-currency-bill/2011/10/11/gIQAhvaUdL_blog.html).  The US needs to recruit some US $ buyers, but unfortunately there are none to fill the multi-trillion dollar gap.

Even more concerning is the focus on China who has been steadily attacking the problem.  The focus on China does not make sense when you look at the appreciation of the Chinese Yuan.  I see a lot more Korean cars on the road and TVs and appliances in the stores, but I do not hear any mention of the extreme undervaluation of the Korean Won to the US$ but especially the Japanese Yen, so it appears the Koreans Won.

I agree that the US$ reserve building needs to stop, but let’s not deliberately induce a positive feedback death spiral.

[R code (click to download from Google Docs):](https://docs.google.com/leaf?id=0B2qp2r96khJPMDVjMWE3ZjktMTM0Yi00MzkyLWI0MmQtOWM5MTBjNzRmYzBh&hl=en_US)

require(quantmod)
require(PerformanceAnalytics)

getSymbols("DEXCHUS",src="FRED")
getSymbols("DEXKOUS",src="FRED")

plot.zoo(merge(1/DEXCHUS,100/DEXKOUS)["1997::",],screens=1,lwd=2,
    col=c("lightblue4","antiquewhite4"),
    xlab="Year",ylab=NA,
    main="Chinese Yuan and Korean Won
    1997 to Sep 2011")
legend("right", c("China","Korea"), lwd = 2, bty="n",
    col=c("lightblue4","antiquewhite4"),y.intersp=2,
    text.col=c("lightblue4","antiquewhite4"))