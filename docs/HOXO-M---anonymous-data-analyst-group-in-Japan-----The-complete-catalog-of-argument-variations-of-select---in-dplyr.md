<!--yml

category: 未分类

日期: 2024-05-18 06:47:57

-->

# HOXO-M - 日本匿名数据分析师团队 -：dplyr 中 select()函数的完整参数目录

> 来源：[`mockquant.blogspot.com/2015/07/the-complete-catalog-of-argument.html#0001-01-01`](http://mockquant.blogspot.com/2015/07/the-complete-catalog-of-argument.html#0001-01-01)

当我阅读[dplyr 介绍文档](https://cran.rstudio.com/web/packages/dplyr/vignettes/introduction.html)时，我发现了一种便利的选择连续列的方式，比如`select(data, year:day)`。

因为我只向`select()`函数输入列名，所以深受这种便利方式的影响。

仔细观察后，我发现`select()`函数接受多种类型的输入。

这里，我将列举`select()`函数的可接受输入的各种类型。

顺便一提，这些列选择方法也可以在**tidyr**包中的一些函数（例如`gather()`）以及`summarise_each()`、`mutate_each()`中使用。

## 1\. 全部代码。

首先，为了明晰起见，展示了全部代码。

在下面的章节中，展示了每个命令的细节。

```
# Data preparation ------------------------------------------------------------------
library(dplyr)
library(nycflights13)
set.seed(123)
data 
```

## 2\. 数据准备。

要按照[dplyr 介绍文档](https://cran.rstudio.com/web/packages/dplyr/vignettes/introduction.html)，我们以**nycflights13**包中的`flights`数据集作为示例。

```
library(dplyr)
library(nycflights13)

set.seed(123)
data 
```

```
Variables:
$ year      (int) 2013, 2013, 2013
$ month     (int) 12, 7, 3
$ day       (int) 15, 17, 2
$ dep_time  (int) 2124, 651, 1636
$ dep_delay (dbl) -4, -9, 1
$ arr_time  (int) 2322, 936, 1800
$ arr_delay (dbl) 1, -28, 0
$ carrier   (chr) "UA", "DL", "WN"
$ tailnum   (chr) "N801UA", "N194DN", "N475WN"
$ flight    (int) 289, 763, 1501
$ origin    (chr) "EWR", "JFK", "LGA"
$ dest      (chr) "DTW", "LAX", "MKE"
$ air_time  (dbl) 88, 306, 103
$ distance  (dbl) 488, 2475, 738
$ hour      (dbl) 21, 6, 16
$ minute    (dbl) 24, 51, 36

```

这个数据集包括上面展示的 16 列。

## 3\. select()的基本使用方法。

首先，展示了使用`select()`的方式。

```
select(data, year) 
```

```
  year
1 2013
2 2013
3 2013

```

这个过程展示了将`year`列从数据中取出的方法。要选择多个列，可以写以下内容。

```
select(data, year, month, day) 
```

```
  year month day
1 2013    12  15
2 2013     7  17
3 2013     3   2

```

如果在数据集中列是连续的，你可以写以下内容来选择连续的列。

```
select(data, year:day) 
```

```
  year month day
1 2013    12  15
2 2013     7  17
3 2013     3   2

```

如果你想要去除特定的列，可以在列名前添加`-`，如下所示。

```
select(data, -year, -month, -day) 
```

```
  dep_time dep_delay arr_time arr_delay carrier tailnum flight origin dest air_time distance hour minute
1     2124        -4     2322         1      UA  N801UA    289    EWR  DTW       88      488   21     24
2      651        -9      936       -28      DL  N194DN    763    JFK  LAX      306     2475    6     51
3     1636         1     1800         0      WN  N475WN   1501    LGA  MKE      103      738   16     36

```

要去除连续的列，将连续的列放在用冒号连接的括号`()`中。

```
select(data, -(year:day)) 
```

```
  dep_time dep_delay arr_time arr_delay carrier tailnum flight origin dest air_time distance hour minute
1     2124        -4     2322         1      UA  N801UA    289    EWR  DTW       88      488   21     24
2      651        -9      936       -28      DL  N194DN    763    JFK  LAX      306     2475    6     51
3     1636         1     1800         0      WN  N475WN   1501    LGA  MKE      103      738   16     36

```

也可以通过选择列号选取列。

```
select(data, 1, 2, 3)
select(data, 1:3) 
```

```
  year month day
1 2013    12  15
2 2013     7  17
3 2013     3   2

```

下一主题稍微有些深入。

可以暂时选出连续的列并去除其中的一部分。

```
select(data, year:day, -month) 
```

```
  year day
1 2013  15
2 2013  17
3 2013   2

```

也可以去除连续的列然后保留其中的一部分。

```
select(data, -(year:day), month) 
```

```
  dep_time dep_delay arr_time arr_delay carrier tailnum flight origin dest air_time distance hour minute month
1     2124        -4     2322         1      UA  N801UA    289    EWR  DTW       88      488   21     24    12
2      651        -9      936       -28      DL  N194DN    763    JFK  LAX      306     2475    6     51     7
3     1636         1     1800         0      WN  N475WN   1501    LGA  MKE      103      738   16     36     3

```

即使使用列编号，也可以用列名得到相同的结果。（结果已被省略。）

```
select(data, 1:3, -2)
select(data, -(1:3), 2) 
```

## 4\. select()的实用函数。

`select()`、`summarise_each()`和`mutate_each()`中存在的实用函数，以及**tidyr**包中的一些函数。

`select()`的实用函数中存在七种函数。

+   `starts_with(match, ignore.case = TRUE)`

+   `ends_with(match, ignore.case = TRUE)`

+   `contains(match, ignore.case = TRUE)`

+   `matches(match, ignore.case = TRUE)`

+   `num_range(prefix, range, width = NULL)`

+   `one_of(...)`

+   `everything()`

现在我们来检查各个命令及其使用方法。

首先，`starts_with()`选择以指定字符串开头的列。

```
select(data, starts_with("arr")) 
```

```
  arr_time arr_delay
1     2322         1
2      936       -28
3     1800         0

```

参数`ignore.case`指定小写字母是否被分类为大写字母（默认为`TRUE`）。

`ends_with()`选择以指定字符串结尾的列。

```
select(data, ends_with("time")) 
```

```
  dep_time arr_time air_time
1     2124     2322       88
2      651      936      306
3     1636     1800      103

```

`contains()`选择包含指定字符串的列。

```
select(data, contains("_")) 
```

```
  dep_time dep_delay arr_time arr_delay air_time
1     2124        -4     2322         1       88
2      651        -9      936       -28      306
3     1636         1     1800         0      103

```

`matches()`基于正则表达式匹配的字符串选择列。

```
select(data, contains("_")) 
```

```
  dep_time dep_delay arr_time arr_delay air_time
1     2124        -4     2322         1       88
2      651        -9      936       -28      306
3     1636         1     1800         0      103

```

当列名中包含数字时，`num_range()`可能会很有用。

在本例中，我们将列名称更改为`x1`-`x16`，并对数据集执行`num_range()`命令。

```
data2 
```

```
  x8     x9  x10 x11
1 UA N801UA  289 EWR
2 DL N194DN  763 JFK
3 WN N475WN 1501 LGA

```

通过`num_range("x", 8:11)`指定，可以识别出`x8`到`x11`列。

列名中的数字不一定是连续的。

```
select(data2, num_range("x", c(9, 11))) 
```

```
      x9 x11
1 N801UA EWR
2 N194DN JFK
3 N475WN LGA

```

当列名被填充时，列名会显示为`x01`。

在这里，`num_range()`中的`width`参数可能很有用。

现在我们尝试用列名称更改为`x01`-`x16`的数据进行这个过程。

```
data3 
```

```
  x08    x09  x10 x11
1  UA N801UA  289 EWR
2  DL N194DN  763 JFK
3  WN N475WN 1501 LGA

```

通过指定`width=2`，可以选择出填充为零的列。

当列名被命名为向量或字符字符串时，`one_of()`可能会有用。

在以下情况下，使用`select()`会出现错误。

```
col_vector 
```

```
Error: All select() inputs must resolve to integer column positions.
The following do not:
*  col_vector

```

但是，在使用`one_of()`时会出现意外情况。

```
select(data, one_of(col_vector)) 
```

```
  year month day
1 2013    12  15
2 2013     7  17
3 2013     3   2

```

`everything()`选择所有列。（结果被省略）

```
select(data, everything()) 
```

如果在实用函数名字开头加上`-`，我们可以选择除实用函数指定区域外的所有内容。

```
select(data, -starts_with("arr")) 
```

```
  year month day dep_time dep_delay carrier tailnum flight origin dest air_time distance hour minute
1 2013    12  15     2124        -4      UA  N801UA    289    EWR  DTW       88      488   21     24
2 2013     7  17      651        -9      DL  N194DN    763    JFK  LAX      306     2475    6     51
3 2013     3   2     1636         1      WN  N475WN   1501    LGA  MKE      103      738   16     36

```

## 5\. 标准评估。

到目前为止，我们解释了一般的`select()`函数；但是，一般的`select()`函数无法处理字符字符串作为参数。

当例如将列名给定为字符串向量时，这可能会成为一个问题。

为了解决这个问题，**dplyr**中装备了`select_()`函数。（注意：在函数名中添加了下划线。）

`select_()`函数的使用方式与`select()`相同，只是通过字符串指定列；但是，在通过向量指定列名时需要注意。

```
select_(data, "year", "month", "day") 
```

```
  year month day
1 2013    12  15
2 2013     7  17
3 2013     3   2

```

当通过向量指定列名时，应该给向量提供`.dot`参数。

```
col_vector 
```

```
  year month day
1 2013    12  15
2 2013     7  17
3 2013     3   2

```

所有能够使用`select()`函数的参数也都可以成为`select_()`函数的潜在候选。

```
select_(data, 'year:day')
select_(data, 'year:day', '-month')
select_(data, '-(year:day)')
select_(data, 'starts_with("arr")')
select_(data, '-ends_with("time")') 
```

此外，即使在这种情况下，也应该在`select_()`函数中给参数向量提供`.dot`参数。

```
select_(data, .dots = c('starts_with("arr")', '-ends_with("time")')) 
```

## 6\. 参考资料。

dplyr 介绍

[`cran.rstudio.com/web/packages/dplyr/vignettes/introduction.html`](https://cran.rstudio.com/web/packages/dplyr/vignettes/introduction.html)

`select()`函数的帮助页面

`> help("select", package = "dplyr")`

原始日语输入者为 hoxo_m

[`qiita.com/hoxo_m/items/f2f1793c6f086d381340`](https://qiita.com/hoxo_m/items/f2f1793c6f086d381340)

译者：siero
