<!--yml

类别：未分类

日期：2024-05-17 23:27:39

-->

# 校准局部波动率模型 – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2016/09/11/the-collocating-local-volatility-model/#0001-01-01`](https://hpcquantlib.wordpress.com/2016/09/11/the-collocating-local-volatility-model/#0001-01-01)

在最近的一篇论文[1]中，Lech Grzelak 引入了他的校准局部波动率模型（CLV）。该模型利用所谓的校准方法[2]将任意核过程的累积分布函数映射到从期权市场报价中提取的真实累积分布函数（CDF）。

校准局部波动率模型的起点是标的资产![S_t](img/1d564057c93bc399876bcac34123a321.png)在时间![t_i](img/47514cfd3eec7658c4bd9fa21c2063d0.png)的市场暗示 CDF：

![F_{S(t_i)}(x) = 1 + e^{r t_i}\frac{\partial V_{call}(t_0, t_i, K)}{\partial K}\mid_{K=x} = e^{r t_i}\frac{\partial V_{put}(t_0, t_i, K)}{\partial K}\mid_{K=x}](img/1d564057c93bc399876bcac34123a321.png)过程的动态应由某个随机过程![X_t](img/bac49ad8e6c0a4d679f98639122d578f.png)和一个确定性的映射函数![g(t, x)](img/3f1bc1c27f83ae5b847f8485a3814727.png)给出，使得

![S_t=g(t, X_t) ](img/6f3ce2d0369c41f0c254a6f7d3c51739.png)

映射函数![g(t, x)](img/3f1bc1c27f83ae5b847f8485a3814727.png)确保了由 CLV 模型给出的![S_t](img/1d564057c93bc399876bcac34123a321.png)的期末分布与市场暗示的 CDF 相匹配。然后模型读作

![\begin{array}{rcl} S_t &=& g(t,X_t)  \nonumber \\ dX_t &=& \mu(X_t)dt + \sigma(X_t)dW_t\nonumber \end{array}](img/be97cd57200ff5abef0e7fb870f5a1d6.png)

选择随机过程![X_t](img/bac49ad8e6c0a4d679f98639122d578f.png)不会影响欧式看涨期权的价格——它们由市场暗示的期末 CDF 给出——但会影响模型生成的远期波动率偏斜的动态，因此影响更复杂期权的 prices. 选择一个可追踪的分析过程![X_t](img/bac49ad8e6c0a4d679f98639122d578f.png)以减少计算工作量是可取的。

[2]中概述的配点方法定义了一种有效的算法，可基于一组到期日 ![T_i, i=1,...,m](img/a0a980c52556423df9d70abdfe05361d.png) 和每个到期日 ![T_i](img/0b14d2773a21390d36e26cac3575a150.png) 的 ![j=1,...,n](img/e5b30c05a440ec0f5bec2b027132bd79.png) 插值点近似映射函数 ![g(t, x)](img/3f1bc1c27f83ae5b847f8485a3814727.png)。令 ![F_{S_{T_i}}(s)](img/4d6738ee49a1daba8678bf77d83d5f75.png) 为给定到期日 ![T_i](img/0b14d2773a21390d36e26cac3575a150.png) 的市场隐含 CDF。然后我们得到

![\begin{array}{rcl}  F_{X_{T_i}}\left(x_{i,j}\right) &=& F_{S_{T_i}}\left(g(T_i, x_{i,j})\right) = F_{S_{T_i}}  \left(s_{i,j}\right) \nonumber \\ \Rightarrow s_{i,j}&=&F^{-1}_{S_{T_i}}\left(F_{X_{T_i}}(x_{i,j})\right) \nonumber \end{array}](img/539dfc0861e96986d2bf995f020e4a11.png)

对于带有 ![s_{i,j}=g(T_i, x_{i,j})](img/09d7beec79c7a2c2313028872113982b.png) 的配点。

最佳配点由 ![X_{T_i}](img/be440dd146826fc96b85170fe4e13c1b.png) 的终端分布的高斯积分的横坐标给出。最简单的选择是一个类似于 Ornstein-Uhlenbeck 过程的正态分布内核过程 ![X_t](img/bac49ad8e6c0a4d679f98639122d578f.png)。

![dX_t = \kappa(\theta-X_t)dt + \sigma dW_t](img/e371c8c036fe11e44853873101b1daeb.png)。

正态-CLV 模型的相应配点由以下给出

![\begin{array}{rcl} x_j(t) &=& \mathbb{E}\left[X_t\right] + \sqrt{\mathbb{V}ar\left[X_t\right]} x_j^{\mathcal{N}(0,1)}  \nonumber \\ &=& \theta + \left(X_0 - \theta)e^{-\kappa t}\right) + \sqrt{\frac{\sigma²}{2\kappa}\left(1-e^{-2\kappa t}\right)} x_j^{\mathcal{N}(0,1)}, \ j=1,...,n\end{array}](img/a06b465580b3b248792efa2389ca3ff8.png)

使用 QuantLib 的 Gauss-Hermite 积分实现可以计算标准正态分布的配点 ![x_j^{\mathcal{N}(0,1)}](img/8ef60cf059939554d792608da9ed01da.png)。

```
Array abscissas = std::sqrt(2)*GaussHermiteIntegration(n).x()

```

拉格朗日插值多项式[3]是一种有效的插值方案，可用于插值配点之间的映射函数 ![g(t, x)](img/3f1bc1c27f83ae5b847f8485a3814727.png)。

