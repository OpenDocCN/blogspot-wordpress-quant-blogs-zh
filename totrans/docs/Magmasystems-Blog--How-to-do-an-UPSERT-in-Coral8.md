<!--yml
category: 未分类
date: 2024-05-18 05:03:04
-->

# Magmasystems Blog: How to do an UPSERT in Coral8

> 来源：[http://magmasystems.blogspot.com/2008/04/how-to-do-upsert-in-coral8.html#0001-01-01](http://magmasystems.blogspot.com/2008/04/how-to-do-upsert-in-coral8.html#0001-01-01)

Assume that the LastTrades window has the retention policy of KEEP LAST PER Symbol.

Here is some code (provided by Mark of Coral8) to do an upsert.

**INSERT INTO****LastTrades******SELECT** SPC.symbol, SPC.price, **If** LT.volume **Is Null Then** 0 **Else** LT.volume **End If****FROM** StreamPriceCorrections SPC **Left Outer Join** LastTrades LT **ON** SPC.Symbol = LT.Symbol;

If we need to do an update rather than an upsert, this piece of code works:

 `**INSERT INTO**
LastTrades
**SELECT**
SPC.symbol,
SPC.price,
LT.volume
**FROM**
StreamPriceCorrections SPC, LastTrades LT
**ON** SPC.Symbol = LT.Symbol;` 

©2008 Marc Adler - All Rights Reserved**