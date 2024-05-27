<!--yml

category: 未分类

日期：2024-05-13 00:13:24

-->

# 矩匹配期权定价：案例研究 – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2019/11/26/moment-matching-option-pricing-a-case-study/#0001-01-01`](https://hpcquantlib.wordpress.com/2019/11/26/moment-matching-option-pricing-a-case-study/#0001-01-01)

随机变量 *Z* 的矩生成函数是

![M_Z(\theta) := E\left(e^{\theta Z}\right) , \ \theta\in \mathbb{R}](img/fe23617925504d96684f4c15b8af2d21.png)

概率分布 *Z* 的第 *n* 个矩则为

![\displaystyle m_n=E\left(Z^n\right) = M_Z^{(n)}(0) = \frac{d^n M_Z(\theta)}{d\theta^n}\bigg\rvert_{\theta=0}](img/5f664dc216bebde5e7bc03b0acf0d012.png)

对许多金融模型来说，矩生成函数是已知的。因此，基于矩生成函数推导出近似的精确定价公式是很自然的。

克鲁格（Kluge）模型 [1] 使用指数跳跃尺寸分布，在这里可以作为这种方法的测试平台。它的定义如下

![\displaystyle \begin{array}{rcl} S_t &=& \exp(f_t + X_t + Y_t) \\ dX_t &=& -\alpha X_tdt + \sigma dW_t^x \\ dY_t &=& -\beta Y_{t-}dt+J_tdN_t \\ \omega(J) &=& \eta e^{-\eta J} \end{array} ](img/71ee40e5982f6748faffab6247f9278b.png)

其中 ![N_t](img/c6d44fd3b9c210c1d0e71a4a31edb3dc.png) 是具有跳跃强度 ![\lambda](img/4a42b8a415b6b944138e18b71269a40a.png) 的泊松过程，![\eta](img/3d744e5faf1efbb1fd86f7d17ef67fec.png) 是逆跳跃尺寸。为了匹配今天的远期曲线 ![F_0^t](img/421429e49cb430d88afd689dbfe570cc.png)，函数 ![f_t](img/f963c39a6323c381d376d8074fc65006.png) 给出如下

![\displaystyle f_t = \ln F_0^t -X_0 e^{-\alpha t}-Y_o e^{-\beta t} -\frac{\sigma²}{4\alpha}\left(1-e^{-2\alpha t} \right ) - \frac{\lambda}{\beta}\ln\left( \frac{\eta-e^{-\beta t}}{\eta-1}\right), \eta\ge 1 ](img/2b3ad4e6ae2eba9d5316e5e0253cbd3e.png)

对数点过程的矩生成函数

![Z_t = \ln S_t = f_t+X_t+Y_t](img/a293d8acdbd5e262abd4223736f13217.png)

则由 [1] 给出

![\displaystyle M_Z(t) = \exp\left( \theta f_t + \theta X_0 e^{-\alpha t} + \theta² \frac{\sigma²}{4\alpha}\left(1-2e^{-2\alpha t}\right) + \theta Y_0e^{-\beta t}\right) \left( \frac{\eta-\theta e^{-\beta t}}{\eta-\theta}\right)^\frac{\lambda}{\beta}](img/e5e1133417f9c4ceac0f9275c4d0391d.png)

定价近似公式是基于中心矩

![\displaystyle \mu_n = E\left[\left(Z-E(Z)\right)^n\right] = \sum_{i=0}^n {n\choose i} m_i (-E(Z))^{n-i}](img/cf5eea80663cdf7c10d1e58b075aa5c2.png)

Mathematica 计算前四个中心矩如下

![\begin{array}{rcl} \displaystyle \mu_1&=&0 \\ \displaystyle \mu_2 &=& \frac{\sigma² \left(1-e^{-2 \alpha t}\right)}{2\alpha }+\frac{\lambda \left(1- e^{-2 \beta t}\right)}{\beta \eta ²}\\ \mu_3 &=& \frac{\lambda \left(2-2 e^{-3 \beta t}\right)}{\beta \eta ³} \\ \displaystyle \mu_4 &=& \frac{3 e^{-5 t (\alpha +\beta )} \left(16 \alpha ² \beta \lambda e^{5 \alpha t+3 \beta t} \sinh (2 \beta t)+e^{t (\alpha +\beta )} \left(\beta \eta ² \sigma² \left(e^{2 \alpha t}-1\right) e^{2 \beta t}+2 \alpha \lambda e^{2 \alpha t} \left(e^{2 \beta t}-1\right)\right)²\right)}{4 \alpha ² \beta ² \eta ⁴}.\end{array}](img/9170a7ae9f54bd9502c6d88dcb7ad4b7.png)

