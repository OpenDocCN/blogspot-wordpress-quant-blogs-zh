<!--yml

category: 未分类

日期：2024-05-18 06:49:06

-->

# HOXO-M - 日本匿名数据分析团队 - : 简单示例：如何使用 foreach 和 doSNOW 包进行并行计算。

> 来源：[`mockquant.blogspot.com/2011/02/simple-examplehow-to-use-foreach-and.html#0001-01-01`](http://mockquant.blogspot.com/2011/02/simple-examplehow-to-use-foreach-and.html#0001-01-01)

**更新**

************************************************************************************************

我检查了这个例子是否在**仅限 Windows XP (32 位)** 上正确运行了！

************************************************************************************************

在 R 语言中，Revolution R 的成员们提供了用于并行计算的 foreach 和 doSNOW 包。这些包允许我们并行计算。因此，我们开始安装这些包。

<fieldset>[由 Pretty R 在 inside-R.org 创建](http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 创建")</fieldset>

在 foreach 包中，你可以编写不仅可以并行运行还可以顺序运行的代码。以下是这些代码。

<fieldset>

```
library(foreach)
#we get result as list
foreach(i = 1:3) %do% {sqrt(i)}
#we get result as vector with using .combine="c" option
foreach(i = 1:3,.combine = "c") %do% {sqrt(i)}
#if a result is "vector",we can get it as matrix with using .combine="cbind" option
foreach(i = 1:3,.combine = "cbind") %do% {letters[1:4]}
#if you define a function,you can use it as .combine option
#I wrote my function as returning same result that specify .combine="c" 
MyFunc <- function(x,y)c(x,y)
foreach(i = 1:3, .combine = "MyFunc") %do% {
  sqrt(i)
}
```

[由 Pretty R 在 inside-R.org 创建](http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 创建")</fieldset>

接下来，我们使用 doSNOW 包来创建集群，以进行并行计算。

因为我有双核机器，所以我将集群数指定为两个。

<fieldset>

```
> library(doSNOW)
> getDoParWorkers()
[1] 1
> getDoParName()
NULL
> registerDoSNOW(makeCluster(2, type = "SOCK"))
> getDoParWorkers()
[1] 2
> getDoParName()
[1] "doSNOW"
> getDoParVersion()
[1] "1.0.3"
```

[由 Pretty R 在 inside-R.org 创建](http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 创建")</fieldset>

现在，我们已经准备好进行并行计算了。通过 foreach 包，我们很容易做到这一点。你只需要将 "%do%" 改为 "%dopar%"。我将并行计算的性能与单一计算进行了比较，如下所示。

<fieldset>[由 Pretty R 在 inside-R.org 创建](http://www.inside-r.org/pretty-r "由 Pretty R 在 inside-R.org 创建")</fieldset>

（对不起，一些术语是用日语写的！）

你可以理解并行计算的结果大约比单个计算快近一倍！！！

参考（包括 PDF）

-

[`cran.r-project.org/web/packages/foreach/foreach.pdf`](http://cran.r-project.org/web/packages/foreach/foreach.pdf)

-

[`cran.r-project.org/web/packages/foreach/vignettes/foreach.pdf`](http://cran.r-project.org/web/packages/foreach/vignettes/foreach.pdf)

-

[`cran.r-project.org/web/packages/foreach/vignettes/nested.pdf`](http://cran.r-project.org/web/packages/foreach/vignettes/nested.pdf)
