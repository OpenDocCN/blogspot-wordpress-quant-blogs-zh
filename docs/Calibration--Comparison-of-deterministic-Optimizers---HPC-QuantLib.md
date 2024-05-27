<!--yml

类别：未分类

日期：2024-05-17 23:43:23

-->

# 校准：确定性优化器的比较 – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2011/05/17/calibration-comparison-of-deterministic-optimizers/#0001-01-01`](https://hpcquantlib.wordpress.com/2011/05/17/calibration-comparison-of-deterministic-optimizers/#0001-01-01)

目标是校准一个时间相关的 Heston 模型，该模型由以下 SDE 定义

![ &=& \mu_t S dt + \sqrt{v} S dW_1 \\ dv(t, S) &=& \kappa_t (\theta_t - v) dt + \sigma_t \sqrt{v} dW_2 \\ dW_1 dW_2 &=& \rho_t dt \end{array}")](http://www.codecogs.com/eqnedit.php?latex=%5Cbegin%7Barray%7D%7Brcl%7D%20dS%28t,%20S%29%20&=&%20%5Cmu_t%20S%20dt%20@plus;%20%5Csqrt%7Bv%7D%20S%20dW_1%20%5C%5C%20dv%28t,%20S%29%20&=&%20%5Ckappa_t%20%28%5Ctheta_t%20-%20v%29%20dt%20@plus;%20%5Csigma_t%20%5Csqrt%7Bv%7D%20dW_2%20%5C%5C%20dW_1%20dW_2%20&=&%20%5Crho_t%20dt%20%5Cend%7Barray%7D)

参数集 ![\{\kappa_t, \theta_t, ,\sigma_t, \rho_t\}](img/0fbc0509db71e752f7099e569e721184.png) 应该在时间上分段常数。该模型基于特征函数方法有一种半封闭解来定价普通欧式看涨/看跌期权 [1]。

基于 2002 年 7 月 5 日的数据，DAX 隐含波动率曲面定义了“基准”校准问题。

![\Theta = \{\nu_0, \kappa_{0\leq t < 0.25}, \kappa_{0.25 \leq t},\theta, \sigma, \rho\}](img/cce1c6db5ea57e29f0eb7573e76ec363.png).

非线性最小二乘优化问题由拟合度度量定义

![\zeta=\min_{\Theta} \sum_{i=1}^N \left( \sigma_i^{market}(K,T) - \sigma_i^{model}(K,T, \Theta) \right)²](img/1fa36158722237a38f624e39f8bde452.png)

其中 ![\sigma_i^{market}(K,T)](img/9e5e12fcb2e9f683e3a9ea424a83977a.png) 是罢工价 K 和到期 T 的市场隐含波动率，![\sigma_i^{model}(K,T, \Theta)](img/60e7a13f5bf3301f65f8bca7ffc8b298.png) 是相应的从模型价格推导出的 Black-Scholes 波动率隐含值。此问题的最优解是

![\Theta_{min} = \{ 0.2231, 39.651, 7.546, 0.0954, 5.1865, -0.5004 \}](img/00211b944537773793afcdc6f092fe56.png)

导致拟合度度量为 ![\zeta_{min}=74.4731](img/b905c4624a6dbf040387a7307295c2b1.png) （请记住，这个结果是一个简单的校准过程的结果。由于大 ![\kappa](img/c4a59d75f76dfbea9fda1b0ae27cb387.png) 和 ![\sigma](img/d2e0f91b4f9ab5cb8554a898295d118c.png) 值，我不会使用这些参数来定价衍生产品。）。

![](https://hpcquantlib.wordpress.com/wp-content/uploads/2011/05/plot5.png) [](https://hpcquantlib.wordpress.com/wp-content/uploads/2011/05/plot3.png) 上图显示了参数集的“拟合度”曲面

![公式](img/d52373188e27bca6a1db73e6254d0d80.png)：**θ = { 0.2231, 39.651, $κ_{0.25 ≤ t} \in [0, 16]$, 0.0954, $σ \in [0, 16]$, -0.5004 }**

为了能够比较更多的确定性优化器，模型校准将使用[R](http://www.r-project.org/)进行，并借助额外的包[minpack.lm](http://cran.r-project.org/web/packages/minpack.lm/index.html)和[minqa](http://cran.r-project.org/web/packages/minqa/index.html)进行。

**非线性最小二乘优化**：

1.  **nls.lm**：Levenberg-Marquardt 算法（基于[MINPACK](http://www.netlib.org/minpack)，也可在[QuantLib](http://quantlib.org/)中找到）

1.  **nls**：高斯牛顿算法

1.  **nl2sol**：基于 PORT 库。

**非线性（信任区域）最小化**：

1.  **nlm**：牛顿样式最小化器

1.  **bfgs**：由 Broyden、Fletcher、Goldfarb 和 Shanno 发表的拟牛顿方法

1.  **l-bfgs-b**：包含箱式约束的有限内存 BFGS 算法

1.  **cg**：共轭梯度算法

1.  **nm**：Nelder-Mead 方法

1.  **bobyqa**：通过插值形成二次模型的信任区域方法。

1.  **newuoa**：通过插值形成二次模型的信任区域方法。

1.  **uobyqa**：通过插值形成二次模型的信任区域方法。

具体结果取决于起始向量，但下图显示了一种常见结果。

![图](https://hpcquantlib.wordpress.com/wp-content/uploads/2011/05/plot7.png) [](https://hpcquantlib.wordpress.com/wp-content/uploads/2011/05/plot6.png) 最佳方法是非线性最小二乘算法 nls.lm 和 nls，其次是 nl2sol。未包含在图中的算法甚至比此问题的“nm”表现更差。

拟合优度量是基于[QuantLib](http://quantlib.org)中的 C++ 计算，并使用[RCPP](http://cran.r-project.org/web/packages/Rcpp/index.html)暴露给[R](http://www.r-project.org/)。可以在[这里](http://hpc-quantlib.de/src/optimproblem.zip)找到执行优化和创建图表的 C++ 代码和 R 脚本。

1] A. Elices，[使用变换方法处理具有时间相关参数的模型：Heston 模型的应用](http://arxiv.org/pdf/0708.2020)

[2]  A. Sepp，[使用傅立叶变换处理跳跃扩散过程的随机波动性下的欧式期权定价：应用](http://math.ut.ee/%7Espartak/papers/stochjumpvols.pdf)
