<!--yml

类别：未分类

日期：2024-05-12 20:27:52

-->

# Falkenblog：杠杆交易所交易基金突显波动性需求

> 来源：[`falkenblog.blogspot.com/2012/06/levered-etfs-highlights-volatility.html#0001-01-01`](http://falkenblog.blogspot.com/2012/06/levered-etfs-highlights-volatility.html#0001-01-01)

[PowerShares 推出了一对 ETN](http://finance.yahoo.com/news/powershares-rolls-inverse-leveraged-japanese-150033810.html)

PowerShares 推出了两款与日本政府债券期货相关的 ETN，3 倍日本政府债券期货 ETN（JGBT）和 3 倍反向日本政府债券期货 ETN（JGBD）。政府债券通常被认为风险较低，但为了产生足够的需求，似乎需要将其杠杆化，使其风险高到值得利息。我怀疑 10 年后，任何东西都会有 2 倍和 3 倍的衍生品在流动交易所上可交易。

现在，需求的一个原因是，像 401(k)这样的账户会限制杠杆，因此杠杆是隐含在 ETF 中的，而非显性的。这是杠杆限制的一个大问题，因为这种方式的杠杆总是可以被操纵，而且没有简单的解决办法。

但我怀疑主要原因更基本：人们喜欢波动性，所以随着波动性的增加，需求也会增加。现在，在大多数表述中，风险资产的需求大致像这样决定。

首先，最大化风险资产的权重，其中 w 是投资者配置给风险资产的投资组合的一部分：

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh2hlFrQsti6a5xuRSjSovay3br34GRLAUISVD27HKT_XzWt6NSHJiIVw4coVE2Feh-ZRnQKSzf6i2_dlBZhJD3_mNkikqYyHQWn0oDRvPK2G-jB8v-HnKQ9tnIcfHTdow3qecOjQ/s1600/Eqn001.gif)

按照定义，风险资产具有高斯分布，无风险资产是一些常数。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi0WMTo7WYDl0gEl0GXCYllnFOHpYqzJlbgXis_dn6jIwbHpwOZxGuXvxicvTaysgK6IeSaQUIpUHS6bRnPPmA4gGmiJqTGNdsrhNWfLb9lNa77N0iTrxZ4xxjVjy6BAOi4vwf78Q/s1600/Eqn002.gif)

对 w 求导并令其等于零，得到了熟悉的风险资产需求。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjN7t5j7OfhZxUBNXg0LGk6-GyuFmjwAi-vJuqg8iJc-zdcALgh4cxnuHJb-TRgENoL83-gXqJsCJt2M9cJE1nzDbm_4ULkM76FCeqk8E347e-2dVViMzjoLJC4t08r9JIflOD8Jw/s1600/Eqn003.gif)

这意味着它与预期收益呈线性关系，并与其方差呈反向关系。增加杠杆会使收益（分子）增加 X 倍，方差（分母）也增加 X 倍。

²

，因此比例变化了 1/x。按照这个理论，最优需求会下降

*parri passu*

杠杆比例变化；杠杆不应影响实际需求，因为它被冲刷掉了。

然而，在实践中，情况并非如此。 我不确定发生了什么，但我认为其中一部分是量子效应，投资者对某事情不感兴趣，直到它能产生足够的回报。也就是说，大多数投资者基本上对他们的日本债券敞口为零。 如果他们有机会赚取 200 美元，许多投资者会拿出 1000 美元，但对拿出 1000 美元赚取 100 美元的兴趣要少得多。 当然，他们总是可以通过杠杆自行进行头寸，但那是另一种复杂的层面，会产生各种运营风险，比如税收问题和保证金调用问题。
