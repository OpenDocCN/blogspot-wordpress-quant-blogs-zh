<!--yml

分类：未分类

日期：2024-05-18 15:18:11

-->

# 及时组合：美国货币政策限制的新宠测试

> 来源：[`timelyportfolio.blogspot.com/2011/04/new-favorite-test-of-us-monetary-policy.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/04/new-favorite-test-of-us-monetary-policy.html#0001-01-01)

经过一些深思熟虑后，我发现我的[死亡螺旋警告图](http://timelyportfolio.blogspot.com/2011/03/death-spiral-warning-graph.html)可以通过分离美国 10 年收益率的预期通胀成分来改进，该收益率由美国 10 年收益率-美国 10 年 TIP 收益率提供。不幸的是，它更准确地揭示了美国联邦储备银行积极货币政策的成本，并且我认为对这种政策的限制进行了更严重的评估。

我们所经历的增长似乎比简单的标普 500 图表所显示的要短暂和虚假得多。

R 代码：

需要(quantmod)

需要(性能分析)

注释：来自圣路易斯联邦储备银行(FRED)的数据

获取符号("DGS10"，源="FRED") #加载 10 年国债

获取符号("DFII10"，源="FRED") #加载 10 年 TIP 的真实回报

获取符号("DTWEXB"，源="FRED") #加载 US 美元

获取符号("SP500"，源="FRED") #加载 SP500

#新的美联储货币政策限制监控

注释：US10Y TIP 盈亏平衡通胀除以 US 美元

旧宠是 US 10 年名义除以 US 美元

fedpolicytest<-合并((DGS10-DFII10)/DTWEXB,DGS10/DTWEXB)

列名(fedpolicytest)<-c("US10yTIPInflationDivByUSDollar (新宠)","US10yDivByDollar (旧宠)")

图表.TimeSeries(fedpolicytest["2003::2011"],图例.位置="顶部左方",

主标题="美国货币政策测试-伯南克有极限吗？"，颜色集=c("海军蓝","深橄榄绿 3"),y 轴标签=""

事件线条="2008-07-02"，事件标签="2008 年 7 月 2 日"

注释：添加标签以表示新的近期高点

文本(NROW(fedpolicytest["2003::2011"])-15,fedpolicytest[NROW(fedpolicytest),1]+.001,"新高")

注释：以前的高点

abline(h=fedpolicytest["2008-07-02",1],col="navy")
