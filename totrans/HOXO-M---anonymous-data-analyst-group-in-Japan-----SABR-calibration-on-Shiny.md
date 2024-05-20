<!--yml
category: 未分类
date: 2024-05-18 06:48:21
-->

# HOXO-M - anonymous data analyst group in Japan - : SABR calibration on Shiny

> 来源：[http://mockquant.blogspot.com/2013/09/sabr-calibration-on-shiny.html#0001-01-01](http://mockquant.blogspot.com/2013/09/sabr-calibration-on-shiny.html#0001-01-01)

As you already know(if you often use R!!),

[Shiny](http://www.rstudio.com/shiny/)

allows us to create web applications in R easily. It doesn't require the knowledge of HTML, CSS, javascript, I mean, we don't need to write HTML, CSS and javascript directly to create web application.

The users of your web application can change the input parameters interactively via web applications. It will give a good opportunities to understand how the model works and it's limitation.

[Systematic Investor's examples](http://systematicinvestor.wordpress.com/shiny/)

are very nice application in financial analysis, I was so excited when I saw it at first. I decided to create my own web application by shiny as a "mock" quant.

My appication is here(you can also get the source code of this application on

[Github](https://github.com/teramonagi/SABRCalibrationOnShiny)

):

It is a calibration of SABR model based on Hagan's approximation formula(

[Managing Smile Risk, P. Hagan et al(pdf)](http://www.math.columbia.edu/~lrb/sabrAll.pdf)

). In some derivative market, SABR model is de facto model, you can understand how much degree SABR model can fit market data(IV) and it's limit.