<!--yml

分类：未分类

日期：2024-05-18 14:59:53

-->

# 及时组合：使用 R 语言 lattice 制作的更多 JGB 收益率图表

> 来源：[`timelyportfolio.blogspot.com/2013/05/even-more-jgb-yield-charts-with-r.html#0001-01-01`](http://timelyportfolio.blogspot.com/2013/05/even-more-jgb-yield-charts-with-r.html#0001-01-01)

详细内容请查看上一贴。我就是忍不住再创作几幅。

### 最爱图表之变体——按到期期限绘制的 JGB 收益率时间序列线条图

```
p2 <- xyplot(value ~ date | indexname, data = jgb.melt, 
    type = "l", layout = c(length(unique(jgb.melt$indexname)), 
        1), panel = function(x, y, ...) {
        panel.abline(h = c(min(y), max(y)))
        panel.xyplot(x = x, y = y, ...)
        panel.text(x = x[length(x)/2], y = max(y), 
            labels = levels(jgb.melt$indexname)[panel.number()], 
            cex = 0.7, pos = 3)
    }, scales = list(x = list(tck = c(1, 0), alternating = 1), 
        y = list(tck = c(1, 0), lwd = c(0, 1))), strip = FALSE, 
    par.settings = list(axis.line = list(col = 0)), 
    xlab = NULL, ylab = "Yield", main = "JGB Yields by Maturity Since Jan 2012")
p2 <- p2 + layer(panel.abline(h = pretty(jgb.melt$value), 
    lty = 3))
p2 
```

```
 jgb.xts.diff <- jgb.xts["2012::", ] - matrix(rep(jgb.xts["2012::", 
    ][1, ], NROW(jgb.xts["2012::", ])), ncol = NCOL(jgb.xts), 
    byrow = TRUE)
jgb.diff.melt <- xtsMelt(jgb.xts.diff)
jgb.diff.melt$date <- as.Date(jgb.diff.melt$date)
jgb.diff.melt$value <- as.numeric(jgb.diff.melt$value)
jgb.diff.melt$indexname <- factor(jgb.diff.melt$indexname, 
    levels = colnames(jgb.xts))

p4 <- xyplot(value ~ date | indexname, data = jgb.diff.melt, 
    type = "h")

update(p2, ylim = c(min(jgb.diff.melt$value), max(jgb.melt$value) + 
    0.5)) + p4 
```

```
 update(p2, ylim = c(min(jgb.diff.melt$value), max(jgb.melt$value) + 
    0.5), par.settings = list(axis.line = list(col = "gray70"))) + 
    update(p4, panel = function(x, y, col, ...) {
        # do color scale from red(negative) to
        # blue(positive)
        cc.palette <- colorRampPalette(c(brewer.pal("Reds", 
            n = 9)[7], "white", brewer.pal("Blues", 
            n = 9)[7]))
        cc.levpalette <- cc.palette(20)
        cc.levels <- level.colors(y, at = do.breaks(c(-0.3, 
            0.3), 20), col.regions = cc.levpalette)
        panel.xyplot(x = x, y = y, col = cc.levels, 
            ...)
    }) 
```

```
 p5 <- horizonplot(value ~ date | indexname, data = jgb.diff.melt, 
    layout = c(1, length(unique(jgb.diff.melt$indexname))), 
    scales = list(x = list(tck = c(1, 0))), xlab = NULL, 
    ylab = NULL)

p5 
```

```
 update(p2, ylim = c(0, max(jgb.melt$value) + 0.5), 
    panel = panel.xyplot) + p5 + update(p2, ylim = c(0, 
    max(jgb.melt$value))) 
```

### 收益率曲线演变之透明度颜色刻度变化

```
# add alpha to colors
addalpha <- function(alpha = 180, cols) {
    rgbcomp <- col2rgb(cols)
    rgbcomp[4] <- alpha
    return(rgb(rgbcomp[1], rgbcomp[2], rgbcomp[3], 
        rgbcomp[4], maxColorValue = 255))
}

p3 <- xyplot(value ~ indexname, group = date, data = jgb.melt, 
    type = "l", lwd = 2, col = sapply(400/(as.numeric(Sys.Date() - 
        jgb.melt$date) + 1), FUN = addalpha, cols = brewer.pal("Blues", 
        n = 9)[7]), main = "JGB Yield Curve Evolution Since Jan 2012")

p3 <- update(asTheEconomist(p3), scales = list(x = list(cex = 0.7))) + 
    layer(panel.text(x = length(levels(jgb.melt$indexname)), 
        y = 0.15, label = "source: Japanese Ministry of Finance", 
        col = "gray70", font = 3, cex = 0.8, adj = 1))

# make point rather than line
update(p3, type = "p") 
```

```
 # make point with just most current curve as line
update(p3, type = "p") + xyplot(value ~ indexname, 
    data = jgb.melt[which(jgb.melt$date == max(jgb.melt$date)), 
        ], type = "l", col = brewer.pal("Blues", n = 9)[7]) 
```
