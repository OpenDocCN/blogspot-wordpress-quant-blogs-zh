<!--yml
category: 未分类
date: 2024-05-13 00:16:08
-->

# VPP Pricing II: Mixed Integer Linear Programming – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2011/06/23/vpp-pricing-ii-mixed-integer-linear-programming/#0001-01-01](https://hpcquantlib.wordpress.com/2011/06/23/vpp-pricing-ii-mixed-integer-linear-programming/#0001-01-01)

The next two steps are defining a simple VPP contract (or a simplified gas-run power plant) and setting up a mixed integer linear programming optimization (MIP) to calculated the intrinsic value and an upper bound for the extrinsic value based on a Monte-Carlo simulation and assuming *perfect foresight*. The third step outlined in the next part will then be the “exact” pricing of the extrinsic value using dynamic programming and finite difference methods.

The set-up of the simplified gas-run power plant is similar to the one explained in chapter 4.2.3 of the text-book [1]. In general the power plant has three power output level:

*   Plant is off, ![P=0](img/e6a39763349325e64a2cb1f56a703d1a.png)
*   Generation at minimum load ![P=P_{min}](img/361e4208ab739b5579f6bc36a0e591c8.png)
*   Generation at maximum load ![P=P_{max}](img/c8590c99e43dac221a1bc4d9c0276ad2.png)

The power plant has a fixed efficiency rate

![\zeta=\frac{MWh Power Output}{MWh Heat}](img/11c8673ee7ddbae40bfb3120a80a1a61.png).

Ramp rates will be neglected, but the power plant has a minimum uptime ![t_{up}](img/ce9f2d695269ddc536f87667a8fb2f8c.png) and a minimum downtime ![t_{down}](img/e7fa3dd6aa07bfc2b8f8a6ffd6b98c7d.png). The start-up costs are given by a fixed start-up cost ![\eta](img/3d744e5faf1efbb1fd86f7d17ef67fec.png) (in €) and the price of the gas needed to produce the start-up heat ![\theta](img/7f8a6418866b970be4b223f5ebe39ad9.png) (in MWh).

The mixed integer linear optimization is running in one hour blocks and is using three decision variables per hour ![i](img/1c6d35059c23d515f36289e414c54889.png). The binary decision variable ![\beta_i](img/f2008920bbe7574f365e536c5c00afcc.png) is true if the power plant is running at minimum load ![P_{min}](img/4cf540f7f38835a5cb32e13d99d585f0.png) or at maximum load ![P_{max}](img/d2203289f04e1c265751ea6d6f79ba08.png) and ![\beta_i](img/f2008920bbe7574f365e536c5c00afcc.png) is false if the plant is off. The real decision variable ![0\le s_i \le 1](img/428553899a59a14cdcf7682694338d9c.png) is equal to one if the plant is started in hour ![i](img/1c6d35059c23d515f36289e414c54889.png), which is implied by the following constraint

![\beta_i - \beta_{i-1} \le s_i](img/6f53e5243ea4d4cbea0e929bfeb0c1f9.png).

The minimum up-time ![t_{up}](img/ce9f2d695269ddc536f87667a8fb2f8c.png) and the minimum down-time ![t_{down}](img/e7fa3dd6aa07bfc2b8f8a6ffd6b98c7d.png) is a consequence of the constraints

![\begin{array}{rcl} \beta_i &\ge& \sum_{t=i-t_{up}+1}^{t=i} s_t \\[7pt] \beta_i &\le& 1-\sum_{t=i+1}^{t=i+t_{down}} s_t \end{array}](img/6c9ce869fd21ff4f135816f050204369.png)

The real decision variable ![0\le \gamma \le 1](img/d16f3542048d3bf7b4da8f1efe4aff93.png) is equal to one if the power plant is running at maximum load ![P_{max}](img/d2203289f04e1c265751ea6d6f79ba08.png) and zero if the power plant is either running at minimum load ![P_{min}](img/4cf540f7f38835a5cb32e13d99d585f0.png) or if the plant is off, that means

![\beta_i \ge \gamma_i](img/67d4b7a3c2812333cd95c006dfb8a868.png)

