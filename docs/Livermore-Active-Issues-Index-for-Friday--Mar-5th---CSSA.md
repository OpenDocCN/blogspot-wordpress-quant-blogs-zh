<!--yml

分类：未分类

日期：2024-05-12 18:34:45

-->

# 3 月 5 日周五的 Livermore 活跃问题指数 | CSSA

> 来源：[`cssanalytics.wordpress.com/2010/03/05/livermore-active-issues-index-for-friday-mar-5th/#0001-01-01`](https://cssanalytics.wordpress.com/2010/03/05/livermore-active-issues-index-for-friday-mar-5th/#0001-01-01)

2010 年 3 月 8 日 1:29 pm

David,

在你的上一篇文章中，如果你使用移动平均的 ROC，结果似乎更好

原因 – 5 天的 ROC 容易受到成交量突然变化的影响，但 5 天的 MA 要平滑得多。

你有什么想法吗

以下是我的代码

//设置系统变量

AvgVol5 = MA(V, 5);

MA200 = MA(C, 200);

//5dROC SPY 体积>0，V 0 AND V 0 AND V < Ref(V,-1);

Sell = 0;

Short=0;

Cover=0;
