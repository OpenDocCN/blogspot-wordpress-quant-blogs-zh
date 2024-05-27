<!--yml

分类：未分类

日期：2024-05-17 23:29:41

-->

# QuantLib-SWIG 针对 JVM/.NET 语言的补丁 – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2014/05/11/quantlib-swig-patch-for-jvm-net-languages/#0001-01-01`](https://hpcquantlib.wordpress.com/2014/05/11/quantlib-swig-patch-for-jvm-net-languages/#0001-01-01)

更新 23.11.2015：最新版本现在已是官方 QuantLib 发布版 1.7 的一部分。

更新 22.09.2015：请在此处找到 QuantLib 1.6.2 的最新且改进的补丁版本。[链接](https://hpcquantlib.wordpress.com/2015/09/20/quantlib-1-6-2-multithreading-patch-for-jvm-net/)。

通过 SWIG 接口在 JVM 和 .NET 语言（例如 Java/Scala 和 C#/F#）中使用 QuantLib 有一个已知的缺陷。QuantLib 的观察者模式的实现不支持在不同线程中运行的并行垃圾收集器。结果程序可能会随机崩溃或产生“纯虚拟函数调用”。关于此问题的详细描述，可以在此处找到例如[此处](https://hpcquantlib.wordpress.com/2012/02/27/quantlib-swig-and-a-thread-safe-observer-pattern-in-c/)和参考文献中。

请在此处找到[补丁](http://hpc-quantlib.de/src/observer.zip)，用于修复 QuantLib 1.4 中的此问题。它包含

安装说明包含在 readme.txt 文件中。
