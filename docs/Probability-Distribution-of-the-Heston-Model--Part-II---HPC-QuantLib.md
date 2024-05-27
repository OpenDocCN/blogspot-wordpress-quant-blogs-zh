<!--yml

类别：未分类

日期：2024-05-17 23:32:32

-->

# Heston 模型的概率分布，第二部分 - HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2014/02/22/probability-distribution-of-the-heston-model-part-ii/#0001-01-01`](https://hpcquantlib.wordpress.com/2014/02/22/probability-distribution-of-the-heston-model-part-ii/#0001-01-01)

Heston 模型的 Fokker-Planck 正向方程的半解析解的起点是 Broadie 和 Kaya [1] 的精确抽样算法（有关符号，请参见 [2]）

![\begin{array}{rcl} x_t &=& x_0 + m(t) + \sigma(t)Z \nonumber \\ \sigma²(t) &=& (1-\rho²)\int_0^t \nu_s ds \nonumber \\ m(t) &=& (r_t-q_t)t - \frac{1}{2}\int_0^t \nu_s ds + \rho\int_0^t \sqrt{\nu_s}dW_s^{(1)} \nonumber \end{array}](img/928b825394cb30fa0d6e679752c8f983.png)

概率分布函数可以描述为

![p(x_t, \nu_t, t) = p(\nu_t, t) p(x_t,t\mid \nu = \nu_t) ](img/bdea86416e661daeb5822f56f8e4bfc7.png)

以及 ![p(\nu_t, t)](img/430842f34bf863fe6bb7c17e3c6a3a8f.png) 是一个非中心卡方分布。分布 ![p(x_t, t \mid \nu = \nu_t)](img/e3bed4b562bcc0bd779656cbc56327a1.png) 可以使用精确模拟算法计算。在这个算法中，变量 ![x_t](img/7a6c51eeafde57877526801e4a5da1e1.png) 是两个随机变量 ![\int_0^t \nu_s ds](img/787aff30b276853cbb00259a1e526614.png) 和 ![Z](img/051625cbd82ebd99476330b3cd2e1917.png) 的函数。

![x_t](img/7a6c51eeafde57877526801e4a5da1e1.png) 的分布现在可以使用随机变量的一般转换定理来推导：设 *X* 是一个具有概率密度函数 *f* 的随机变量。转换后的随机变量 ![Y=h(X)](img/8bddc80b8b9e990d7a203826ae694707.png) 具有概率密度函数

![p(y) = f(h^{-1}(y)) \left| \det \left( \frac{\partial h^{-1}_i(y)}{\partial y_j} \right)\right|](img/b42c2ccbbce570d49a91ce7efaafa8ce.png)

第一步是现在将精确模拟方法重写为两个随机变量的形式

![X_1 = \int_0^t \nu_s ds \ , X_2=Z](img/78c8b1e2144b8f71f4f5d88a3621625e.png)。

模拟方案现在变成了

![\begin{array}{rcl} x_t &=& x_0+a(t) -\frac{1}{2}X_1 + \frac{\rho\kappa}{\sigma}X_1+\sigma(t) X_2 \nonumber \\\sigma²(t)&=&(1-\rho²)X_1 \nonumber \\a(t)&=&(r_t-q_t)t+\frac{\rho}{\sigma}\left( \nu_t-\nu_0-\kappa\theta t \right)\end{array}](img/9abcbc08578a7594631e2893d55544e2.png)

或者用转换后的随机变量表示

![\begin{array}{rcl} Y_1 =h_1(X_1,X_2) &=& x_0+a(t)-\frac{1}{2}X_1 + \frac{\rho\kappa}{\sigma}X_1+\sqrt{\left(1-\rho²\right)X_1}X_2 \nonumber \\ Y_2=h_2(X_1,X_2)&=& X_1 \nonumber\end{array}. ](img/c230689e5a6bace646eaa6ab0e27981a.png)

让 ![phi(x_1)](img/607cb35ad5e19ff578fdbbd4e617bdd7.png) 成为 ![X_1](img/1db0a764a9aadca3989c631bd0a5fef2.png) 的密度函数

