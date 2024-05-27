<!--yml

分类：未分类

日期：2024-05-18 14:33:31

-->

# 板块轮动回测 Shiny 网络应用 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2013/02/18/sector-rotation-back-test-shiny-web-application/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/02/18/sector-rotation-back-test-shiny-web-application/#0001-01-01)

[首页](https://systematicinvestor.wordpress.com/ "前往主页")

[R](https://systematicinvestor.wordpress.com/category/r/)

,

[Shiny](https://systematicinvestor.wordpress.com/category/shiny/)

> 板块轮动回测 Shiny 网络应用

## 板块轮动回测 Shiny 网络应用

今天，我想分享[板块轮动回测](http://glimmer.rstudio.com/systematicin/sector.rotation/)应用（代码在[GitHub](https://github.com/systematicinvestor/SIT/tree/master/Shiny/sector.rotation/)）。

这是系列示例中的最后一个应用（我已经分享了 5 个示例），将展示令人惊叹的[Shiny](http://www.rstudio.com/shiny/)框架和[系统投资者工具箱](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)，用于分析股票、进行回测和创建摘要报告。

这一系列文章的动机是展示如何以最小的努力，将你的回测脚本翻译成可以从 Shiny 服务器或你的个人电脑运行的实时网络应用。

请注意，回测应用更新图表/表格需要更长的时间，因此可能更适合从你的本地电脑运行。

例如，要从你的电脑运行[板块轮动](http://glimmer.rstudio.com/systematicin/one.stock/)应用，你首先需要安装[Shiny](http://www.rstudio.com/shiny/)。然后执行以下命令：

```
library(shiny)
runGitHub('SIT','systematicinvestor', subdir = 'Shiny/sector.rotation')

```
