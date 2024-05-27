<!--yml

类别：未分类

日期：2024-05-18 15:17:38

-->

# 及时投资组合：商品指数估算器

> 来源：[`timelyportfolio.blogspot.com/2011/05/commodity-index-estimators.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/05/commodity-index-estimators.html#0001-01-01)

在本文中，我将展示我第一次尝试使用商品指数替代品。 regular 读者知道我在尝试向可能没有资源支付数据的用户展示各种技术时感到沮丧。我已经用美国 10 年期国债总回报系列作为我的债券代理取得了良好的结果，但到目前为止，我还没有找到一个免费且易于获得的替代商品指数。

PPI 不是实时的，但可能提供一个好的 1 个月滞后代理，用于商品指数。 如果我们要使用

[来自圣路易斯联邦储备银行 FRED 系统的 PPI 数据](http://research.stlouisfed.org/fred2/categories/31)

，我可以接近，但我不知道它是否足够接近，直到进一步的系统测试。

R 代码：

需要（性能分析）

需要（量化模块）

#获取符号（"NAPMPRI"，来源="FRED"）#加载 ISM 制造业价格

获取符号（"PPIACO"，来源="FRED"）#加载 PPI 所有商品

获取符号（"PPICRM"，来源="FRED"）#加载 PPI 粗略进一步处理

获取符号（"PPIIDC"，来源="FRED"）#加载 PPI 工业

#不幸的是，无法为专有 CRB 数据找到替代品

#从 csv 文件获取数据系列

CRB<-as.xts（读取.csv（"spxcrbndrbond.csv"，行名=1）[，2]）

#我的 CRB 数据是月底；可以更改，但 R 中更有趣

CRB<-to.monthly（CRB）[，4]

CRB 指数<-as.Date（CRB 指数）

#NAPMPRI_change<-ROC（NAPMPRI，1）

PPIACO_change<-ROC（PPIACO，1）

PPICRM_change<-ROC（PPICRM，1）

PPIIDC_change<-ROC（PPIIDC，1）

#将所有变化率系列与 CRB 1 个月滞后（向前移动）结合，以考虑 PPI 延迟

CRBandPPI<-合并（CRB 滞后（k=1），PPIACO_change，PPICRM_change，PPIIDC_change）

列名（CRBandPPI）<-c（"CRB"、"PPI 所有商品"、"PPI 粗略进一步处理"、"PPI 工业"）

图表.累积回报（CRBandPPI，主="通过 PPI 的 CRB 估算器"，图例.位置="顶部左")

图表.累积回报（CRBandPPI["1990::"]，主="自 1990 年以来通过 PPI 的 CRB 估算器"，图例.位置="顶部左")

图表.相关性（CRBandPPI，主="通过 PPI 的 CRB 估算器"）

图表.相关性（CRBandPPI["1990::"]，主="自 1990 年以来通过 PPI 的 CRB 估算器"）
