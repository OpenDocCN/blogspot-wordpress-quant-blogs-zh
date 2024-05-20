<!--yml
category: 未分类
date: 2024-05-18 06:49:06
-->

# HOXO-M - anonymous data analyst group in Japan - : Simple example:How to use foreach and doSNOW packages for parallel computation.

> 来源：[http://mockquant.blogspot.com/2011/02/simple-examplehow-to-use-foreach-and.html#0001-01-01](http://mockquant.blogspot.com/2011/02/simple-examplehow-to-use-foreach-and.html#0001-01-01)

**update**

************************************************************************************************

I checked whether this example was run collectly or not in **Windows XP(32bit) only** ! 

************************************************************************************************

In R language, the members at Revolution R provide foreach and doSNOW packages for parallel computation. these packages allow us to compute things in parallel. So, we start to install these packages.

<fieldset>[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")</fieldset>

In foreach package, you can write the codes which are run not only in parallel but also in sequence. And, these are as following.

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

[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")</fieldset>

Next, we make clusters by doSNOW package for the purpose of parallel computation.

Because I have dual core machine, I specify two as the number of clusters.

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

[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")</fieldset>

Now, We are ready to compute things in parallel. It is easy for us to do that by foreach package. You only have to change "%do%" into "%dopar%". I compared the performance of parallel comutation to single computation as following.

<fieldset>[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")</fieldset>

(I'm sorry that some terms are written in Japanese!)

You can understand the result of parallel computation is about twice as fast as single computation do !!!

Reference（including PDF）

-

[http://cran.r-project.org/web/packages/foreach/foreach.pdf](http://cran.r-project.org/web/packages/foreach/foreach.pdf)

-

[http://cran.r-project.org/web/packages/foreach/vignettes/foreach.pdf](http://cran.r-project.org/web/packages/foreach/vignettes/foreach.pdf)

-

[http://cran.r-project.org/web/packages/foreach/vignettes/nested.pdf](http://cran.r-project.org/web/packages/foreach/vignettes/nested.pdf)