<!--yml
category: 未分类
date: 2024-05-18 14:33:31
-->

# Sector Rotation Back Test Shiny web application | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2013/02/18/sector-rotation-back-test-shiny-web-application/#0001-01-01](https://systematicinvestor.wordpress.com/2013/02/18/sector-rotation-back-test-shiny-web-application/#0001-01-01)

[Home](https://systematicinvestor.wordpress.com/ "Go to homepage")

>

[R](https://systematicinvestor.wordpress.com/category/r/)

,

[Shiny](https://systematicinvestor.wordpress.com/category/shiny/)

> Sector Rotation Back Test Shiny web application

## Sector Rotation Back Test Shiny web application

Today, I want to share the [Sector Rotation Back Test](http://glimmer.rstudio.com/systematicin/sector.rotation/) application (code at [GitHub](https://github.com/systematicinvestor/SIT/tree/master/Shiny/sector.rotation)).

This is the last application in the series of examples (I have shared 5 examples) that will demonstrate the amazing [Shiny](http://www.rstudio.com/shiny/) framework and [Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/) to analyze stocks, make back-tests, and create summary reports.

The motivation for this series of posts is to show how to translate, with minimal effort, your back-test scripts into live web applications that can either be run from the Shiny server or your personal computer.

Please note that Back Test applications take longer time to update the plots/tables and hence maybe more appropriate to run from your local computer.

For example to run [Sector Rotation](http://glimmer.rstudio.com/systematicin/one.stock/) application from your computer, you first need to install [Shiny](http://www.rstudio.com/shiny/). And next execute following commands:

```
library(shiny)
runGitHub('SIT','systematicinvestor', subdir = 'Shiny/sector.rotation')

```