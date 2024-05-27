<!--yml

类别：未分类

date: 2024-05-18 14:35:31

-->

# TFX Package | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/12/06/tfx-package/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/12/06/tfx-package/#0001-01-01)

## TFX Package

今天我想突出一下由 Garrett See 创建的[TFX Package](http://cran.r-project.org/web/packages/TFX/index.html)。TFX 是 R 语言的一个接口，用于访问 TrueFX(tm) Web API，可以免费流式传输实时的和历史的高精度逐笔市场数据，这些数据是可交易的银行间外汇汇率，具有毫秒级的细节。

Garrett 提供了一个很棒的教程和一个闪亮的 TFX 应用程序示例，请访问[`rpubs.com/gsee/TFX`](http://rpubs.com/gsee/TFX)

请注意，运行[TFX](http://cran.r-project.org/web/packages/TFX/index.html)需要 R 版本大于等于 2.15.0。入门非常简单。首先安装所需的包：

```
# TFX : R (>= 2.15.0)
install.packages(c('XML','bitops','TFX','shiny'), repos = 'http://cran.r-project.org', dependencies = 'Imports')

```

Next, let run a shiny example of TFX provided by Garrett:

```
# http://cran.r-project.org/web/packages/TFX/index.html
# http://rpubs.com/gsee/TFX
# https://gist.github.com/4122626
library('shiny')

runGist('4122626')

```

最后，要在 R 会话中访问外汇报价：

```
library(TFX)

QueryTrueFX()

```
