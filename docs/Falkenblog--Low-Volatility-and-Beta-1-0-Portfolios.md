<!--yml

类别：未分类

日期：2024-05-12 21:20:54

-->

# Falkenblog：低波动和 Beta 1.0 投资组合

> 来源：[`falkenblog.blogspot.com/2010/09/low-volatility-and-beta-10-portfolios.html#0001-01-01`](http://falkenblog.blogspot.com/2010/09/low-volatility-and-beta-10-portfolios.html#0001-01-01)

低波动率投资组合针对波动率或 beta 低的股票。我发现使用 3-4 因子模型来最小化方差会产生最低的波动率投资组合，但是这种方法的优势是年化波动率为 2-4%，鉴于大多数投资者不理解因子分析，仅仅选择波动率或 beta 最低的股票能得到一个相当不错的近似值，同时也保留了更多的可读性。我昨天提出的另一种方法是 beta 1.0 投资组合。低波动率和 beta 1.0 方法的区别如下：

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj9MZ31hkVcDoDBKb0t5K_Mzx59xbqYjfsRIniJbFQ6XpxhZVCfjmLeE0sv-Enfzcz-vnovtBc79nAl9QprIIz7bIoyjjAVruEfZxBVaJfTwElREL_Bdm4hcOy6ifksd080Qjgwew/s1600/betadist.jpg)

Beta 1.0 只是选择那些 beta 最接近 1.0 的股票。也就是说，每 6 个月我估算一次所有美国上市股票的 beta 值(约 2500 只股票)，并监测回报，将合并或退市股票重新纳入指数。数据来自 CRSP，Compustat 和 Bloomberg，当过去构建时，包含了已死亡公司，所以这是一个无生存偏差的数据集。1997 年之前，我使用月回报，之后则使用每日回报来估算 beta 值。beta 1.0 投资组合实时的投资组合 beta 值非常接近 1.0（大约为 1.05）。低 beta 投资组合仅仅每 6 个月选择最低的 100 个 beta 股票（深蓝色圆圈），做同样的事情。

他们的平均回报之间的差异如下：

**自 1962 年来美国的回报**

|   | Beta1.0 | Low Beta | S&P500 |
| --- | --- | --- | --- |
| 平均年度几何回报 | 11.4% | 10.4% | 9.3% |
| Ann StDev | 17.4% | 13.1% | 15.1% |
| Beta | 1.04 | 0.58; |   |

如果人们主要关心 beta，这仍然是商学院的主导观点，他们应该投资于低波动率或低 beta 投资组合。您可以在大约相同的回报率下获得更低的“风险”，甚至还可能略高。仅仅剔除高波动率股票也会带来更高的回报，这就是为什么低波动率投资组合，比如

[罗宝](https://www.robeco.com/com/eng/institutional_investors/product_information.jsp?pdstchn=instcom&pfndid=2581&plang=english)

对于试图最大化夏普比率的机构投资者来说，可能会具有吸引力。

注意 beta 1.0 股票的回报略高于低 beta 股票（波动性也略高）。这并不奇怪，因为反常的波动效应通常是高波动性或 beta 股票的大幅表现不佳。从低到中 beta，实际上会获得适度的回报改善。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEghusIjcL6LR7q0nT0rzUn83AnmQGxddAQt_tI8Rjf7zWt9hoseG3PxqMsoVrdaz5JyBGxEWloVXe4TUFj0X59FCUTLia5LyTMVu-u2wn5Jh41_nzXEk8_zAJ8lIpM30a2xPypfMQ/s1600/histret.jpg)

上面我们看到的是

相对

回报，并且相对回报分布与β为 1.0 的投资组合相比事实上更丰富。如果你的基准是指数，那么‘低风险’就是有风险的。这在 2000 年的科技泡沫时期尤为突出（下图），当高β股大幅跑赢其他股票时，任何凑巧投资低β股票的人可能都失业了（除非他们是沃伦·巴菲特，他在科技股的表现不佳中幸存下来）。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhJthqlMilBaLOELmMhDnpPpxytTYCxoHOiDhtKHrhpp11c60CPl5WeP48fLdQ8OohAo4n0qOjtckcOG5P3aF8UcqOxheXZncWu7lCSOxxqu3w7nG0DvUZ-6-H5gvwbDG4i2HgwKA/s1600/bubble.jpg)

结论是，如果你关心相对表现，那么β为 1.0 的投资组合是低波动率方法的一个明智选择，它最大的优势是避免那些从长期来看在每个主要股票市场上都表现可怕的彩票股票。

现在你可能会说，“什么傻瓜会用标普相对测量风险？”我难道只在乎我的消费，我的财富？我会说，大多数人更关心相对回报而不是绝对回报。CAPM 先驱比尔夏普为养老金基金提供咨询，评估资产管理人员，并声明他的首要目标是“我希望一个产品相对于某个基准来定义”（see

[塔努斯](http://www.amazon.com/Investment-Gurus-Wealth-Managers-Selection/dp/0132607204)

)。基金经理肯尼斯·费舍的书

[只有三个问题是重要的](http://www.onlythreequestions.com/)

在风险旁边的指数，它有“见基准测定。”当被问及小股票的风险性质时，

[尤金·法玛指出](http://www.dfaus.com/2009/05/an-interview-with-eugene-fama.html)

1980 年代，“小股票处于萧条状态”，默顿·米勒注意到，常胜基金公司的小盘股组合在连续 6 年以来都表现不如标普 500 指数，这证明了它的风险。但与 1970 年代相比，较小的股票实际上获得了可比的总回报，并且相对无风险利率而言，在 1980 年代获得了更高的回报。只是相对于它们的基准（标普 500 指数，大盘股）它们表现“糟糕”，这凸显了甚至法玛和米勒在风险方面的实际直觉都是相对的，这些人是标准模型的冠军。不用说其他人，尤其是基金经理，都非常清楚他们的年度和生涯相对于标普 500 的表现。

从投资专业人士和学者的角度来看，风险是相对于基准的回报变化，这种假设似乎是合理的。这一事实对于进行最佳投资具有几个重要的影响，无论你是否采取了这种方式。
