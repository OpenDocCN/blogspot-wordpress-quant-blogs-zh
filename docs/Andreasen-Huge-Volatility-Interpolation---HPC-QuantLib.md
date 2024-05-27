<!--yml

类别：未分类

日期：2024 年 5 月 13 日 00:17:14

-->

# 安德烈森-休格波动率插值 – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2018/01/05/andreasen-huge-volatility-interpolation/#0001-01-01`](https://hpcquantlib.wordpress.com/2018/01/05/andreasen-huge-volatility-interpolation/#0001-01-01)

几年前，安德烈森和休格提出了一种高效且无套利的波动率插值方法[1]，基于一步有限差分隐式欧拉方案应用于局部波动率参数化。可能最引人注目的用例是从一组期权报价生成局部波动率曲面。

起点是杜皮雷（Dupire）关于欧式看涨期权价格![C_t(T, K)](img/aa953acb973aa0cc8e5fe2f1cec8b911.png)在时刻![t](img/2000b896307ab7e1efa5069769a4fc7f.png)的前向方程，其中行权价为![K](img/7fbda8d36d2bb059dcc3ef722b1f7c78.png)，到期时间为![T](img/6866d563ac5ae988f9a62db320fd2827.png)，给出如下：

![ \frac{\partial C_t(T, K)}{\partial T} = \frac{1}{2}\sigma_{LV}²(T,K)K²\frac{\partial² C_t(T, K)}{\partial K²} - \left(r(T) -q(T)\right) K\frac{\partial C_t(T, K)}{\partial K}-q(T)C_t(T, K)](img/0c212b75a63ba19d1060efc768ff2776.png)

用折现因子![P(t,T)](img/c0f6965fc341ada217f5bf22294e3594.png)、前向价格![F(t,T)](img/e9f9693259b9db50f9dc2cd884a75941.png)和金钱性质![\kappa](img/c4a59d75f76dfbea9fda1b0ae27cb387.png)来定义规范化看涨期权价格![\hat{C}_t(T, \kappa)](img/6d21c2f1808041fa3ca0864a7e5b305f.png)，如下所示：

![P(t,T) &=& e^{-\int_t^T r(\tau)d\tau} \nonumber \\ F(t,T) &=& S_t e^{\int_t^T \left( r(\tau)-q(\tau)\right)d\tau} \nonumber \\ \kappa &=& \frac{K}{F(t,T)} \nonumber \\ \hat{C}_t(T, \kappa) &=& \frac{C_t \left( T, \kappa F(t,T) \right) }{P(t,T)F(t,T)} \nonumber](img/dc3370506b0b8646b551e2c6511257c9.png)。

规范化价格![\hat{C}_t(T,\kappa)](img/9229078bfa8067d5f5e4215ce9cb88c8.png)的杜皮雷前向方程如下：

![ \frac{\partial \hat{C}_t(T, \kappa)}{\partial T} = \frac{1}{2} \sigma_{LV}(T, \kappa F(t,T))\kappa² \frac{\partial² \hat{C}_t(T, \kappa)}{\partial \kappa²} ](img/0828f0135569c82f93d71190ebf9bfa4.png)。

重写这个方程，用![u=\ln \kappa](img/4f83e20ccf571044194a3c01f256a8bb.png)和![\tilde{C}_t(T, u) = \hat{C}_t(T, \kappa)](img/0f886765f539cba48f90530fa5bbab22.png)表示如下：

![ \frac{\partial \tilde{C}_t(T,u)}{\partial T} = \frac{1}{2} \sigma_{LV}² \left( T, e^u F(t,T)\right) \left( \frac{\partial² \tilde{C}_t(T, u)}{\partial u²} - \frac{\partial \tilde{C}_t(T, u)}{\partial u}\right) ](img/7abf43fb08bc074959655ea8550586a5.png)

标准化的看跌期权价格![\tilde{P}_t(T, u) ](img/c494e09d27c531b12de370ab09392cc0.png)满足同样的方程，可以通过将看涨期权价格-看跌期权价格套利插入上述方程中轻松证明

![ \displaystyle \tilde{C}_t(T, u) = \tilde{P}_t(T,u) + 1 - e^u](img/d12a24877d776a9d966a47e4e25d8330.png).

原算法[1]的数值稳定性可以通过立即校准看涨期权和看跌期权来增强，同时插值方案对稳定性有显著影响。这个话题已在[2][3]中讨论。对于有限差分方案，沿着当前现货水平集中网格有利于算法的稳定性和准确性。

为了稳定计算局部波动率函数

![ \displaystyle \sigma_{LV}\left( T, e^uF(t,T)\right) = \sqrt{\frac{2 \frac{\partial \tilde{C}_t(T,u)}{\partial T}}{  \frac{\partial² \tilde{C}_t(T, u)}{\partial u²} - \frac{\partial \tilde{C}_t(T, u)}{\partial u} }}](img/da17886fc1b8bebf10f8f6759e3e62a1.png)

应当评估![\tilde{C}_t(T,u)](img/6dc4e784d17d48fba3574056176e1d9e.png)相对于时间![T](img/6866d563ac5ae988f9a62db320fd2827.png)的一阶导数，利用矩阵![\bf{A}(t)](img/fcdf334da142a0344264f714ae64a562.png)的逆的导数可以得到

![\displaystyle \frac{\partial \bf{A}(t)^{-1}}{\partial t} = -\bf{A}(t)^{-1} \frac{\partial \bf{A}(t)}{\partial t} \bf{A}(t)^{-1}](img/978dfe428afeba21f32d27cd4eef5765.png)

作为例子，下图展示了将 Andreasen-Huge 波动率插值不同标准的 SABR 波动率偏斜校准到离散行权价集合上

![x \in \{ 0.02, 0.025, 0.03, 0.035, 0.04, 0.05, 0.06\} \vee x\in \{0.03, 0.035, 0.04\}](img/925b6919960f4a1f8a1a04a7298979ec.png)

对于 SABR 参数

![\alpha = 0.15, \beta = 0.8, \nu = 0.5, \rho = -0.48, \text{fwd} = 0.03, T=20](img/83e66f0426cf03419089f7fdb0671226.png)

![sabr](img/55798ab77e364d9bd574abf28088240d.png)

QuantLib 实现是[1.12 版本](http://quantlib.org/download.shtml)的一部分。

[1] J. Andreasen, B. Huge, [波动率插值](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=1694972)

[2] F. Le Floc’h, [Andreasen-Huge 插值 – 不要保持平坦](http://chasethedevil.github.io/post/dont-stay-flat-with-andreasen-huge-interpolation/)

[3] J. Healy, [使用 Andreasen-Huge 一步法进行样条插值填补空缺](https://quantsrus.github.io/post/andreasen_huge_spline/)
