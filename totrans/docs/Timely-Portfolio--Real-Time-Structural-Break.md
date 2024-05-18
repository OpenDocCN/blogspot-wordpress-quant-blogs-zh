<!--yml
category: 未分类
date: 2024-05-18 15:07:16
-->

# Timely Portfolio: Real Time Structural Break

> 来源：[http://timelyportfolio.blogspot.com/2012/04/real-time-structural-break.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/04/real-time-structural-break.html#0001-01-01)

Yesterday as I played with bfast I kept thinking “Yes, but this is all in hindsight.  How can I potentially use this in a system?”  Fortunately, one of the fine authors very generously commented on my post [Structural Breaks (Bull or Bear?)](http://timelyportfolio.blogspot.com/2012/04/structural-breaks-bull-or-bear.html):

> “Jan Verbesselt Apr 27, 2012 02:01 AM
> 
> Nice application! you can also detect seasonal breaks. also check some new near real-time disturbance detection functionality using bfastmonitor() http://bfast.r-forge.r-project.org/Verbesselt+Zeileis+Herold-2012.pdf
> cheers, Jan”

And away I went on an unexpected but very pleasant journey into bfastmonitor.  Please see the following paper for all the details.

> [Jan Verbesselt, Achim Zeileis, Martin Herold (2011). Near Real-Time Disturbance
>   Detection in Terrestrial Ecosystems Using Satellite Image Time Series: Drought
>   Detection in Somalia. Working Paper 2011-18\. Working Papers in Economics and
>   Statistics, Research Platform Empirical and Experimental Economics, Universitaet
>   Innsbruck. URL http://EconPapers.RePEc.org/RePEc:inn:wpaper:2011-18](http://scholar.google.com/scholar?cluster=9016488513865299942&hl=en&as_sdt=0,1)

Doing a walk-forward test seemed like the best method of testing and illustration, so I chose the excruciating and incredibly volatile period from late 2008 to early 2009 as our example.  Amazingly, it picked with no optimizing or manual intervention March 2009 as the breakpoint. Of course, we would not know this until the end of March, but picking real-time with only a month lag is unbelievable to me.  Please try it out, and let me know your results.  Of course, I already have the 30 year bond bull in mind as a next trial.

Thanks to Yihui Xie who resurfaced again ([see posts on knitr](http://timelyportfolio.blogspot.com/search/label/knitr)) with his animation package, which I used to create a good old-fashioned animated GIF.  I wish I had time to play more with the prettier and more robust options offered by the package.

[![animation](img/681bf18f9cefdcfc0a53dd0d2df1fc11.png "animation")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjTBXCl0YwcHCDuo1awf-OIpQ4ocQ1m0Tob2bA43nYd14MssSyVF7qVg_2-Au3KO3BytjY76o4qlwa8Ey5jduk4Le7z_eMsrNjYc7Fdh4eKr7U2VGfjKSdMHjQ9UWuOHZt-wrF3RDL5IQ/s1600-h/animation%25255B2%25255D.gif)

[R code from GIST:](https://gist.github.com/2510469)