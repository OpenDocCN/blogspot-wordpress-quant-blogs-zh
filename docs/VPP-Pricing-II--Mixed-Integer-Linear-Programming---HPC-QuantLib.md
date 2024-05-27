<!--yml

类别：未分类

日期：2024 年 05 月 13 日 00:16:08

-->

# 虚拟电厂定价 II：混合整数线性规划 – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2011/06/23/vpp-pricing-ii-mixed-integer-linear-programming/#0001-01-01`](https://hpcquantlib.wordpress.com/2011/06/23/vpp-pricing-ii-mixed-integer-linear-programming/#0001-01-01)

接下来的两个步骤是定义一个简单的虚拟电厂（或简化的燃气发电厂）合同，并设置混合整数线性规划优化（MIP）来计算内在价值和基于蒙特卡罗模拟并假设*完美预见*的外在价值的上限。下一部分中概述的第三步将是使用动态规划和有限差分方法“精确”定价外在价值。

简化燃气发电厂的设置类似于教材 [1] 第 4.2.3 章节中解释的设置。一般来说，发电厂有三个功率输出级别：

+   发电厂关闭时，![P=0](img/e6a39763349325e64a2cb1f56a703d1a.png)

+   发电在最小负荷时 ![P=P_{min}](img/361e4208ab739b5579f6bc36a0e591c8.png)

+   发电在最大负荷时 ![P=P_{max}](img/c8590c99e43dac221a1bc4d9c0276ad2.png)

发电厂有固定的效率率

![\zeta=\frac{MWh 发电量}{MWh 热量}](img/11c8673ee7ddbae40bfb3120a80a1a61.png)。

斜坡率将被忽略，但发电厂有最小正常运行时间 ![t_{up}](img/ce9f2d695269ddc536f87667a8fb2f8c.png) 和最小停机时间 ![t_{down}](img/e7fa3dd6aa07bfc2b8f8a6ffd6b98c7d.png)。启动成本由固定启动成本 ![\eta](img/3d744e5faf1efbb1fd86f7d17ef67fec.png)（以欧元计）和产生启动热量所需的天然气价格 ![\theta](img/7f8a6418866b970be4b223f5ebe39ad9.png)（以 MWh 计）给出。

混合整数线性优化每小时运行一个小时的时间，并且每小时使用三个决策变量 ![i](img/1c6d35059c23d515f36289e414c54889.png)。二进制决策变量 ![\beta_i](img/f2008920bbe7574f365e536c5c00afcc.png) 如果发电厂运行在最小负荷 ![P_{min}](img/4cf540f7f38835a5cb32e13d99d585f0.png) 或者最大负荷 ![P_{max}](img/d2203289f04e1c265751ea6d6f79ba08.png) 时为真，且 ![\beta_i](img/f2008920bbe7574f365e536c5c00afcc.png) 在发电厂关闭时为假。实际决策变量 ![0\le s_i \le 1](img/428553899a59a14cdcf7682694338d9c.png) 在小时 ![i](img/1c6d35059c23d515f36289e414c54889.png) 启动发电厂时为 1，这由以下约束隐含

![\beta_i - \beta_{i-1} \le s_i](img/6f53e5243ea4d4cbea0e929bfeb0c1f9.png)。

最小正常运行时间 ![t_{up}](img/ce9f2d695269ddc536f87667a8fb2f8c.png) 和最小停机时间 ![t_{down}](img/e7fa3dd6aa07bfc2b8f8a6ffd6b98c7d.png) 是约束的结果

![\begin{array}{rcl} \beta_i &\ge& \sum_{t=i-t_{up}+1}^{t=i} s_t \\[7pt] \beta_i &\le& 1-\sum_{t=i+1}^{t=i+t_{down}} s_t \end{array}](img/6c9ce869fd21ff4f135816f050204369.png)

实际决策变量 ![0\le \gamma \le 1](img/d16f3542048d3bf7b4da8f1efe4aff93.png) 等于 1，如果发电厂以最大负载 ![P_{max}](img/d2203289f04e1c265751ea6d6f79ba08.png) 运行，等于 0，如果发电厂以最小负载 ![P_{min}](img/4cf540f7f38835a5cb32e13d99d585f0.png) 运行或者发电厂关闭，即

