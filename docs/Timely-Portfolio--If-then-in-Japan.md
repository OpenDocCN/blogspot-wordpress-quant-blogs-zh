<!--yml

类别：未分类

日期：2024-05-18 14:59:43

-->

# 及时投资组合：日本的如果…那么

> 来源：[`timelyportfolio.blogspot.com/2013/05/ifthen-in-japan.html#0001-01-01`](http://timelyportfolio.blogspot.com/2013/05/ifthen-in-japan.html#0001-01-01)

如果日本开始失控，他们该怎么办？失控的表现将是日本国债利率的突然上升和日元的同时崩溃。他们将通过外部干预来试图减缓正反馈循环。幸运的是，与美国的 1350 亿储备相比，日本积累了 1.2 万亿的显著储备地位，因此他们确实拥有些火力。

```
require(latticeExtra)
require(quantmod)

japanReserves <- getSymbols("TRESEGJPM052N", src = "FRED", 
    auto.assign = FALSE)
asTheEconomist(xyplot(japanReserves, scales = list(y = list(rot = 1)), 
    main = "Japan Foreign Reserves excluding Gold"))
```

基于**数据**

[美国财政部的数据](http://www.treasury.gov/resource-center/data-chart-center/tic/Pages/index.aspx)

日本 1.2 万亿的外汇储备中有 1.1 万亿是美国国债债券。如果日本决定（被迫）变现，他们唯一可以变现的就是美国国债债券。如果他们出售，谁会购买？接下来会发生什么？

```
# get data from US Treasury for top 10 foreign
# holders of US treasuries
foreignUSTreas <- read.csv("http://www.treasury.gov/resource-center/data-chart-center/tic/Documents/mfhhis01.csv", 
    skip = 4, nrows = 13, stringsAsFactors = FALSE)
top10 <- data.frame(foreignUSTreas[4:13, 1:2])
colnames(top10) <- c("Country", "Value")
top10$Value <- as.numeric(top10$Value)
top10$Country <- factor(top10$Country, levels = top10$Country[order(top10$Value)])

barchart(Country ~ Value, data = top10, origin = 0, 
    xlab = "Value (in $Billions)", main = "Foreign Holders of US Treasuries - Top 10", 
    scales = list(y = list(alternating = 3)), par.settings = theEconomist.theme(box = "transparent"), 
    lattice.options = theEconomist.opts())
```

**对于那些将美联储 H4 数据与美国财政部 TIC 数据进行比较的人，这是一个非常好的总结[`www.treasury.gov/resource-center/data-chart-center/tic/Pages/ticfaq2.aspx#q10`](http://www.treasury.gov/resource-center/data-chart-center/tic/Pages/ticfaq2.aspx#q10)。**
