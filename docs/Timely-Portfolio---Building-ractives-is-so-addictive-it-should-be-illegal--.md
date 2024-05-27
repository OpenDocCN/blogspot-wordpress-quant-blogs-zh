<!--yml

类别：未分类

日期：2024-05-18 15:00:40

-->

# 及时组合：“构建 ractives 如此令人上瘾，它应该被禁止！”

> 来源：[`timelyportfolio.blogspot.com/2013/03/building-ractives-is-so-addictive-it.html#0001-01-01`](http://timelyportfolio.blogspot.com/2013/03/building-ractives-is-so-addictive-it.html#0001-01-01)

这是一个非常棒的 R 包。[clickme](https://github.com/nachocab/clickme)。当我第一次看到[Nacho Caballero](https://twitter.com/nachocaballero)的声明时，我并不确定会看到什么。实际上，我既怀疑又害怕，但这两种反应都是没有根据的。示例证明了它的力量，而[他的 wiki 教程](https://github.com/nachocab/clickme/wiki/_pages)减轻了新手的困难。clickme 与 shiny 非常相似，它作为 html、javascript（尤其是[d3](http://d3.js.org)）和 R 的集成点。虽然 clickme 不支持 shiny 的 R websocket 交互性，但它更专注于快速可复现性和共享，使其成为一个非常有用的工具。这与[可复用图表](http://dexvis.wordpress.com/2013/03/27/reusable-charts-part-6-parallel-coordinates/)的精神非常相似。**ractives** [定义](https://github.com/nachocab/clickme/wiki)如下：

> （简称 interactives-向 Neal Stephenson 致敬），这是一个包含用于用 R 输入数据填充 JS 代码的模板文件的简单文件夹结构

为 clickme 提供结构以从

1.  一个 R markdown 模板（template.rmd）

1.  一个转换器 R 脚本（translator.r）

1.  数据源

1.  外部脚本（可能是 javascript）和样式（.css）。

受到[clickme 纵向热图示例](http://bl.ocks.org/timelyportfolio/raw/5225228/)的启发，我忍不住尝试创建自己的 ractive。我认为[Mike Bostock 的线图示例](http://bl.ocks.org/mbostock/3902569)将作为我的第一个 ractive 的好模板。数据不出所料将来自 R 金融包**PerformanceAnalytics**数据集，名为**managers**。对 Bostock 源进行了非常小的修改，并编写了一个简单的自定义 R 脚本转换器（translator.R，如下所示），我们就有了这个 ractive 所需的一切，我将称其为 multiline。

```
#' Translate the data object to the format expected by current template

#'

#' @param data input data object

#' @param opts options of current template

#' @return The opts variable with the opts$data variable filled in

translate <- function(data, opts = NULL) {

    require(df2json)

    # I would like to generalize this to handle both price and return right

    # now just handles return clickme template.Rmd javascript can handle

    # prices or cumulative so we will send cumulative which can serve as price

    # remove na

    data[is.na(data)] <- 0

    # get cumulative growth

    data <- cumprod(1 + data)

    # convert to data frame

    data.df <- data.frame(cbind(format(index(data), "%Y-%m-%d"), coredata(data)))

    colnames(data.df)[1] = "date"

    # melt the data frame so we have our data in long form

    data.melt <- melt(data.df, id.vars = 1, stringsAsFactors = FALSE)

    colnames(data.melt) <- c("date", "indexname", "price")

    # remove periods from indexnames to prevent javascript confusion these .

    # usually come from spaces in the colnames when melted

    data.melt[, "indexname"] <- apply(matrix(data.melt[, "indexname"]), 2, gsub, 

        pattern = "[.]", replacement = "")

    opts$data <- df2json(data.melt)

    opts

} 
```

现在要创建我们的第一个 clickme html 页面，我们只需要在 R 中写几行代码。

```
# if not already installed, uncomment the tow lines below

# library(devtools) install_github('clickme', 'nachocab')

require(clickme)

# set location where you put your multiline ractive

set_root_path("your-path-goes-here/ractives") 
```

```
require(PerformanceAnalytics)

data(managers)  #although I use managers, really any xts series of returns will work

clickme(managers, "multiline") 
```

然后，我们将创建一个网页，该网页将使用累积增长**经理**回报系列的 d3 线图进行交互。如果您看不到下面的嵌入内容，请点击[这里](http://bl.ocks.org/timelyportfolio/5257985)跟进链接。

最终，拥有一个完整的一系列令人惊叹的 ractives 的画廊将是非常好的。
