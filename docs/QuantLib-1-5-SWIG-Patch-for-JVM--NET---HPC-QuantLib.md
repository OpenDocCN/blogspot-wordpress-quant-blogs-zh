<!--yml

分类：未分类

日期：2024-05-13 00:13:30

-->

# QuantLib-1.5 SWIG 补丁用于 JVM/.NET – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2015/02/28/quantlib-1-5-swig-patch-for-jvm-net/#0001-01-01`](https://hpcquantlib.wordpress.com/2015/02/28/quantlib-1-5-swig-patch-for-jvm-net/#0001-01-01)

更新 23.11.2015：补丁的一个[修改版本](https://wordpress.com/post/hpcquantlib.wordpress.com/1376)现在已成为官方 QuantLib 1.7 发布版的一部分。

更新 22.09.2015：请在此找到 QuantLib 1.6.2 的最新且改进的补丁版本[链接](https://hpcquantlib.wordpress.com/2015/09/20/quantlib-1-6-2-multithreading-patch-for-jvm-net/)。

通过 SWIG 接口在 JVM 和 .NET 语言（例如 Java/Scala 和 C#/F#）中使用 QuantLib 存在一个已知的问题。QuantLib 的观察者模式实现不支持在不同线程中运行的并行垃圾回收器。结果程序会随机崩溃或产生“纯虚拟函数调用”。关于这个问题的详细描述可以在此处找到，例如[链接](https://hpcquantlib.wordpress.com/2012/02/27/quantlib-swig-and-a-thread-safe-observer-pattern-in-c/)和参考文献中。

请在此找到用于修复此问题的 QuantLib 1.5 补丁[链接](http://hpc-quantlib.de/src/observer15.zip)。
