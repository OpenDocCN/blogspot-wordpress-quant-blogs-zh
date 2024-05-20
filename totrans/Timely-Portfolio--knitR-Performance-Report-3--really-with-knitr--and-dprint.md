<!--yml
category: 未分类
date: 2024-05-18 15:06:51
-->

# Timely Portfolio: knitR Performance Report 3 (really with knitr) and dprint

> 来源：[http://timelyportfolio.blogspot.com/2012/05/knitr-performance-report-3-really-with.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/05/knitr-performance-report-3-really-with.html#0001-01-01)

*please see [knitr Performance Report–Attempt 3](http://timelyportfolio.blogspot.com/2012/05/knitr-performance-reportattempt-3.html), [knitr Performance Report-Attempt 2](http://timelyportfolio.blogspot.com/2012/04/knitr-performance-report-attempt-2.html) and [knitr Performance Report-Attempt 1](http://timelyportfolio.blogspot.com/2012/04/knitr-performance-report-attempt-1.html)*

[alstated](http://yihui.name/knitr/options "http://yihui.name/knitr/options")’s asked a very good question in his comment on [knitr Performance Report–Attempt 3](http://timelyportfolio.blogspot.com/2012/05/knitr-performance-reportattempt-3.html), and I’m not sure I could have answered well until I endured some frustrations with Sweave.  I actually did not use knitr for that report, and I struggled with many of the issues that knitr addresses.  knitr’s power comes in its extra ability to control output with additional chunk options described in [http://yihui.name/knitr/options](http://yihui.name/knitr/options "http://yihui.name/knitr/options"), so no more wide, textblock, etc. latex commands.

A very prominent R Finance contributor also alerted me to the dprint (be aware in pre-Alpha) package from Carl Brickner [https://r-forge.r-project.org/projects/tabular/](https://r-forge.r-project.org/projects/tabular/) presented at [userR! 2010](http://user2010.org/slides/Brickner+Slavov+Napoli.pdf) and also at .  To use, you will have to manually install with the command:

> install.packages("dprint", repos="[http://R-Forge.R-project.org](http://R-Forge.R-project.org)")

For the final pdf, use the knit2pdf command from knitr:

> knit2pdf(“pathtofile.rnw”)

I was delighted with the result and probably will abandon the Sweave-direct option.  Thanks to Carl for dprint and Yihui for knitr.  If you do not see the embedded pdf below, please get directly through [https://www.box.com/s/416b473f6c92c581e343](https://www.box.com/s/416b473f6c92c581e343 "https://www.box.com/s/416b473f6c92c581e343"). <embed src="https://www.box.com/embed/sh30hjuz4cmypu3.swf" wmode="opaque" type="application/x-shockwave-flash" allowfullscreen="true" allowscriptaccess="always">

[R code from GIST:](https://gist.github.com/2777021)