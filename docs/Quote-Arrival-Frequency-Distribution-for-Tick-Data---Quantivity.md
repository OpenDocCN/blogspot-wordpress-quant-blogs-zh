-   <!--yml

-   分类：未分类

-   date: 2024-05-18 13:55:13

-   -->

# -   Quote Arrival Frequency Distribution for Tick Data | Quantivity

> -   来源：[`quantivity.wordpress.com/2009/12/27/quote-arrival-frequency-distribution-for-tick-data/#0001-01-01`](https://quantivity.wordpress.com/2009/12/27/quote-arrival-frequency-distribution-for-tick-data/#0001-01-01)

-   高频系统开发是基于成交量数据的分析。一个经典例子是统计日内报价的频率和到达时间，这对于构建利用[市场微观结构](http://en.wikipedia.org/wiki/Market_microstructure)效应的系统很有用。

-   然而，此类分析的时间规律性与传统的定量分析有根本的不同：成交量以不规则的时间间隔到达（甚至在同一时间到达多个），时间间隔从零到几秒（甚至几分钟）。成交量的非规律时间到达与经典统计时间序列方法的规律时间假设以及相应的计算工具相冲突。

-   最近的研究证实了这一挑战。

-   考虑为单一货币工具生成报价到达频率分布，例如存储在标准 CSV 文件中的 EURUSD，以下为文件格式（带标题行）：

-   `pair,date,bid,ask

-   EURUSD,2009-01-26 00:00:11.000,1.294500,1.294800`

-   考虑到 2009 年 1 月 26 日所有这些不规则间隔的报价，通过小时和分钟计算时间频率分布。结果在 R 中比天真预期的要难得多。任何有 R 专业知识的读者，建议欢迎改进下面的代码（承认不是最漂亮的）。

-   假设已经加载了一个名为*data*的数据框，其中包含了所有的上述成交量数据。首先，解析日期，假设一个非标准格式，生成一个按顺序的*数值*时间戳向量，测量的是自纪元以来的秒数。

`datesNum <- as.numeric(as.POSIXct(strptime(as.character(data$date), "%Y-%m-%d %H:%M:%OS")))`

-   接下来，将时间戳截断为零基，并转换为所需的时间单位（除以 60 转为分钟，360 转为小时）：

-   `datesNum <- datesNum - min(datesNum)

-   `datesNum <- datesNum / 60`

-   现在迎来了 R 的魔法，通过将报价到达时间戳转换为数值变为可能：

-   `plot(cbind(table(cut(datesNum, seq(min(datesNum), max(datesNum), by=1), right=FALSE))), type="l", xlab="Minutes", ylab="Quote Frequency")`

-   这个表达式需要稍微展开一下，看看它是如何组合在一起的（更多详细解释，请参见[r-tutor](http://www.r-tutor.com/elementary-statistics/quantitative-data/frequency-distribution-quantitative-data)）：

+   -   范围：计算时间戳的范围，如`min()`和`max()`返回的值

+   -   子区间划分：通过定义一个等距序列的断点，将范围划分为非重叠的子区间，使用`seq()`

+   分类：使用`cut()`函数，根据子时间间隔（左闭右开）对每个时间戳进行分类。

+   频率：通过`table()`函数计算每个子时间间隔内时间戳的频率。

+   列绑定：通过`cbind()`将子时间间隔和频率列绑定在一起。

考虑到这一点，`plot()`函数生成一个简单的折线图，其 x 轴是子时间间隔的单位值（*即*分钟或小时），y 轴是在该时间间隔内到达的报价的频率。

对于那些进行高频分析的人，适合于非等间距方法的 R 包包括[zoo](http://cran.r-project.org/web/packages/zoo/index.html)、[xts](http://cran.r-project.org/web/packages/xts/index.html)、[its](http://cran.r-project.org/web/packages/its/index.html)、[tseries](http://cran.r-project.org/web/packages/tseries/index.html)和[fts](http://cran.r-project.org/web/packages/fts/index.html)。
