<!--yml

类别：未分类

日期：2024-05-17 23:41:41

-->

# 使用 Scala 进行支付脚本编程 - HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2011/09/01/using-scala-for-payoff-scripting/#0001-01-01`](https://hpcquantlib.wordpress.com/2011/09/01/using-scala-for-payoff-scripting/#0001-01-01)

使用内置解释器或“即时编译器”进行支付脚本编程，而不是在 C++中实现支付，其优势是显而易见的。因为不需要重新编译和部署 C++定价库，所以上市时间更快，而且不需要深入 C++知识的人也能够开发和测试新的结构化产品。一个缺点通常是所选脚本语言的执行速度。我所见过的/用于支付脚本的语言例子有 [Python](http://python.org/) （C++接口 [boost::python](http://www.boost.org/doc/libs/1_47_0/libs/python/doc/)），[Lua](http://www.lua.org/)，[tinycc](http://tinycc.org) 和 [CINT](http://root.cern.ch/drupal/content/cint)。当涉及到执行速度时，这些语言都不适合构建高性能解决方案，例如 [1]。 特别是如果 Monte-Carlo 场景生成器在 GPU 上运行。那么在 CPU 上运行的支付脚本编程很容易成为定价库的瓶颈。

[Scala](http://www.scala-lang.org) 是一种现代编程语言，它集成了面向对象和函数式语言特性。Scala 编译器为 Java 虚拟机生成字节码。因此，Scala 脚本的执行速度与 Java 相当，大约比 C++慢一倍 [1]。

Scala 编译器本身是一个 Scala 对象，可以在运行时用来编译和链接新的脚本或类。此外，利用[JNI](http://download.oracle.com/javase/6/docs/technotes/guides/jni/index.html) ，很容易将 Java 虚拟机附加到 C++进程之间，以及 C++和 Scala 之间交换数据。Scala 还提供了许多特性，用于设计一个“内部”用户友好的领域特定语言（DSL）用于支付脚本。

一个小型 QuantLib/Scala Monte-Carlo 模拟的示例代码可以在 [这里](http://hpc-quantlib.de/src/scalaPayoffScripting.zip) 找到。它依赖于 QuantLib 1.0 或更高版本，Java 1.6 虚拟机和 Scala 2.8/9\。覆盖 PayoffImpl.scala 类，不重新编译 C++代码来实现不同的支付。

[1] [计算机语言基准游戏](http://shootout.alioth.debian.org/u32/which-programming-languages-are-fastest.php)
