<!--yml

类别：未分类

date: 2024-05-18 04:44:49

-->

# 智能交易：使用 R rle 函数模拟赢/输连续次数

> 来源：[`intelligenttradingtech.blogspot.com/2011/05/simulating-winloss-streaks-with-r-rle.html#0001-01-01`](http://intelligenttradingtech.blogspot.com/2011/05/simulating-winloss-streaks-with-r-rle.html#0001-01-01)

以下脚本允许您根据随机分布模拟赢、输和平局连续运行的样本运行，使用 R 中的运行长度编码函数 rle。相关概率被输入为样本函数中的向量参数。

通过查看交易结果，您可以查看实际的试验序列（以及随之产生的连续次数）。maxrun 返回每次样本运行的最大连续赢、输和平局次数的向量。最后，prop table 提供了从长度为 n 的连续失败到所有交替长度的连续次数转换对的比例表。

示例输出（此处连续损失的最大运行长度为 8）：

100*prop.table(tt)

lt.2

lt.1      1      2      3      4      5      6      7      8

1 41.758 14.298  5.334  1.662  0.875  0.131  0.000  0.044

2 14.692  4.897  1.924  0.787  0.394  0.087  0.131  0.000

3  4.985  2.405  0.525  0.350  0.000  0.000  0.044  0.000

4  1.662  0.875  0.306  0.087  0.000  0.000  0.000  0.000

5  0.831  0.219  0.175  0.000  0.000  0.044  0.000  0.000

6  0.087  0.131  0.044  0.000  0.000  0.000  0.000  0.000

7  0.087  0.087  0.000  0.000  0.000  0.000  0.000  0.000

8  0.044  0.000  0.000  0.000  0.000  0.000  0.000  0.000

maxrun

B  L  W

3  8 17

-----------------------------------------------------------------------------------------

#使用 rle 函数生成赢/输连续次数模拟

trades<-sample(c("W","L","B"),10000,prob=c('.6','.35','.05'),replace=TRUE)

traderuns<-rle(trades)

tr.val<-traderuns$values

tr.len<-traderuns$lengths

maxrun<-tapply(tr.len,tr.val,max)

#连续失败交易次数

lt<-tr.len[which(tr.val=='L')]

lt.1<-lt[1:(length(lt)-1)]

lt.2<-lt[2:(length(lt))]

#简单的连续失败交易次数(n)频率表

table(lt)

#生成连续集合表 streak(n) vs streak(n+1)

tt<-table(lt.1,lt.2)

#转换为比例

options(digits=2)

100*prop.table(tt)

maxrun