![\phi(x_1)=\frac{2}{\pi}\int_0^\infty \cos ux_1 \mathrm{Re}(\Phi(u))\mathrm{d}u](img/fca80341c360f103a604586749044e10.png)

并且 ![X_2](img/143c44d06619ea584f5e40cf47d21c85.png) 根据定义遵循正态分布。![X_1, X_2](img/0820147029a025c055ff21d510e92ea0.png) 的联合概率密度函数为

![f\left( \begin{matrix} x_1 \\ x_2 \end{matrix}\right)=\phi(x_1) \frac{1}{\sqrt{2\pi}}e^{-\frac{x_2²}{2}}](img/0194f06c261d4782d12ee9553e1bf3ed.png)

通过

![\begin{array}{rcl}f\left(h^{-1}(y)\right)&=&f\left(\begin{matrix}y_2 \\ \frac{1}{\sqrt{\left(1-\rho²\right)y_2}}\left(y_1-x_0-a(t)+\frac{1}{2}y_2-\frac{\rho\kappa}{\sigma}y_2\right)\end{matrix}\right)  \nonumber \\  \left|\det \left( \frac{\partial h^{-1}_i(y)}{\partial y_j} \right)\right| &=& \frac{1}{\sqrt{\left(1-\rho²\right)y_2}}  \end{array}.](img/e09ad5419d77b32ebfb9edffa87f1251.png)

这导致了 Fokker-Planck 方程的半解析解，因为根据定义 ![p(x_t,t \mid \nu = \nu_t)](img/101b0fc5df95d5209d689ffcfffb6db2.png) 是 ![Y_1](img/7a7aaee8206ca6fdf1f140cc29a465ac.png) 的分布密度函数，它由以下给出

![p(x_t,t \mid \nu = \nu_t) = \int_0^\infty \mathrm{d}y_2 p(y_1, y_2)\mid_{y_1=x_t} = \int_0^\infty \mathrm{d}y_2 \left[f\left(h^{-1}(y)\right)\left|\det \left( \frac{\partial h^{-1}_i(y)}{\partial y_j} \right)\right| \right]_{y_1=x_t}](img/30818ad101b0f674c0b63d908b613d37.png)

对 ![y_2](img/ec1ac6fd3be365487b52e785be175352.png) 进行积分，例如使用 Simpson 积分法和 Cornish-Fisher 扩展，这给出了积分上限截断的上界。

下面的等高线图显示了 Heston 模型的概率密度函数，用一些示例参数化。

![绘图](https://hpcquantlib.wordpress.com/wp-content/uploads/2014/02/plot.png)

![\begin{array}{|c|c|c|c|c|c|c|c|c|} \hline {\rm 参数} & x_0 & \nu_0 & r & q & \kappa & \theta & \sigma & \rho \\ \hline \hline  a & 4.6052 & 0.4 & 5\% & 2.5\% & 1.0 & 0.4 & 0.8 & -75\%  \\ \hline  b & 4.6052 & 0.4 & 5\% & 2.5\% & 1.0 & 0.4 & 0.8 & \ \ 75\%  \\ \hline  c & 4.6052 & 0.4 & 5\% & 2.5\% & 1.0 & 0.4 & 0.4 & -75\%  \\ \hline  d & 4.6052 & 0.4 & 5\% & 2.5\% & 1.0 & 0.4 & 0.4 & \ \ \ \ 0\%  \\ \hline  \end{array}](img/2d7094c664a4fb63528d7fe90e0d74c2.png)

示例代码可在[此处](http://hpc-quantlib.de/src/hestonpdf.zip)获取，并依赖即将推出的 QuantLib 版本 1.4。

[1] M. Broadie, Ö. Kaya，[随机波动性和其他仿射跳跃扩散过程的精确模拟](http://finmath.stanford.edu/seminars/documents/Broadie.pdf)

[2] K. Spanderen，[Heston 模型的概率分布，第 I 部分](https://hpcquantlib.wordpress.com/2014/02/04/probability-distribution-of-the-heston-model-part-i/)

[3] R.U. Seydel，[计算金融工具，第 86 页](http://www.springer.com/mathematics/quantitative+finance/book/978-1-4471-2992-9)
