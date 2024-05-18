<!--yml
category: 未分类
date: 2024-05-18 13:50:57
-->

# Why Minimize Negative Log Likelihood? | Quantivity

> 来源：[https://quantivity.wordpress.com/2011/05/23/why-minimize-negative-log-likelihood/#0001-01-01](https://quantivity.wordpress.com/2011/05/23/why-minimize-negative-log-likelihood/#0001-01-01)

One of the wonders of machine learning is the diversity of divergent traditions from which it originates, from classical statistics (both frequentist and Bayesian) to information and control theories, plus a significant dose of pragmatism from computer science. For those interested in the historical relationship between statistics and machine learning, see Breiman’s [Two Cultures](http://www.stat.osu.edu/~bli/dmsl/papers/Breiman.pdf).

This diversity is reflected in the *surprising complexity in answering simple-sounding questions*, which often speaks to the heart of trading using computational machine learning models—ranging from estimating HMM models via MLE (*e.g.* vol / correlation regime models) to non-convex optimization via non-standard likelihood or loss functions (*e.g.* portfolio optimization via [omega](http://finance.yendor.com/etfviz/2007/0928/Omega-intro.pdf)):

> Why is minimizing the negative log likelihood equivalent to maximum likelihood estimation (MLE)?

Or, equivalently, in Bayesian-speak:

> Why is minimizing the negative log likelihood equivalent to maximum a posteriori probability (MAP), given a uniform prior?

Answering this question provides insight into the foundations of machine learning, as well as connection with several branches of mathematics.

Classic statistics opens the answer, beginning with the definition of a likelihood function:

   ![\mathcal{L}(\theta\,|\,x_1,\ldots,x_n) = f(x_1,x_2,\ldots,x_n|\theta) = \prod\limits_{i=1}^n f(x_i|\theta) ](img/db7b7c771dae4d02ed64d1e6926aaca1.png)

Applying the natural log function in this context is handy, for several reasons. First, numerical analysis reminds us that logs reduce potential for underflow, due to very small likelihoods. Second, calculus reminds us logs permit the addition trick: converting a product of factors into a summation of factors (as seen before in [Why Log Returns?](https://quantivity.wordpress.com/2011/02/21/why-log-returns/)). Finally, calculus again reminds us that the natural log function is a [monotone transformation](http://en.wikipedia.org/wiki/Monotone_transformation).

Thus, the extrema of ![\mathcal{L} ](img/8639f7e55dad758d20f029b786e751d6.png) are equivalent to the extrema of ![\log \mathcal{L} ](img/02559069dc8e9039e69fd36941cdb361.png):

   ![\log \mathcal{L}(\theta\,|\,x_1,\ldots,x_n) = \sum\limits_{i=1}^n \log f(x_i|\theta) ](img/771cfc5a64a745e3f1adadf98e7b5cb8.png)

From which the maximum likelihood estimator ![\hat{\theta}_{\textnormal{MLE}} ](img/9394ddc68735b13f4d7783aeb4d5ebeb.png) is defined as:

   ![\hat{\theta}_{\textnormal{MLE}} = \underset{\theta}{\arg\max} \sum\limits_{i=1}^n \log f(x_i|\theta) ](img/31c41082b843f584d849d8c093990986.png)

As an aside, Bayesians will remind us we can generalized into a MAP estimator, given uniform prior ![g(\theta) ](img/6352dcc368facb12058a8b962faab298.png):

   ![\underset{\theta}{\arg\max} \sum\limits_{i=1}^n \log f(x_i|\theta)  = \underset{\theta}{\arg\max} \log(f|\theta) = \underset{\theta}{\arg\max} \log(f|\theta) g(\theta) = \hat{\theta}_{\textnormal{MAP}} ](img/8bd285cc2ac47d37c270931132d62dda.png)

From which optimization and real analysis reminds us of the following equivalence, for all ![x](img/2d501e79ed2376e8a010ea6a3ecd5a7a.png):

   ![\underset{x}{\arg\max} (x)  = \underset{x}{\arg\min} (-x) ](img/1899e2696a8fd36a9315850efb198c1e.png)

Thus, the following are equivalent:

   ![\underset{\theta}{\arg\max} \sum\limits_{i=1}^n \log f(x_i|\theta) = \underset{\theta}{\arg\min} - \sum\limits_{i=1}^n \log f(x_i|\theta) = \hat{\theta}_{\textnormal{MLE}} ](img/b88ac1ce4ac1d4305e7f94fb112eec39.png)

From this, we technically have an answer to the above two questions on equivalence. Yet, from here lies the opportunity to continue and *uncover the relationship between MLE/MAP and both entropy and loss via [Kullback-Leibler divergence](http://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence)* (KL). To get there, consider the statistical *average* of the above:

   ![\underset{\theta}{\arg\min} (\frac{1}{n} \sum\limits_{i=1}^n - \log f(x_i|\theta) ) ](img/1b5a26ea8f0e1a0181399514de712caa.png)

Which converges, by the strong law of large numbers, to the expectation:

   ![E[- \log f(x|\theta)] ](img/b8ac9258711173ed57fd070378fa01a4.png)

Which is interesting when considering the *difference in distribution* between ![\theta ](img/5658aea6429ae8d7ac8025a9e14d9ad5.png) and its corresponding true actual parameter ![\theta^*](img/8c02debe01f63b57c846d411d0b0bfc5.png):

   ![E[\log f(x|\theta^*) - \log f(x|\theta)] = E[\log\frac{f(x|\theta^*)}{f(x|\theta)}] = \int \log \frac{f(x|\theta^*)}{f(x|\theta)} f(x|\theta^*) dx ](img/b78999766cb5815374665ffde632aa21.png)

Which is indeed equal to none other than the KL divergence, ![K(f(x|\theta),f(x|\theta^*))](img/de221839e02e156764ec42360c5bc279.png), between ![\theta ](img/5658aea6429ae8d7ac8025a9e14d9ad5.png) and ![\theta^* ](img/7cf97fab765bc754e466fdd1527b652a.png):

   ![\int \log \frac{f(x|\theta^*)}{f(x|\theta)} f(x|\theta^*) dx = K(f(x|\theta),f(x|\theta^*))](img/79102b38603c147d6afa5dece6e93102.png)

Which information theory reminds us is relative entropy, and thus is also equal to the excess risk for the loss function defined by the negative log-likelihood. Finally, connecting Bayesian statistics to the foundation of information theory: gain in [Shannon entropy](http://en.wikipedia.org/wiki/Entropy_(information_theory)#Definition) going from prior to posterior is indeed the KL divergence.

Thus, *maximum likelihood and maximum a posteriori probability are special case loss functions* (see [Loss Function Semantics](http://hunch.net/?p=269) for more on loss semantics in ML).