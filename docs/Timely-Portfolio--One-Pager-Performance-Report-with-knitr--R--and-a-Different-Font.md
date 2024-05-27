<!--yml

类别：未分类

日期：2024-05-18 15:00:53

-->

# 及时投资组合：使用 knitr, R 和不同字体的性能报告单页

> 来源：[`timelyportfolio.blogspot.com/2013/03/one-pager-performance-report-with-knitr.html#0001-01-01`](http://timelyportfolio.blogspot.com/2013/03/one-pager-performance-report-with-knitr.html#0001-01-01)

虽然我对排版一无所知，但在[Hyndsight 博客](http://robjhyndman.com/hyndsight/xelatex/)和[mages 的博客](http://lamages.blogspot.com/2011/10/using-sweave-with-xelatex.html)的两篇博文的帮助下，我想尝试在我们用[Onepager Now with knitR](http://timelyportfolio.blogspot.com/2013/02/onepager-now-with-knitr.html)创建的性能报告上使用一种不同的字体。我认为[Open Sans Light](http://www.google.com/webfonts/specimen/Open+Sans)并不是这份报告的最佳选择，但既然这是谷歌上最受欢迎的字体，我想那些在排版上比我有更多知识的人也不会对我太过苛责。

> ```
> options(tikzDefaultEngine = "xetex")
> 
> require(knitr)
> 
> knit2pdf("onepager_text_graphics-knitr.rnw", compiler = "xelatex")
> 
> ```

结果（如果下面的嵌入式内容无法显示，请[点击此处](https://www.box.com/s/4nftk6qpa0cugapmncsn)）：

```html

[R 代码来自 GIST：](https://gist.github.com/timelyportfolio/5189615)
