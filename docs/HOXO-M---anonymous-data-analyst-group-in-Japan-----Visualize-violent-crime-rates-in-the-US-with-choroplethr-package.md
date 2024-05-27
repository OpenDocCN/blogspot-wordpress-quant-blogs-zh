<!--yml

分类：未分类

日期：2024 年 5 月 18 日 06:48:13

-->

# 霍克索 M - 日本匿名数据分析小组 - ：使用 choroplethr 包可视化美国的暴力犯罪率

> 来源：[`mockquant.blogspot.com/2014/04/visualize-violent-crime-rates-in-us.html#0001-01-01`](http://mockquant.blogspot.com/2014/04/visualize-violent-crime-rates-in-us.html#0001-01-01)

<title>使用 choroplethr 包在不同的美国州中可视化暴力犯罪率</title>

我已阅读

[choroplethr 包](http://cran.r-project.org/web/packages/choroplethr/index.html)

来自博客文章

[R 中的动态 Choropleths](http://blog.revolutionanalytics.com/2014/04/animated-choropleths-in-r.html)

几天前。作为 R 语言中的另一个可视化工具，我想尝试这一个。

要安装最新的稳定版本（CRAN），请在 R 控制台中输入以下内容：

```
install.packages("choroplethr") 
```

要安装从 github 使用 devtools 包的开发版本，请在 R 控制台中输入以下内容：

```
library(devtools)
install_github("choroplethr", "trulia")
library(choroplethr) 
```

我对仅运行在 choroplethr 包中编写的示例代码不感兴趣。相反，我使用了其他数据

[rMaps](https://github.com/ramnathv/rMaps)

作为快速数据源并进行可视化！

```
library(devtools)
install_github("ramnathv/rCharts@dev")
install_github("ramnathv/rMaps") 
```

现在我们可以使用

**美国的暴力犯罪率数据**

包括在 rMaps 包中。

我们可以创建

**动态 Choropleths**

如下页：

在我的案例中，我们仅处理数据并将其可视化为以下简单的代码：

```
# load packages
library(rMaps)
library(choroplethr)
# initialization list and get years from violent_crime data
choropleths = list()
# Get years for loop
years <- sort(unique(violent_crime$Year))
# convert to level data
violent_crime$Crime <- cut(violent_crime$Crime, 9)
# Create choropleth component.
for (i in 1:length(years)) {
    df <- subset(violent_crime, Year == years[i])
    # We need to change the column names for choroplethr function
    colnames(df) <- c("Year", "region", "value")
    # Cut decimal off df$value <- round(df$value)
    title <- paste0("Violent crime rates: ", years[i])
    choropleths[[i]] = choroplethr(df, "state", title = title)
}
# Vizualize it!
choroplethr_animate(choropleths) 
```

结果通过 Dropbox 发布如下（图像）链接

现在可以享用！