Let ![P_i](img/851eb93aff1d491fde0bc5e9c238bae0.png) be the power price, ![G_i](img/91be26c50e785abee2be0623446e67c5.png) be the gas price and ![CO_2^i](img/45bef925de0593fd06b00a157f185de8.png) be the carbon dioxide price at hour ![i](img/1c6d35059c23d515f36289e414c54889.png). The objective function is then given by

![P\& L = \sum_{t=1}^N\left[\left(\gamma_iP_{max} + P_{min}(\beta_i-\gamma_i)\right) \left(P_i - \frac{G_i+CO_2^i}{\zeta}\right) - s_i\left(\eta + \theta (G_i+CO_2^i)\right)\right]](img/a23fead6eabe08004bb479b6923100fd.png)

For a one year span the problem consists of ![3\cdot 365 \cdot 24 = 26280](img/ff4a69ed3a1ab70bb588449fe95ea4c1.png) decision variables ![\{\beta_i, \gamma_i, s_i\}](img/658c980af94e43651309f3213617e615.png) and ![4 \cdot 365\cdot 24 = 35040](img/79d5ec4d1607f2d08177de184550406d.png) constraints. This comparable small problem can be solved using e.g. the [Gnu Linear Programming Kit](http://www.gnu.org/software/glpk/) (GLPK). For an overview on open source linear/mixed integer programming solver see [2].

The model parameters and the example forward curves are outlined in the previous entry [VPP Pricing I](https://hpcquantlib.wordpress.com/2011/06/13/vpp-pricing-i-stochastic-processes-partial-integro-differential-equation/). The diagram below shows the intrinsic value and the upper bound for the total value (intrinsic plus extrinsic value) based on Monte-Carlo, perfect foresight and MIP for different  power plant efficiencies ![\zeta](img/bb875f3aec94dd3d714f429e921bcd14.png). The parameters of the VPP contract are given by

![t_{up}=t_{down}=2h, P_{min}=8MW, P_{max}=40MW, \eta=300 EUR, \theta=20MWh](img/dd948e6f4a925165406d8c5576662879.png),

the (fixed) carbon dioxide price is 3.0€ per MWh heat. [](https://hpcquantlib.files.wordpress.com/2011/06/plot13.png) [![](img/b9378345b8b9ef774028b4394b6023c3.png "plot")](https://hpcquantlib.files.wordpress.com/2011/06/plot14.png)

The source code is available [here](http://hpc-quantlib.de/src/vpp2.zip). It depends on [GLPK](http://www.gnu.org/software/glpk) and the latest [QuantLib](http://www.quantlib.org/) version from the [SVN trunk](http://sourceforge.net/p/quantlib/code/HEAD/tree/) or the next QuantLib 1.2 release.

It is now quite easy to add and price time-integral constraints, e.g. the following constraint restricts the number of starts within a year to be less than or equal to a given number

![\sum_{t=1}^N s_i \le \#Starts](img/16fa6e6079f9c3086db6f18aa357237a.png).

The following diagram shows the results for ![\#Starts \le 25](img/3255bc1367b968ade02fefd2b18a0194.png) and a minimum load ![P_{min}=25MW](img/4a7694c1e7cea64dff3f7670e2fd3093.png).

[![](img/270f6f938e8ffa4dd68a1dced7f3b2f2.png "plot")](https://hpcquantlib.files.wordpress.com/2011/06/plot10.png)

The source code is available [here](http://hpc-quantlib.de/src/vpp3.zip). It depends on QuantLib 1.1 and if  you want to generate the plot directly from the C++ program you’ll also need [R](http://www.r-project.org/), [RCPP](http://cran.r-project.org/web/packages/Rcpp/index.html) and [RInside](http://cran.r-project.org/web/packages/RInside/index.html).

[1] M. Burger, B. Graeber, G. Schindlmayr, Managing Energy Risk, ISDN 978-0-470-ß2962-6

[2] S. R. Thorncraft, [Evaluation of Open-Source LP Optimization Codes in Solving Electricity Spot Market Optimization Problems.](http://www.ceem.unsw.edu.au/content/userDocs/stu-ORMMES06_Benchmarking_20060610_FINAL_CEEM.pdf)