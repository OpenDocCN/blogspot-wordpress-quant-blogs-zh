<!--yml

类别：未分类

date: 2024-05-18 15:06:51

-->

# Timely Portfolio: knitR 性能报告 3（真正使用 knitr）和 dprint

> 来源：[`timelyportfolio.blogspot.com/2012/05/knitr-performance-report-3-really-with.html#0001-01-01`](http://timelyportfolio.blogspot.com/2012/05/knitr-performance-report-3-really-with.html#0001-01-01)

*请参阅[knitr 性能报告–尝试 3](http://timelyportfolio.blogspot.com/2012/05/knitr-performance-reportattempt-3.html)，[knitr 性能报告–尝试 2](http://timelyportfolio.blogspot.com/2012/04/knitr-performance-report-attempt-2.html)和[knitr 性能报告–尝试 1](http://timelyportfolio.blogspot.com/2012/04/knitr-performance-report-attempt-1.html)*

[alstated](http://yihui.name/knitr/options "http://yihui.name/knitr/options")在他的[knitr 性能报告–尝试 3](http://timelyportfolio.blogspot.com/2012/05/knitr-performance-reportattempt-3.html)评论中提出一个非常好的问题，我敢肯定在我忍受 Sweave 的挫折之前无法回答得很好。实际上，在那份报告中我没有使用 knitr，并且我处理了许多 knitr 要解决的问题。knitr 的强大之处在于它通过额外的 chunk 选项来控制输出的能力，这些选项在[`yihui.name/knitr/options`](http://yihui.name/knitr/options "http://yihui.name/knitr/options")中有描述，所以不再需要宽、textblock 等 LaTeX 命令。

一个非常著名的 R 金融贡献者还提醒我注意 Carl Brickner 在[`r-forge.r-project.org/projects/tabular/`](https://r-forge.r-project.org/projects/tabular/)提供的 dprint（请注意是 pre-Alpha 版本）包，在[userR! 2010](http://user2010.org/slides/Brickner+Slavov+Napoli.pdf)和其它地方展示过。要使用，您必须使用命令手动安装：

> install.packages("dprint", repos="[`R-Forge.R-project.org`](http://R-Forge.R-project.org)")

要生成最终的 pdf，请使用 knitr 的 knit2pdf 命令：

> knit2pdf("pathtofile.rnw")

我对结果非常满意，可能将放弃 Sweave 直接选项。感谢 Carl 提供 dprint 和 Yihui 提供 knitr。如果您看不到下面的内嵌 pdf，请直接通过[`www.box.com/s/416b473f6c92c581e343`](https://www.box.com/s/416b473f6c92c581e343 "https://www.box.com/s/416b473f6c92c581e343")获取。<embed src="https://www.box.com/embed/sh30hjuz4cmypu3.swf" wmode="opaque" type="application/x-shockwave-flash" allowfullscreen="true" allowscriptaccess="always">

[R 代码来自 GIST：](https://gist.github.com/2777021)
