<!--yml

类别：未分类

日期：2024 年 5 月 18 日 06:48:17

-->

# HOXO-M - 日本匿名数据分析团队 - ：WDI、dplyr 和 rMaps 打造的无缝分析环境

> 来源：[`mockquant.blogspot.com/2014/03/seamless-analytical-environment-by-wdi.html#0001-01-01`](http://mockquant.blogspot.com/2014/03/seamless-analytical-environment-by-wdi.html#0001-01-01)

最近我发现我的 R 领域大师[@ramnath_vaidya](https://twitter.com/ramnath_vaidya)正在开发一个新的可视化包[rMaps](https://github.com/ramnathv/rMaps)。

当我第一次看到它时，我感到非常兴奋，我认为在地图上绘制任何数据都非常棒。

让我解释一下我们如何

+   获取数据（WDI 包）

+   操作数据（dplyr 包）

+   用 rMaps 包可视化结果

用了很棒的 R 包。

除了 rMaps 包，你可以按照通常的方法从 CRAN 安装这些包（WDI、dplyr）。

```
install.packages(c("WDI", "dplyr")) 
```

要安装 rMaps 包，你只需要在 R 控制台上输入以下命令。

```
require(devtools)
install_github("ramnathv/rCharts@dev")
install_github("ramnathv/rMaps") 
```

（不要忘记安装“devtools”包以使用 install_github 函数。）

现在，举个例子，我给你展示

+   从世界银行用 WDI 包获取“二氧化碳排放（kt）”数据

+   通过 dplyr 包对其进行总结

+   通过 rMaps 包可视化

结果如下所示：

…尽情享用！！！

顺便说一句，最近一个日本的 R 专业人士经常发布他的优秀文章。如果你对可视化和 dplyr 特别感兴趣，我建议你看看这些文章。

源代码：

```
library(WDI)
library(rMaps)
library(dplyr)
library(countrycode)
# Get CO2 emission data from World bank
# Data source : http://data.worldbank.org/indicator/EN.ATM.CO2E.KT/
df <- WDI(country=c("all"), 
          indicator="EN.ATM.CO2E.KT", 
          start=2004, end=2013)
# Data manipulation By dplyr
data <- df %.% 
  na.omit() %.%
  #Add iso3c format country code 
  mutate(iso3c=countrycode(iso2c, "iso2c", "iso3c")) %.% 
  group_by(iso3c) %.%
  #Get the most recent CO2 emission data
  summarize(value=EN.ATM.CO2E.KT[which.max(year)])
# Visualize it by rMaps
i1 <- ichoropleth(value~iso3c, data, map="world")
i1$show("iframesrc", cdn = TRUE) # for blog post
#... or you can direct plot by just evaluating "i1" on R console. 
```
