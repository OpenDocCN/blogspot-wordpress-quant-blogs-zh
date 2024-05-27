<!--yml

类别：未分类

日期：2024 年 05 月 18 日 06:47:33

-->

# HOXO-M - 匿名日本数据分析小组 - ：新的 R 包 magicfor - 用于在 R 中通过 for 循环获得结果的魔法函数

> 来源：[`mockquant.blogspot.com/2016/12/new-r-package-magicfor-magic-functions.html#0001-01-01`](http://mockquant.blogspot.com/2016/12/new-r-package-magicfor-magic-functions.html#0001-01-01)

R 中 for 循环的不便之处是什么？那就是您得到的结果会消失。因此，我们创建了一个包来自动存储结果。要做到这一点，您只需要施展一行咒语`magic_for()`。在本文中，我们将告诉您如何使用这种魔法。

## 1\. 概述

`for()` 是 R 中最流行的函数之一。如您所知，它用于创建循环。

例如，让我们计算 1 到 3 的平方值。

```
for (i in 1:3) {
  squared <- i ^ 2
  print(squared)
}
#> [1] 1
#> [1] 4
#> [1] 9
```

这非常容易。

但是，将这些代码改成存储打印结果就会变得太麻烦。您必须准备一些具有正确长度的容器来存储结果，并将`print()`更改为赋值语句。

```
result <- vector("numeric", 3) # prepare a container
for (i in 1:3) {
  squared <- i ^ 2
  result[i] <- squared         # change to assignment
}
result
#> [1] 1 4 9
```

此外，您可能希望在数据框中以迭代编号存储结果。

```
result <- data.frame(matrix(nrow = 3, ncol = 2))
colnames(result) <- c("i", "squared")
for (i in 1:3) {
  squared <- i ^ 2
  result[i, 1] <- i
  result[i, 2] <- squared
}
result
#>   i squared
#> 1 1       1
#> 2 2       4
#> 3 3       9
```

真是麻烦！

在像您必须存储许多变量的这样或更麻烦的情况下，代码将变得更加复杂。

**magicfor** 包使得保持可读性的问题得到解决。

在 for 循环之前只需添加两行。首先，加载库。第二，调用`magic_for()`。请注意，主 for 循环保持不变。

```
library(magicfor)  # Load library
magic_for(print)   # Call magic_for()

for (i in 1:3) {
  squared <- i ^ 2
  print(squared)
}
#> The loop is magicalized with print().
#> [1] 1
#> [1] 4
#> [1] 9
```

`magic_for()`接受函数名，并重新构造`for()`以记住在 for 循环中传递给指定函数的值。我们称之为*魔法化*。一旦调用`magic_for()`，就像通常一样执行`for()`，结果将自动存储在内存中。

在这里，让我们使用`magic_result_as_vector()`来访问存储的值。

```
magic_result_as_vector()  # Get the result
#> [1] 1 4 9
```

这是从*魔法化的 for 循环*获取结果的函数之一，意味着以向量的形式取出结果。

即使观察变量数量增加，您也可以以相同的方式完成。

```
magic_for(silent = TRUE)

for (i in 1:3) {
  squared <- i ^ 2
  cubed <- i ^ 3
  put(squared, cubed)
}

magic_result_as_dataframe()
#>   i squared cubed
#> 1 1       1     1
#> 2 2       4     8
#> 3 3       9    27
```

`put()`是在魔法化的 for 循环中存储值的默认函数。它允许接受任意数量的变量，并且可以显示它们。

## 2\. 安装

您可以从 CRAN 安装**magicfor** 包。

```
install.packages("magicfor")
```

**magicfor** 包的源代码可在 GitHub 上找到

## 3\. 详细信息

**magicfor** 包提供以下函数：

+   `magic_for()`: 魔法化 for。

+   `magic_free()`: 取消魔法化。

+   获取结果：

    +   `magic_result()`: 作为列表。

    +   `magic_result_as_vetor()`: 作为向量。

    +   `magic_result_as_dataframe()`: 作为数据框。

+   `put()`: 显示值。

在下文中，我们假设已加载库以使用这些函数。

```
library(magicfor)
```

### 3.1 基础知识

主函数`magic_for()`将 for 循环进行魔法化。 *魔法化* 意味着更改`for()`的行为以存储通过目标函数输出的值。

```
magic_for()

for (i in 1:3) {
  squared <- i ^ 2
  put(squared)
}
#> The loop is magicalized with put().
#> squared: 1
#> squared: 4
#> squared: 9
```

默认的目标函数是`put()`。它显示输入值，例如：

```
x <- 1
put(x)
#> x: 1
```

当 for 循环完成时，您可以使用`magic_result_**()`取出存储的值。

```
magic_result_as_vector()
#> [1] 1 4 9
```

### 3.2 `magic_for()`

`magic_for()`有几个选项。

指定第一个参数`func`，你可以更改目标函数。

```
magic_for(cat)

for (i in 1:3) {
  squared <- i ^ 2
  cat(squared, " ")
}
#> The loop is magicalized with cat().
#> 1  4  9
```

如果`progress = TRUE`，显示进度条。

```
magic_for(progress = TRUE)

for (i in 1:3) {
  squared <- i ^ 2
  put(squared)
}
```

```
#> |=================================================================| 100%
```

如果你设置`test`为一个数字，那么迭代将被限制在这个次数。

```
magic_for(test = 2)

for (i in 1:100) {
  squared <- i ^ 2
  put(squared)
}
#> The loop is magicalized with put().
#> squared: 1
#> squared: 4
```

如果`silent = TRUE`，目标函数将不会被执行，但只有值将被存储。

如果`temp = TRUE`，魔法化效果将在 for 循环执行一次后丢失。

```
magic_for(temp = TRUE)
is_magicalized()
#> [1] TRUE

for (i in 1:3) {
  squared <- i ^ 2
  put(squared)
}
#> The loop is temporary magicalized with put().
#> squared: 1
#> squared: 4
#> squared: 9

is_magicalized()
#> [1] FALSE
```

### 3.3 `magic_free()`

你可以使用`magic_free()`来取消魔法化。

```
magic_for()
is_magicalized()
#> [1] TRUE

magic_free()
is_magicalized()
#> [1] FALSE
```

该函数还清除了存储的值。

```
magic_for(silent = TRUE)

for (i in 1:3) {
  squared <- i ^ 2
  put(squared)
}

magic_result_as_vector()
#> [1] 1 4 9

magic_free()
magic_result_as_vector()
#> NULL
```

### 3.4 `magic_result_**()`

你可以使用`magic_result_**()`从魔法化的 for 循环中获取结果。

```
magic_for(silent = TRUE)

for (i in 1:3) {
  squared <- i ^ 2
  put(squared)
}
```

`magic_result()`以列表的形式返回结果。

```
magic_result()
#> $squared
#> $squared[[1]]
#> [1] 1
#> 
#> $squared[[2]]
#> [1] 4
#> 
#> $squared[[3]]
#> [1] 9
```

`magic_result_as_vector()`以向量的形式返回结果。

```
magic_result_as_vector()
#> [1] 1 4 9
```

`magic_result_as_dataframe()`以 data.frame 的形式返回结果。

```
magic_result_as_dataframe()
#>   i squared
#> 1 1       1
#> 2 2       4
#> 3 3       9
```

### 3.5 `put()`

`put()`以高度灵活的方式显示输入值。

```
x <- 2
y <- 3
put(x)
#> x: 2
put(x, y)
#> x: 2, y: 3
put(x, x ^ 2, x ^ 3)
#> x: 2, x²: 4, x³: 8
put(x, squared = x ^ 2, cubed = x ^ 3)
#> x: 2, squared: 4, cubed: 8
```

它对**magicfor**非常有用。

```
magic_for()

for (i in 1:3) {
  put(x = i, squared = i ^ 2, cubed = i ^ 3)
}
#> The loop is magicalized with put().
#> x: 1, squared: 1, cubed: 1
#> x: 2, squared: 4, cubed: 8
#> x: 3, squared: 9, cubed: 27

magic_result_as_dataframe(F)
#>   x squared cubed
#> 1 1       1     1
#> 2 2       4     8
#> 3 3       9    27
```

## 4\. 其他

当你只在魔法化的 for 循环中放置变量时，它们的值将被存储，而不管目标函数如何。

```
magic_for()

for (i in 1:3) {
  squared <- i ^ 2
  squared
}
#> The loop is magicalized with put().

magic_result_as_vector()
#> [1] 1 4 9
```

当你在 if 语句内部写入目标函数而没有 else 时，会插入`NA`表示缺失。

```
magic_for()

for (i in 1:3) {
  squared <- i ^ 2
  if(i == 3) put(squared)
}
#> The loop is magicalized with put().
#> squared: 9

magic_result_as_vector()
#> [1] NA NA  9
```

目标函数仅适用于魔法化的 for 循环中的顶层行或 if 语句内部。例如，在嵌套的 for 循环中不起作用。

```
magic_for()

for (i in 1:2) {
  for (j in 1:2) {
    put(i, j, i * j)
  }
}
#> The loop is magicalized with put().
#> i: 1, j: 1, i*j: 1
#> i: 1, j: 2, i*j: 2
#> i: 2, j: 1, i*j: 2
#> i: 2, j: 2, i*j: 4

magic_result_as_vector()
#> list()
```

## 5\. Bug 报告

+   https://github.com/hoxo-m/magicfor/issues
