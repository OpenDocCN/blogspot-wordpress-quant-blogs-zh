<!--yml
category: 未分类
date: 2024-05-12 19:51:03
-->

# Weighted least squares in R | Coding the markets

> 来源：[https://etrading.wordpress.com/2006/08/18/weighted-least-squares-in-r/#0001-01-01](https://etrading.wordpress.com/2006/08/18/weighted-least-squares-in-r/#0001-01-01)

## Weighted least squares in R

### August 18, 2006

I’m using R to fit curves to data that has outliers backed by low observation counts. I’ve been thrashing round trying different R fitting methods, including [glm.fit](https://etrading.wordpress.com/2006/08/15/the-power-of-r-curve-fitting/). But linear fits were obviously wrong. Not being a maths graduate, I was a bit stumped until I had a chat with one of our more maths and tech minded model traders. He looked at my charts and data, and suggested a weighted least squares fit.

In R we can do a least squares fit with loess() and predict(). Given sample data including weights, loess() will generate fitting parameters. The you feed data points to be charted through predict(), along with the fitting parameters, and plot the nicely smoothed result. Do example(loess) in R to get started.