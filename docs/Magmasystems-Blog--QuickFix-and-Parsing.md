<!--yml

分类：未分类

日期：2024-05-18 05:10:02

-->

# Magmasystems 博客：QuickFix 和解析

> 来源：[`magmasystems.blogspot.com/2007/04/quickfix-and-parsing.html#0001-01-01`](http://magmasystems.blogspot.com/2007/04/quickfix-and-parsing.html#0001-01-01)

我惊讶于，在 QuickFix 提供的.NET API 中，竟然没有方法或 MessageFactory 能够接受一个任意的 FIX 字符串，并返回一个正确的 FIX 消息对象。我遗漏了什么吗？

我相信 FIX4NET 具备这样的功能，但他们不支持 FIX 4.4。

我们必须请求 Mike Roberts 为我们提供.NET 版本的 TTConnect FIX 引擎。

©2007 Marc Adler - 版权所有