![g(t, X_t) = \sum_{j=1}^N s_j (t)\prod_{k=1, j\neq k}^N \frac{X(t)-x_j(t)}{x_k(t)-x_j(t)}](img/5c7c4c35cf602167cc3c158501a42079.png)

严格来说，拉格朗日插值多项式不保留单调性，人们也可以使用 QuantLib 的样条插值例程支持的单调插值方案。正如[2]所述，此方法也可以用于近似“昂贵”分布的逆 CDF。

因此，将正态-CLV 模型校准到市场价格非常快速和简单，因为它需要校准 ![g(t, x_t)](img/6f25e33438698975fc801f70334b69ef.png)。

蒙特卡洛定价意味着模拟可追踪过程![X_t](img/bac49ad8e6c0a4d679f98639122d578f.png)并评估如果需要现货过程![S_t](img/mu(x)\frac{\partial V}{\partial x} + \frac{1}{2}\sigma²(x)\frac{\partial² V}{\partial x²}-rV = 0](img/b661d6810fc338425b8833f9242f9cb4.png)。

在到期时间![T](img/6866d563ac5ae988f9a62db320fd2827.png)时的终值条件

![V(T, x_T) = \text{Payoff}\left(S_T=g(T,x_T)\right) ](img/605db840410df2fc8e9e04438cf63047.png)。

对于普通香草期权，上边界和下边界条件为

![\frac{\partial² V}{\partial x²} = 0 \ \ \forall x\in\left\{x_{min},x_{max}\right\}](img/9a48225d6728b0fb0b2882a2bda1fe87.png)。

**示例 1：普通香草期权的定价误差**

+   市场价格由布莱克-舒尔斯-默顿模型给出，

![S_0=100, r=0.1, q=0.04, \sigma=0.25](img/e2c0d9b1310cc3679696b6e03ffcb6e6.png)。

+   普通-CLV 过程参数由

![\kappa=1.0, \theta=0.1,\sigma=0.5,x_0=0.1](img/d7fa7ffc371d4163ebde8d5c55e14fa3.png)。

使用了十个节点来定义映射函数![g(t, x)](img/3f1bc1c27f83ae5b847f8485a3814727.png)，到期时间为一年。下面的图表显示了基于 PDE 解的普通正态-CLV 价格的隐含波动率与真实值的 25%之间的偏差。

![clvpriceerror](img/3cdfdb69e18b377969a2c8410b5bf119.png)。

即使已经使用了十个节点，就已经足够获得非常小的定价误差。如果在节点数增多时，[2]中的建议——扩展节点网格，已经被证明是非常有效的。

**示例 2：波动率曲线的斜率**

+   市场价格由 Heston 模型给出，

![S_0=100, r=0.1, q=0.05, \nu_o=0.09, \kappa=1.0, \theta=0.06, \sigma=0.4, \rho=-0.75](img/8876640de7835a850a82d605d0a762cb.png)。

+   普通-CLV 过程参数由

![\kappa=-0.075, \theta=0.05,\sigma=0.25,x_0=0.05](img/3c8b368d814578cb96fefe0cc0bcd1b2.png)。

下面的图表显示了一种欧式看涨期权（forward starting）的隐含波动率，该期权的行权价从 0.5 到 2 不等，且在重置日之后六个月到期。

![hestonforward](img/5bd33622c388bc6a9b4a6ae653c0b21d.png)。

**参考文献**

毫不奇怪，1Y 双触点期权的价格在与正态-CLV 模型和海森-SLV 模型下所示的“八字胡”图表中表现出类似的模式。但是，使用正态-CLV 模型的计算工作量远小于校准和解决海森-SLV 模型的努力。

+   Market prices are given by the Heston model with

![S_0=100, r=0.02, q=0.01, \nu_o=0.09, \kappa=1.0, \theta=0.06, \sigma=0.8\rho=-0.8](img/170416200f7ee08985d9894c3f2baf33.png).

+   Normal-CLV process parameters are given by different ![\kappa](img/c4a59d75f76dfbea9fda1b0ae27cb387.png) values and

![moustache.png](img/25f436dcca49fbeaadf9f7f729f59f6f.png)

[2] L.A. Grzelak, J.A.S. Witteveen, M.Suárez-Taboada, C.W. Oosterlee,

[The Stochastic Collocation Monte Carlo Sampler: Highly efficient sampling from “expensive” distributions](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=2529691)

The QuantLib implementation of the Normal-CLV model is available as a pull request [#117](https://github.com/lballabio/QuantLib/pull/117), the [Rcpp](https://cran.r-project.org/web/packages/Rcpp/index.html) based package [Rclv](http://hpc-quantlib.de/src/Rclv.tgz) contains the R interface to the QuantLib implementation and the demo code for all three examples.

正态-CLV 模型的远期波动率表面与具有大混合角度 ![\eta](img/3d744e5faf1efbb1fd86f7d17ef67fec.png) 的更复杂的海森或海森随机局部波动（Heston-SLV）模型的表面有重要的相似性。但是，正态-CLV 模型的本质使得远期波动率不依赖于 ![\theta, \sigma](img/227715ad1271e4ab2f943f3443755d65.png) 或 ![x_0](img/c9da0cd5b4ab1e2b208ec1c4a20c8c1b.png) 的值，这限制了该模型可以创建的不同远期偏斜动态的多样性。非正态核过程的 CLV 模型将支持更大的多样性。

**示例 3：双触点期权的定价**

![\theta=100,\sigma=0.15,x_0=100.0](img/1ec5425f0ca67558b998f00f4b1e82e2.png)

[1] A. Grzelak, 2016, [The CLV Framework – A Fresh Look at Efficient Pricing with Smile](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=2747541)
