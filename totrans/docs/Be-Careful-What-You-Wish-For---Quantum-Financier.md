<!--yml
category: 未分类
date: 2024-05-18 14:01:48
-->

# Be Careful What You Wish For – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2010/10/28/be-careful-what-you-wish-for/#0001-01-01](https://quantumfinancier.wordpress.com/2010/10/28/be-careful-what-you-wish-for/#0001-01-01)

It is in the human nature to seek the path of least resistance. While this might be good in some instances, when dealing with my capital I usually try to keep it simple but I try to always steer clear from intellectual laziness.

Many top tier bloggers have mentioned the traps of assumptions and the limitations of parametric statistics when dealing with market data. A good thing to do before using a certain method or model is always to do a little research on the underlying assumptions. If they don’t fit our data, then we know we have to be more careful, however they can still be quite useful, do not automatically disregard a method or model when your assumptions aren’t met.

For example, consider the great workhorse of econometrics: the least square model. It is widely used in academia. It is actually quite hard to find a finance paper without the mention of regression in a certain way or form. That’s just what we do, we like to try and model phenomenon in simple and elegant ways. It is often used in its simplest form; the ordinary least square model that you of you may know as the linear regression. I am sure that most of the readers of this blog used it before in some fashion. I also think that some may have used it without really paying attention to some of its assumptions.

1\. Population regression function is linear in parameters
2\. The independent variable and the errors are independent: ![cov(x_i, \varepsilon_i) = 0](img/b35240989ae5e105ee6ae46ac47ab5ca.png)
3\. Homoscedasticity (ie. constant variance) of the errors
4\. No autocorrelation: ![cov(\varepsilon_t, \varepsilon_{t-1}) = 0](img/d9bbf4381fc46813f34013abab38b3b9.png)
5\. The regression model is correctly specified, all relevant variables are included
6\. The error is normally distributed

Now with this in mind, we see how the ols has some assumptions that we would need to address before we blindly apply it. The big two for financial time series are number 3 and 4\. See the post series on GARCH modeling for a more specific discussion on the matter [here](https://quantumfinancier.wordpress.com/2010/09/12/381/).

The point here is not to invalidate the least squares method at all; I use it frequently. The point is to show that sometimes assumptions can be really restrictive and need to be considered regardless of what method or model you want to use, and also remember that sometimes, the path of least resistance in trading is not always the best. A good habit when stumbling upon a new promising tool for your trader’s toolbox is to dig a bit more and understand the underlying process and the assumptions you make every time you use it. It is also a nice plug for the non-parametric and non-linear statistical methods, who usually tends to have looser base assumptions.

QF