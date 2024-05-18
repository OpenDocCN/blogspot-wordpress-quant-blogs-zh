<!--yml
category: 未分类
date: 2024-05-18 14:59:43
-->

# Timely Portfolio: If…then in Japan

> 来源：[http://timelyportfolio.blogspot.com/2013/05/ifthen-in-japan.html#0001-01-01](http://timelyportfolio.blogspot.com/2013/05/ifthen-in-japan.html#0001-01-01)

If Japan starts to spiral out of control, then what do they do? A spiral would be a sudden move higher in JGB rates with a simultaneous crash in the Japanese Yen. Their response would be to try to slow the positive feedback loop through external intervention. Fortunately for Japan, they have amassed a significant reserve position of 1.2 trillion compared to a US reserve position of 135 billion, so they do have some firepower.

```
require(latticeExtra)
require(quantmod)

japanReserves <- getSymbols("TRESEGJPM052N", src = "FRED", 
    auto.assign = FALSE)
asTheEconomist(xyplot(japanReserves, scales = list(y = list(rot = 1)), 
    main = "Japan Foreign Reserves excluding Gold"))
```

Based on

[data from the US Treasury](http://www.treasury.gov/resource-center/data-chart-center/tic/Pages/index.aspx)

, 1.1 trillion of the 1.2 trillion of Japanese foreign reserves are US Treasury bonds. If Japan decides (is forced) to liquidate, the only thing they have to liquidate are US Treasury bonds. Who will buy if they sell? What happens next?

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

*For those comparing the Federal Reserve H4 data to the US Treasury TIC data, this is a very good summary [http://www.treasury.gov/resource-center/data-chart-center/tic/Pages/ticfaq2.aspx#q10](http://www.treasury.gov/resource-center/data-chart-center/tic/Pages/ticfaq2.aspx#q10).*