高阶矩的 Black-Scholes 类似对数正态模型的近似总结在[2]中。这些扩展以新奇性和峰度为 Fisher 参数的参数化

![\displaystyle \gamma_3=\frac{\mu_3}{\mu_2^{3/2}}, \ \gamma_4 = \frac{\mu_4}{\mu_2²}-3](img/a8ae17f52bb3b41e4329c9c93bbe14b2.png)

Cor

![\begin{array}{rcl} \displaystyle C_{CS}&=&C_{BS}(F_0^t, K, \sigma, r, t) +\gamma_3 Q_3 + \gamma_4 Q4 \\ Q_3 &=& \frac{1}{3!}F_0^t\sigma\sqrt{t}\left(2\sigma\sqrt{t}-d)\right)\varphi(d)\\ Q_4&=& \frac{1}{4!}F_0^t\sigma\sqrt{t}\left(d²-3d\sigma\sqrt{t}-1\right)\varphi(d)\\ \varphi(d) &=& \frac{1}{\sqrt{2\pi}}e^{-\frac{d²}{2}}\\ d &=& \frac{\ln\left(F_0^t/K\right)+\sigma² t/2}{\sigma \sqrt{t}}\\\sigma &=& \sqrt{\mu_2 / t}.\end{array}](img/ca30fe2b70b40005dc853d0050b78fbe.png)

而 1998 年 Rubinstein [4]在考虑了正态 Edgeworth 级数展开后推导出了以下的近似

![\begin{array}{rcl} \displaystyle C_R = &=&C_{BS}(F_0^t, K, \sigma, r, t) +\gamma_3 Q_3 + \gamma_4 Q4 + \gamma_3² Q_5 \\ Q_5&=& \frac{10}{6!}F_0^t\sigma\sqrt{t}\left(d⁴-5d³\sigma\sqrt{t}-6d²+15d\sigma\sqrt{t}+3\right)\varphi(d). \end{array}](img/e7e14f52245b462b79ce1010995dff0a.png)

考虑了两种情况来测试 Kluge 模型的不同近似的质量。首先是相对较小的跳跃但跳跃强度变化的情况，其次是少数跳跃但跳跃大小变化的情况。测试参数为

![F_0=30, K=F_0, t=0.5, X_0=Y_0=0, \\ \alpha=4.0, \sigma=1.0, \beta=5.0, \eta=5.0, \lambda=4.0](img/c66d300b03f308b0492775875e2ebbee.png)

欧洲式 vanilla 期权的参考结果是使用相应的有限差分定价引擎和理查森外推法生成的。第一个测试案例是通过增加 ![\lambda](img/4a42b8a415b6b944138e18b71269a40a.png) 从零到 40 来变化跳跃次数。![jumpintensity.png](img/810a3a837a35006056667274dfa9885b.png)科拉多/苏第四阶近似仅在跳跃强度非常小的情况下获胜，而对于较大的跳跃强度，科拉多/苏高达第三阶的近似与鲁宾斯坦公式竞争激烈。第二个测试案例中，跳跃次数少但跳跃大小增加，情况类似。对于小跳跃，第四阶近似占主导地位，但大部分时间鲁宾斯坦近似给出最佳结果。![jumpsize.png](img/204a8333c5642a615c7daf34a9d23dec.png)

这些结果的源代码可以从[PR #728](https://github.com/lballabio/QuantLib/pull/728)获取。

[1] Kluge, T. : [定价摆动期权及其他电力衍生品](https://www.semanticscholar.org/paper/Pricing-Swing-Options-and-other-Electricity-Kluge/9e8be93531ffa8aeb1a9e36181e0537cac99e400)

[2] Jurczenko, E, Maillet, B and Negrea, B: [多时刻近似期权定价](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=300922)

[模型：一般比较（第一部分）](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=300922)

[3]  Corrado C. and T. Su: [隐含波动率偏度和股票回报](https://www.researchgate.net/publication/24080621_Implied_volatility_skews_and_stock_return_skewness_and_kurtosis_implied_by_stock_option_prices)

[股票期权价格所隐含的偏度和峰度](https://www.researchgate.net/publication/24080621_Implied_volatility_skews_and_stock_return_skewness_and_kurtosis_implied_by_stock_option_prices) , 欧洲杂志 of

金融 3, 73-85., 1997

[4] Rubinstein M: [爱德华·吉福特二项式树](https://pdfs.semanticscholar.org/f5d2/d0b90dea9a5e2dc298f0ba0aefc2b98387e4.pdf), 《衍生品杂志》

5 (3), 20-27., 1998
