<!--yml

分类：未分类

日期：2024 年 5 月 12 日 18:48:58

-->

# 计算：DV 超平滑双随机振荡器 | CSSA

> 来源：[`cssanalytics.wordpress.com/2009/09/11/calculation-dv-super-smoothed-double-stochastic-oscillator/#0001-01-01`](https://cssanalytics.wordpress.com/2009/09/11/calculation-dv-super-smoothed-double-stochastic-oscillator/#0001-01-01)

各位好，Catallactic Analysis 的 Corey Rittenhouse 很好地测试了一些使用 S&P500 的 DV 随机指标的策略变化。这种组合策略非常有趣。我给他转发了一个示例电子表格，用于精确计算指标，并在他的网站上发布。[`www.catallacticanalysis.com/strategytests/differentstrategyvariationsDVSSDStochastic.php`](http://www.catallacticanalysis.com/strategytests/differentstrategyvariationsDVSSDStochastic.php)

计算双随机振荡器的步骤如下：

1) 获取包括最近 10 天的高、低和收盘数据的随机指标，计算方法为（今日收盘价 - 最近 10 天的 HLC 最小值）/（最近 10 天的 HLC 最大值 - 最近 10 天的 HLC 最小值）

2) 获取第 1 步中计算的数字的随机指标，即（随机指标 - 最近 10 天的随机指标最小值）/（最近 10 天的随机指标最大值 - 最近 10 天的随机指标最小值）

3) 对此结果进行第一次平滑，计算 3 个周期（天）的平均值

4) 取第一次平滑值的 .85 倍 + 前一天的平滑值的 .15 倍，得到最终结果

所得到的随机指标平滑且对 S&P500 中发生的周期非常敏感。祝好运！
