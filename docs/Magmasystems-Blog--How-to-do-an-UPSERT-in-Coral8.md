→yml

类别：未分类

日期：2024-05-18 05:03:04

→

# Magmasystems 博客：如何在 Coral8 中进行插入更新

> 来源：[`magmasystems.blogspot.com/2008/04/how-to-do-upsert-in-coral8.html#0001-01-01`](http://magmasystems.blogspot.com/2008/04/how-to-do-upsert-in-coral8.html#0001-01-01)

假设 LastTrades 窗口的保留策略是 KEEP LAST PER Symbol。

以下是一些代码（由 Coral8 的 Mark 提供），用于进行插入更新。

**INSERT INTO****LastTrades******SELECT** SPC.symbol, SPC.price, **如果** LT.volume **为空，则** 0 **否则** LT.volume **结束如果** FROM StreamPriceCorrections SPC **左外连接** LastTrades LT **ON** SPC.Symbol = LT.Symbol;

如果我们需要进行更新而不是插入更新，这段代码可以工作：

`**INSERT INTO**

最后交易

**SELECT**

SPC.symbol,

SPC.price,

LT.volume

**FROM**

流价格修正 SPC，最后交易 LT

**ON** SPC.Symbol = LT.Symbol;`

©2008 Marc Adler - 版权所有**
