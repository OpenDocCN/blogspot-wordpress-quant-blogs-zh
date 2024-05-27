<!--yml

类别：未分类

日期：2024-05-12 18:16:09

-->

# 另一个短期趋势指标- DSR (Distribution Skew versus Range) | CSSA

> 来源：[`cssanalytics.wordpress.com/2010/11/01/another-short-term-trend-indicator-dsr-distribution-skew-versus-range/#0001-01-01`](https://cssanalytics.wordpress.com/2010/11/01/another-short-term-trend-indicator-dsr-distribution-skew-versus-range/#0001-01-01)

注意：本周我将在芝加哥参加**NAAIM**会议，并将与我的两位同事一起进行交易系统评估演讲。[`naaim.org/`](http://naaim.org/) 我已安排了整个周的会议，但如果您想见面讨论我们的机构服务，我的一位同事应该会有空。您可以发邮件给我：david@cssanalytics.com 鉴于我目前的行程，我的发布会将会减少。预计我将会在返回后在我们的网站上提供为 NAAIM 准备的一些有趣研究成果。

*-还应该查看**Quanting Dutchman** 最近在交易系统方面做了一些良好的工作/研究，并且还提供了该特定类型的 H、L、C 数组的 Amibroker 代码：[`quantingdutchman.wordpress.com/`](http://quantingdutchman.wordpress.com/)

**DSR**—-在 2400 个 bars 上 SPY 的 CAGR：**14%**

这是一个趋势分布指标，它考虑了高时刻价格的偏度与低时刻价格的偏度与价格区间的关系。实际上，相对于价格区间，两者之间的差异比较大意味着价格上涨的可能性大于下跌。到目前为止，这个指标显示出了成为一个短期趋势指标的很大潜力，有很多可能的应用方式。我将把这部分留给很多老练的读者和博主。指标计算略微复杂：

DSR *differentia*l=  average(  65th percentile (H,L,C, 20-days), 80th percentile  (H,L,C, 20-days)) –  average(  35th percentile (H,L,C, 20-days), 20th percentile  (H,L,C, 20-days))

DSR *raw*=  DSR *differential*/（max(H,L,C, 20-days)-min(H,L,C, 20-days))

**DSR**=（10-day sma of DSR *raw)*的 252 天百分等级
