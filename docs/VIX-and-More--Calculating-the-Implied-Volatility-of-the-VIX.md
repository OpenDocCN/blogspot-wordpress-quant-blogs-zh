<!--yml

分类：未分类

日期：2024-05-18 17:53:09

-->

# VIX 和更多：计算 VIX 的隐含波动率

> 来源：[`vixandmore.blogspot.com/2009/04/calculating-implied-volatility-of-vix.html#0001-01-01`](http://vixandmore.blogspot.com/2009/04/calculating-implied-volatility-of-vix.html#0001-01-01)

今天早些时候，一位读者对 VIX 的隐含波动率提出了一个很好的观察和问题：

> *“我注意到当前 ATM 七月期权的 IV 为 50，而 VIX 本身是 42。这对我来说似乎很疯狂，因为 VIX 的 IV 是二阶导数，应该比 VIX 本身大得多…”*

大多数数据源的问题在于，它们假设现金/现货 VIX 是[VIX 期权](http://vixandmore.blogspot.com/search/label/VIX%20options)的底层，而不是使用[VIX 期货](http://vixandmore.blogspot.com/search/label/VIX%20futures)，后者更准确地近似 VIX 期权的底层（技术上是一个[方差互换](http://en.wikipedia.org/wiki/Variance_swap)。)

我不能为每个数据提供商背书，但我相信网上大多数受高度评价的期权网站都是使用现金/现货 VIX 来计算 VIX 隐含波动率，所以由此产生的计算结果受到现金/现货 VIX 与 VIX 期货之间的差异的影响。

有几个期权数据源为可期权证券发布专有的平均隐含波动率计算。或许最著名的是来自 iVolatility.com 的“IV 指数平均值”。今天收盘后，[iVolatility VIX IV 指数平均值](http://www.ivolatility.com/options.j?ticker=vix&R=0&x=0&y=0)为 61.38。国际证券交易所有一个类似的计算，使用相同的名称。今天，[ISE 的 VIX IV 指数平均值](http://www.ise.com/WebForm/md_livevol.aspx?categoryId=124&header2=true&menu1=true)收盘价为 64.98。

思考者交易平台为每个月计算一个 IV。对于四月，他们给出的 VIX IV 为 85.71。在 optionsXpress 网站上进行一些插值，我得到四月 ATM 期权的 VIX IV 为 77.12。

在不了解生成这些 VIX IV 计算的模型的详细情况之前，我无法为任何 VIX IV 输出的一致性背书。我很想找到一个使用 VIX 期货作为底层计算 VIX 隐含波动率的来源。我的猜测是上面四个数字中没有采取这种方法。如果有人知道一个基于 VIX 期货发布 VIX IV 计算的来源，我当然很想了解更多。在此之前，我的假设是所有从数据提供商那里得到的 VIX IV 数据都是无效的，基于现金/现货 VIX。
