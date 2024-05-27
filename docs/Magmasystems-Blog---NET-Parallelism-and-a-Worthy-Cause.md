<!--yml

分类：未分类

date: 2024-05-18 04:49:19

-->

# Magmasystems 博客：.NET 并行处理和一个有价值的事业

> 来源：[`magmasystems.blogspot.com/2011/10/net-parallelism-and-worthy-cause.html#0001-01-01`](http://magmasystems.blogspot.com/2011/10/net-parallelism-and-worthy-cause.html#0001-01-01)

A

[一个引人入胜的案例研究](http://www.microsoft.com/casestudies/Microsoft-Visual-Studio-2010/Massachusetts-General-Hospital/Parallelization-of-Native-C-Code-Helps-Reduce-3-D-Image-Processing-Times-by-a-Factor-of-20/4000010935)

微软提供了一个案例，介绍了马萨诸塞州总医院（MGH）如何大大缩短了结肠镜检查结果分析的时间（和成本）。对于 50 岁以上的男性来说，结肠镜检查几乎是强制性的，而且这个过程有些干扰和不舒服。并行处理技术已经将分析时间缩短了许多数量级，并使“虚拟结肠镜检查”的概念变得更加真实。

微软曾经要求 MGH 将其代码移植到 C#，但由于种种原因，这是不可能的。我想知道如果代码被移植了，改进的程度会不会更大。

将这个技术应用到资本市场，公司可能会发现，他们的实时定价和风险（以及压力测试）可能会从重新架构到.NET/C#/TPL 堆栈中受益。

©2011 Marc Adler - 版权所有。这里的所有观点都是个人观点，与我的雇主无关。
