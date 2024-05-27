<!--yml

类别：未分类

日期：2024-05-18 04:47:10

-->

# 智能交易：使用 J48 决策树分类器动态分配第二天股票或债券的头寸

> 来源：[`intelligenttradingtech.blogspot.com/2010/02/prior-introduction-using-simple-model.html#0001-01-01`](http://intelligenttradingtech.blogspot.com/2010/02/prior-introduction-using-simple-model.html#0001-01-01)

之前使用简单模型来确定基于标普 500 指数和波动率指数的下一周变化并没有看起来那么有希望，尽管希望它使您熟悉了如何使用分类来增强交易决策。如果我们有更好的东西会怎么样？

那么，让我们来看一个使用决策树类型的分类来预测是否要在一天前投资股票或债券的应用。

我们将使用一个非常简单的输入模型刺激来做出决策。

以下将作为输入属性使用。

1) 波动率指数(VIX)一日变化

2) 国债延长到期收益率(TLT)一日变化

3) 标普 500 一日变化

4) 波动率指数(VIX)五日动量

5) 国债延长到期收益率(TLT)五日动量

6) 标普 500 五日动量

波动率指数(VIX)作为波动性的代理来衡量恐惧，这导致（假设地）人们寻求更安全的仪器（债券）。

国债延长到期收益率(TLT)是追踪持有平均到期为 20 年的国债的 iShares Barclays 20+ Year Treas Bond ETF。

标普 500(SPY)是一个追踪通用市场指数：标普 500 的 ETF。

剩余的五日动量属性仅仅是用来大致确定指数在过去五天的动量的名义属性，上升(UP)或下降(DN)。除了输入属性外，我们还增加了一个输出属性，即第二天投资的优秀仪器——标普 500(SPY)或国债延长到期收益率(TLT)(股票或债券)。这就是我们要预测和决定的。训练和测试数据样本来自 2002 年 7 月 31 日至现在的期间。

通过将信息输入 Weka（通过.csv，见之前的教程），我们将选择 J.48 决策树学习器，并使用 90%/10%的训练/测试分割，以便开发一个模型树，该树将根据前一天的输入刺激预测要投资的仪器类别。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjfHCZvDIu2KeCy3Lyol51LhiSXwtkUbCEYqwq57T0ZySoGnb8QUhTfHHS6ovdvLHcP4caq49xHQMQFOqm7Pz_L1FwITe5tSOsOj2LpZRw2BmhvVkvIyGAGZoErA_tVihFOt8j4FA6G4BY/s1600-h/fig1_tree2_raw2.jpg)

图 1. 结果模型决策树

决策树可以从顶部向下阅读，作为基于某些条件做出决策。例如，如果我们遍历最左边的分支，它会给我们以下规则：

如果 5 日标普 500 动量下降(DN)且 1 日国债延长到期收益率(TLT)变化率小于等于 0.91%，且 5 日国债延长到期收益率(TLT)动量上升(UP)且 5 日波动率指数(VIX)动量上升(UP)，则

第二天投资标普 500(SPY)。

我们可以类似地遍历每个分支，以获得一组全面的规则，决定第二天投资什么。

尽管这棵树看起来有点令人望而却步，但如果你能把规则集编程到你喜欢的语言中，对算法来说，把那个模型处理向前就很简单了。

最后，我们想看看预测方案是否比猜测更好或更差。

![图 2. J.48 模型树 90/10 训练/验证结果](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjMxPa_STm5q-cM7cklIDcKnF-ven6TOVUs38iDht2IwVzxVtS5huiJGne7DVOAh2GW_kXuNb5O1gganpouTPZfBmxgc2CckWGjxqgqhmGy9VzmOCHXp7KSJx6h_fETj8YlQTMDRgpi-LY/s1600-h/fig2_results_raw2.jpg)

图 2. J.48 模型树 90/10 训练/验证结果

结果相当不错。利用一个非常简单直观的模型，我们能够以 59%的成功率在 10%的样本外验证集中选择更好的购买工具。同样的方法可以用来在交易系统之间进行选择，只要稍加创新即可。

![图 3. 股票曲线](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgPj9wuNNqr7CI4jbwqTaWnRuyLoFrDr6Ks4pGCF5GOXl2n64Pwi0HkflGNZPwsxHm0PA8Jqt9S7RcwrSjszZSOcxzhT-C8mZoXrWHmjx6skrnTvhIPEcsQ6_L_7kh3WuCyh_VgQnrqljc/s1600-h/fig3_eq_curve.jpg)

图 3. 学习系统与投资类别在样本外数据上的股票曲线比较

最后，我们来看看投资于

1) 我们建模的分类器系统的结果

2) 仅投资 SPY 或 TLT（股票或债券）

3) 各投资一半

请注意，我们的系统终端财富结果仅略微优于其他系统。

所有其他系统。这是一个很好的例子，说明你可能有一个很好的命中率，但净结果的改进只是适中，因为命中率并不考虑大小。此外，由于多次在内外交易中产生的佣金和滑点成本可能会抵消系统性的优势。后来当我们讨论遗传算法时，我们会看到还有许多其他优化方法。

正如往常一样，请务必做好自己的尽职调查，并彻底验证您可能用于自己交易决策的任何结果。
