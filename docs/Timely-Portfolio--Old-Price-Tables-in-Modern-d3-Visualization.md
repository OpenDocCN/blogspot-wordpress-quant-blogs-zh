<!--yml

类别：未分类

日期：2024-05-18 15:00:36

-->

# 及时投资组合：现代 d3 可视化中的旧价格表格

> 来源：[`timelyportfolio.blogspot.com/2013/04/old-price-tables-in-modern-d3.html#0001-01-01`](http://timelyportfolio.blogspot.com/2013/04/old-price-tables-in-modern-d3.html#0001-01-01)

在我的文章[从谷歌书架上拂去 130 年前的黄金书籍尘埃](http://timelyportfolio.blogspot.com/2013/03/dust-off-130-year-old-gold-books-on.html)中，我使用了**latticeExtra xyplot**重现了[詹姆斯·劳伦斯·劳克林](http://books.google.com/books?id=UFMuAAAAYAAJ&printsec=frontcover#v=thumbnail&q&f=false)所著的[1873 年以来的黄金与价格](http://books.google.com/books?id=UFMuAAAAYAAJ&printsec=frontcover#v=thumbnail&q&f=false)附录中的某些旧且已超出版权保护的价格表格。现在，借助我上一篇文章中构建的[**clickme**](https://github.com/nachocab/clickme)多行[d3](http://d3js.org)ractive，我们可以轻松地将这些数据转换成交互式的时间序列线图。

我试图将[多行 ractive](https://github.com/timelyportfolio/clickme_multiline_generic/)泛化，以创建来自[R](http://r-project.org)的 xts 对象的几乎任何线图。查看[提交历史](https://github.com/timelyportfolio/clickme_multiline_generic/commits/)，了解我对[原始 ractive](https://github.com/timelyportfolio/clickme_multiline)所做的少量修改：

1.  采用给定的数据而不是转换为累积线

1.  允许为标题和 x 轴位置设置参数

1.  处理起始日期和结束日期不同的数据系列

我们可以使用几行 R 代码和[**clickme**](https://github.com/nachocab/clickme)构建 html 文件。

```
# if not already installed, uncomment the two lines below
# library(devtools) install_github('clickme', 'nachocab')

require(clickme)
# set location where you put your multiline ractive
set_root_path("path to your ractive/r") 
```

```
clickme(data = priceTables["1850::", c(-1, -6, -8, -11, -12)], ractive = "clickme_multiline_generic", 
    params = list(title = "Price Tables from <em> Gold and Prices Since 1873 </em>", 
        x_axis_location = 100)) 
```

我没有看到传递参数的示例，所以我用标题和 x_axis_location 作为测试，看看**clickme**如何处理参数。如果我看源代码正确的话，template_config.yml 指定了允许的参数。然后，可以通过作为 params 提供给**clickme**函数的列表来指定这些参数，如上面所示。

```
...
default_parameters: {
  width: 960,
  height: 500,
  title,
  x_axis_location
}
... 
```
