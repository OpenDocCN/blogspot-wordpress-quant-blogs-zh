<!--yml

category: 未分类

日期：2024-05-18 14:35:22

-->

# XLLoop 示例 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/12/11/xlloop-examples/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/12/11/xlloop-examples/#0001-01-01)

今天我想跟进 XLLoop 框架帖子。在尝试以下示例之前，请先阅读 XLLoop 框架帖子以设置 [XLLoop](http://xlloop.sourceforge.net/)。

我的第一个示例基于 [TFX Package](https://systematicinvestor.wordpress.com/2012/12/06/tfx-package/) - 用于检索实时外汇报价。要尝试此示例，请首先安装 [TFX Package](http://cran.r-project.org/web/packages/TFX/index.html)。请注意，您需要 R（>= 2.15.0）来运行 [TFX](http://cran.r-project.org/web/packages/TFX/index.html)。

```

# TFX : R (>= 2.15.0)
install.packages(c('XML','bitops','TFX'), repos = 'http://cran.r-project.org', dependencies = 'Imports')

```

接下来，让我们创建一个函数来检索实时外汇报价。

```

# http://rpubs.com/gsee/TFX
# https://gist.github.com/4122626
getFX <- function() {
	require(TFX)
	qtf <- QueryTrueFX()
	qtf$TimeStamp <- as.character(qtf$TimeStamp)
	names(qtf)[6] <- "TimeStamp (GMT)"
	qtf[, c(6, 1:3, 5:4)]
}

```

最后，您需要将 getFX() 函数添加到 rstart.r 脚本中。为此，我创建了一个 user.r 文件来保存您希望在 Excel 中可用的所有用户函数，并将 source(“user.R”) 添加到 rstart.r 脚本以加载我们的函数。我已将 [xlloop-basic.zip](http://www.systematicportfolio.com/xlloop-basic.zip) 压缩包更新为此新功能。

目前您可以下载 [xlloop-basic.zip](http://www.systematicportfolio.com/xlloop-basic.zip) 压缩包，并按照 XLLoop 框架帖子中的步骤设置 [XLLoop](http://xlloop.sourceforge.net/)。接下来，使用 xlloop_TFX.xls 进行操作。

如果一切正常，您将看到以下 Excel 电子表格，每 3 秒更新一次。您可以通过单击“停止”/“启动”按钮停止/启动更新。您还可以通过在单元格 J5 中输入不同的数字来更改更新速度。

![plot1.png.small](https://systematicinvestor.wordpress.com/2012/12/11/xlloop-examples/plot1-png-small-67/)

今天我想分享的另一个示例将从 [BATS 交易所](http://www.batstrading.com/book/SPY/) 检索实时股票报价。请首先安装 [RJSONIO Package](http://cran.r-project.org/web/packages/RJSONIO/index.html)：

```

install.packages('RJSONIO', repos = 'http://cran.r-project.org', dependencies = 'Imports')

```

接下来，让我们创建一个函数来检索实时股票报价。

```

#=FS("bats.quote","IBM")
# http://www.batstrading.com/book/IBM/
bats.quote <- function(ticker) {
	require(RJSONIO)

	url = paste('http://www.batstrading.com/json/bzx/book/', ticker, sep = '')
	x = fromJSON(url)

	# create output
	out = matrix('', 15,6)
	out[1,2] = x$data$timestamp
	out[1,3] = x$data$symbol
	out[1,4] = x$data$company

	out[2,2] = 'Orders'
	out[2,5] = 'Volume'
	out[3,2] = x$data$orders
	out[3,5] = x$data$volume

	out[4,2] = 'Top of the Book'
	out[4,5] = paste('Last', length(x$data$trades), 'trades')

	out[5,] = c('','Shares','Price','Time','Shares','Price')

	out[6,1] = 'Asks'
	if(length(x$data$asks) > 0) out[6:10,2:3] = t(sapply(x$data$asks, unlist))
	out[11,1] = 'Bids'
	if(length(x$data$bids) > 0) out[11:15,2:3] = t(sapply(x$data$bids, unlist))

	if(length(x$data$trades) > 0) out[6:15,4:6] = t(sapply(x$data$trades, unlist))

	out
}

```

我已将 bats.quote() 添加到 [xlloop-basic.zip](http://www.systematicportfolio.com/xlloop-basic.zip) 压缩包中的 user.r 文件中以供此示例使用。接下来，使用 xlloop_BATS.xls 进行操作。

如果一切正常，您将看到以下 Excel 电子表格，每 3 秒更新一次。您可以通过单击“停止”/“启动”按钮停止/启动更新。您还可以通过在单元格 J5 中输入不同的数字来更改更新速度。您还可以通过在单元格 C2 中输入不同的股票代码来更改公司。

![plot2.png.small](https://systematicinvestor.wordpress.com/2012/12/11/xlloop-examples/plot2-png-small-64/)

请在尝试这些示例时告诉我您遇到的任何问题。

我注意到我的系统上的外汇报价更新频率不如我所期望的那样频繁。
