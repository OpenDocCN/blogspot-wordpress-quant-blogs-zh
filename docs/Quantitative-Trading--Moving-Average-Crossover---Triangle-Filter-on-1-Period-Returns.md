<!--yml

类别：未分类

date: 2024-05-12 18:57:24

-->

# 量化交易：移动平均交叉=1 期回报的三角形滤波器

> 来源：[`epchan.blogspot.com/2014/09/moving-average-crossover-triangle.html#0001-01-01`](http://epchan.blogspot.com/2014/09/moving-average-crossover-triangle.html#0001-01-01)

许多使用技术分析的交易员喜欢将移动平均交叉作为动量指标。他们计算价格的短期移动平均减去长期移动平均，如果这一指标刚刚转为正值，则做多；如果它转为负值，则做空。这看起来足够直观。然而，不那么明显的是，移动平均交叉不过是最近平均复合回报的一个估计。

但是，当你可能正想放弃这个指标，转而使用平均复合回报时，可以证明移动平均交叉也是 1 期回报的一个三角形滤波器。（在信号处理中，三角形滤波器是一组权重，施加于时间序列，随时间增加，直到某个点，然后随时间减少，直到现在。参见本文末尾的图表。）这种解释为什么有趣？这是因为它使我们考虑其他更复杂的滤波器（如最小二乘、卡尔曼或小波滤波器）作为可能的动量指标。与我以前

[研讨会](http://epchan.com/workshops)

参与者 Alex W. 受到了启发

[论文](http://www.lyxor.com/fileadmin/_fileup/lyxor_wp/document/51/files/assets/downloads/publication.pdf)

由 Bruder

等人

，我们将在下面给出推导过程。

===

首先，请注意，我们将计算的是以对数价格 y 为基础的移动平均值，而不是原始价格。从价格到对数价格的转换当然不会损失或增加信息量，但这将使我们的分析成为可能。（确切的交叉时间，尽管如此，将取决于我们使用价格还是对数价格。）如果我们用 MA(t, n1) 来表示在时间 t 结束时 n1 个对数价格的移动平均值，那么移动平均值交叉点为 MA(t, n1) - MA(t, n2)，假设 n1 < n2。根据定义，

MA(t, n1)=(y(t)+y(t-1)+...+y(t-n1+1))/n1

MA(t, n2)=(y(t)+y(t-1)+...+y(t-n1+1)+y(t-n1)+...+y(t-n2+1)/n2

MA(t, n1)-MA(t, n2)

=[(n2-n1)/(n1*n2)] *[y(t)+y(t-1)+...+y(t-n1+1)] - (1/n2)*[y(t-n1)+...+y(t-n

=[(n2-n1)/n2] *MA(t, n1)-[(n2-n1)/n2]*MA(t-n1, n2-n1)

=[(n2-n1)/n2]*[MA(t, n1)-MA(t-n1, n2-n1)]

如果我们把 MA(t, n1) 视为对数价格在时间区间 [t-n1+1, t] 中间点 (n1-1)/2 的近似值，而 MA(t-n1, n2-n1) 视为对数价格在时间区间 [t-n1, t-(n2-n1)] 中间点 (n2-n1-1)/2 的近似值，那么 [MA(t, n1)-MA(t-n1, n2-n1)] 是对 n2/2 期间总回报的一个近似。如果我们把这个总回报写成平均复合增长率 r 乘以期间 n2/2，我们得到

MA(t, n1)-MA(t, n2) ≈ [(n2-n1)/n2]*(n2/2)*r

r ≈ [2/(n2-n1)]*[MA(t, n1)-MA(t, n2)]

正如上面论文中方程 4 所示。（注意那篇论文中 n1 和 n2 的角色是相反的。）

===

接下来，我们将说明为什么 MA 交叉也是一个 1 期回报的三角形滤波器。通过将 t 固定为 0，简化记号，

MA(t=0, n1)

=(y(0)+y(-1)+...+y(-n1+1))/n1

=(1/n1)*[(y(0)-y(-1))+2(y(-1)-y(-2))+...+n1*(y(-n1+1)-y(-n1))]+y(-n1)

将从 t-1 到 t 的回报写为 R(t)，这变为

MA(t=0, n1)=(1/n1)*[R(0)+2*R(-1)+...+n1*R(-n1+1)]+y(-n1)

同样，

MA(t=0, n2)=(1/n2)*[R(0)+2*R(-1)+...+n2*R(-n2+1)]+y(-n2)

所以 MA(0, n1)-MA(0, n2)

=(1/n1-1/n2)*[R(0)+2*R(-1)+...+n1*R(-n1+1)]

-(1/n2)*[(n1+1)*R(-n1)+(n1+2)*R(-n1-1)+...+n2*R(-n2+1)]

+y(-n1)-y(-n2)

请注意上述最后一行只是从-n2 到-n1 的总累积回报，可以写作

y(-n1)-y(-n2)=R(-n1)+R(-n1-1)+...+R(-n2+1)

因此我们可以将那个吸收进此表达式之前的部分。

MA(0, n1)-MA(0, n2)

=(1/n1-1/n2)*[R(0)+2*R(-1)+...+n1*R(-n1+1)]

-(1/n2)*[(n1+1-n2)*R(-n1)+(n1+2-n2)*R(-n1-1)+...+(-1)*R(-n2+2)]

=(1/n1-1/n2)*[R(0)+2*R(-1)+...+n1*R(-n1+1)]

+(1/n2)*[(n2-n1-1)*R(-n1)+(n2-n1-2)*R(-n1-1)+...+R(-n2+2)]

我们可以看到从 t=-n2+2 到-n1 的 R 的系数形成了一个正斜率的三角形左侧，而从 t=-n1+1 到 0 形成了一个负斜率的三角形的右侧。下面的图表（点击放大）显示了随时间变化的系数，n2=10，n1=7，当前时间为 t=0。最右边的点是 R(0)的权重：从 t=-1 到 0 的回报。

证明完毕。现在我希望你准备好继续学习小波滤波器！

P.S. 能够用一个简单的 Matlab 程序检查上面那些乱七八糟的代数式的正确性真是太好了！

===

**新服务公告**

我们公司 QTS 资本管理最近推出了一项

[外汇管理账户](http://epchan.com/accounts)

程序。它使用我们在过去三年中在基金中成功交易的均值回归策略之一，尽管市场波动性较低，但它仍然表现强劲。管理账户的好处是，客户始终拥有其资金的完全所有权和控制权，并且可以决定他们舒适的杠杆水平。与某些海外 FX 运营商不同，QTS 是一个受国家期货协会和商品期货交易委员会监管的 CPO/CTA。

===

**研讨会更新**

读者可能对我的下一个研讨会系列感兴趣，该系列将于 11 月 3 日至 7 日在伦敦举行。请点击底部的链接

[此页面](http://epchan.com/workshops)

for information.

===

关注我 Twitter: @chanep