![\beta_i \ge \gamma_i](img/67d4b7a3c2812333cd95c006dfb8a868.png)

让 ![P_i](img/851eb93aff1d491fde0bc5e9c238bae0.png) 为电力价格，![G_i](img/91be26c50e785abee2be0623446e67c5.png) 为天然气价格，![CO_2^i](img/45bef925de0593fd06b00a157f185de8.png) 为第 ![i](img/1c6d35059c23d515f36289e414c54889.png) 小时的二氧化碳价格。然后，目标函数由以下给出

![P\& L = \sum_{t=1}^N\left[\left(\gamma_iP_{max} + P_{min}(\beta_i-\gamma_i)\right) \left(P_i - \frac{G_i+CO_2^i}{\zeta}\right) - s_i\left(\eta + \theta (G_i+CO_2^i)\right)\right]](img/a23fead6eabe08004bb479b6923100fd.png)

对于一年的时间跨度，问题包含 ![3\cdot 365 \cdot 24 = 26280](img/ff4a69ed3a1ab70bb588449fe95ea4c1.png) 决策变量 ![{\beta_i, \gamma_i, s_i}](img/658c980af94e43651309f3213617e615.png) 和 ![4 \cdot 365\cdot 24 = 35040](img/79d5ec4d1607f2d08177de184550406d.png) 约束。这个相对较小的问题可以使用例如 [Gnu Linear Programming Kit](http://www.gnu.org/software/glpk/) (GLPK) 来解决。有关开源线性/混合整数规划求解器的概述，请参见 [2]。

模型参数和示例前向曲线在前一篇文章 [VPP Pricing I](https://hpcquantlib.wordpress.com/2011/06/13/vpp-pricing-i-stochastic-processes-partial-integro-differential-equation/) 中已经概述。下面的图表显示了基于 Monte-Carlo、完全预见和 MIP 对不同功率发电厂效率 ![\zeta](img/bb875f3aec94dd3d714f429e921bcd14.png) 的内在价值和总价值（内在价值加外在价值）的上限。VPP 合同的参数如下

![t_{up}=t_{down}=2h, P_{min}=8MW, P_{max}=40MW, \eta=300 EUR, \theta=20MWh](img/dd948e6f4a925165406d8c5576662879.png),

（固定的）二氧化碳价格为每 MWh 热量 3.0 欧元。 [](https://hpcquantlib.files.wordpress.com/2011/06/plot13.png) ![](https://hpcquantlib.files.wordpress.com/2011/06/plot14.png)

源代码可在 [这里](http://hpc-quantlib.de/src/vpp2.zip) 获取。它依赖于 [GLPK](http://www.gnu.org/software/glpk) 和来自 [SVN trunk](http://sourceforge.net/p/quantlib/code/HEAD/tree/) 或下一个 QuantLib 1.2 发行版的最新版本 [QuantLib](http://www.quantlib.org/)。

现在添加和定价时间积分约束变得非常容易，例如以下约束限制了一年内启动次数不超过给定数量。

![\sum_{t=1}^N s_i \le \#Starts](img/16fa6e6079f9c3086db6f18aa357237a.png)。

以下图表展示了当 ![#Starts ≤ 25](img/3255bc1367b968ade02fefd2b18a0194.png) 且最小负载为 ![P_{min}=25MW](img/4a7694c1e7cea64dff3f7670e2fd3093.png) 时的结果。

![](https://hpcquantlib.files.wordpress.com/2011/06/plot10.png)

源代码在[这里](http://hpc-quantlib.de/src/vpp3.zip)可获得。它依赖于 QuantLib 1.1，如果你想直接从 C++ 程序生成图表，你还需要[R](http://www.r-project.org/)，[RCPP](http://cran.r-project.org/web/packages/Rcpp/index.html)和[RInside](http://cran.r-project.org/web/packages/RInside/index.html)。

[1] M. Burger，B. Graeber，G. Schindlmayr，Managing Energy Risk，ISDN 978-0-470-ß2962-6

[2] S. R. Thorncraft，[评估开源 LP 优化代码解决电力现货市场优化问题。](http://www.ceem.unsw.edu.au/content/userDocs/stu-ORMMES06_Benchmarking_20060610_FINAL_CEEM.pdf)
