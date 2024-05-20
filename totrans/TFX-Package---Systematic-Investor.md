<!--yml
category: 未分类
date: 2024-05-18 14:35:31
-->

# TFX Package | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2012/12/06/tfx-package/#0001-01-01](https://systematicinvestor.wordpress.com/2012/12/06/tfx-package/#0001-01-01)

## TFX Package

Today I want to highlight the [TFX Package](http://cran.r-project.org/web/packages/TFX/index.html) created by Garrett See. TFX is an R Interface to the TrueFX(tm) Web API for free streaming real-time and historical tick-by-tick market data for dealable interbank foreign exchange rates with millisecond detail.

Garrett provided a great tutorial, examples, and shiny application of TFX at [http://rpubs.com/gsee/TFX](http://rpubs.com/gsee/TFX)

Please note that you would need R (>= 2.15.0) to run [TFX](http://cran.r-project.org/web/packages/TFX/index.html). It is very easy to get started. First install required packages:

```
# TFX : R (>= 2.15.0)
install.packages(c('XML','bitops','TFX','shiny'), repos = 'http://cran.r-project.org', dependencies = 'Imports')

```

Next, let run a shiny example of TFX provided by Garrett:

```
# http://cran.r-project.org/web/packages/TFX/index.html
# http://rpubs.com/gsee/TFX
# https://gist.github.com/4122626
library('shiny')

runGist('4122626')

```

Finally, to access the FX quotes in R session:

```
library(TFX)

QueryTrueFX()

```