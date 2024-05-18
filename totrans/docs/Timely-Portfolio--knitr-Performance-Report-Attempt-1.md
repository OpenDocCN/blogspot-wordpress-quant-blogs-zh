<!--yml
category: 未分类
date: 2024-05-18 15:07:40
-->

# Timely Portfolio: knitr Performance Report-Attempt 1

> 来源：[http://timelyportfolio.blogspot.com/2012/04/knitr-performance-report-attempt-1.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/04/knitr-performance-report-attempt-1.html#0001-01-01)

I get very excited about new R packages, but rarely is my excitement so fulfilled as with [knitr](http://yihui.name/knitr/).  Even with no skill, I have already been able to adapt the example Yihui Xie provides in his [**knitr Graphics Manual**](http://yihui.name/knitr/demo/graphics/) into a crude first version of a performance report that I could actually show clients and prospects.  Although this is far from production quality, two days of experimentation already has me to a level that assures me of the wonderful potential of combining the existing amazing R packages with knitr.  Before knitr, I do not believe I could have accomplished even this rough first draft.

If you have not played with [MiKTeX](http://www.miktex.org/) before, you will need to use the Package Manager to install the xcolor and tufte-handout templates for this example to work properly.  MiKTeX is installed automatically with [LyX](http://www.lyx.org) as discussed in yesterday’s post [Latex Allergy Cured by knitr](http://timelyportfolio.blogspot.com/2012/04/latex-allergy-cured-by-knitr.html).  If xcolor causes problems, then just change your repository to another repository.

[![image](img/76789f98812322b9b0b9c8e61a7b4b65.png "image")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjJPtpTFiNVdtQOcP6-OLC_RRJU3b1IGsnP9u9iwZcgzXs2XI04ENJmPK_0t-_KxmN1B8QYWcnB5aRy2DmVYMNFnxftU9PU9bvlfj4rulUkPF0YYODJ996s9da-lbCKzPqYt9gp3xRIVw/s1600-h/image%25255B2%25255D.png)[![image](img/a2336eb766aef1a065f1cecd385e8ef1.png "image")](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhdOKdFBnOKmchEHuJOehbMO0HnYpWr1OEh3Ai3oMFtlTltb5fiX3Kjb0tsU83onigoJmu6nlEcMFWIYas0lL_SA-ZNA_MEMMs79g_Q7JTPszB4W4yUTvCVzj2UNqldQ8MXGDwHyIhKAA/s1600-h/image%25255B5%25255D.png)

knitr weaved with a little PerformanceAnalytics, lattice, and latticeExtra provides this first draft.  As always, thanks so much to the brilliant contributors that have made this possible.

<embed src="http://www.box.com/embed/xus1u7evp8rdlmb.swf" wmode="opaque" type="application/x-shockwave-flash" allowfullscreen="true" allowscriptaccess="always">

[R code in GIST:](https://gist.github.com/2381629)