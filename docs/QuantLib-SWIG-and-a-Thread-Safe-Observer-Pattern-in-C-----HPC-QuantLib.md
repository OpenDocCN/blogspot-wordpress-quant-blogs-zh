<!--yml

类别：未分类

日期：2024-05-17 23:29:47

-->

# QuantLib-SWIG 和 C++中的线程安全观察者模式 – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2012/02/27/quantlib-swig-and-a-thread-safe-observer-pattern-in-c/#0001-01-01`](https://hpcquantlib.wordpress.com/2012/02/27/quantlib-swig-and-a-thread-safe-observer-pattern-in-c/#0001-01-01)

更新 23.11.2015：修改后的补丁现在已是官方 QuantLib 1.7 版本的一部分。

更新 28.02.2015：请在此找到 QuantLib 1.5 的最新补丁版本[这里](http://hpc-quantlib.de/src/observer15.zip)。

更新 11.05.2014：请在此找到 QuantLib 1.4 的最新补丁版本[这里](http://hpc-quantlib.de/src/observer.zip)。

`QuantLib`库并不是真正线程安全的。在多核和并行环境中的成功使用通常是通过在不同进程之间传递消息实现的，而不是共享内存和多线程。如果不同线程对不同对象进行操作，那么 QuantLib 也可以在多线程环境中使用（定义`QL_ENABLE_SESSIONS`以使单例线程相关）。

如果您通过 SWIG[1]在 Java 或 Scala 中使用 QuantLib，即使主程序是单线程的，QuantLib 例程也会自动在多线程环境中执行。JVM 的垃圾收集器通常在不同的线程中运行。与 QuantLib 实现的观察者模式相结合，这可能会导致严重问题，例如，以下单线程 Scala 代码在多核计算机上运行一段时间后会崩溃。

```
import org.quantlib.{Array => QArray, _}
object ObserverTest {
    def main(args: Array[String]) : Unit = {
        System.loadLibrary("QuantLibJNI");
        val aSimpleQuote = new SimpleQuote(0)

        while (true) {
            (0 until 10).foreach(_ => {
                new QuoteHandle(aSimpleQuote)
                aSimpleQuote.setValue(aSimpleQuote.value + 1)
            })
            System.gc
        }
    }
}
```

垃圾收集器可能在同一时间点调用观察者（QuoteHandle）的析构函数，同时`aSimpleQuote.setValue`在同一对象上调用更新方法。（请在此找到关于此问题的原始帖子[这里](http://old.nabble.com/Issues-with-C--Swig-Bindings,-NUnit-and-Settings.instance%28%29.setEvaluationDate%28%29-td30549787.html) ，这是关于这个问题的 QuantLib 邮件列表的原始帖子。）对于一个绿色项目，作者在[2]中为这个问题提供了一个很好的 C++解决方案。不幸的是，这个解决方案不能应用于 QuantLib，因为解决方案涉及观察者接口签名的更改，此后会导致 QuantLib 库发生很多变化。

这里的主要问题是，我们必须在析构函数开始工作之前禁用观察者。理论上，这可以通过向每个新的`boost::shared_ptr`实例添加一个特殊的“删除器”来实现。但这样做又会导致库中出现很多变化。

当使用预处理器指令`BOOST_SP_ENABLE_DEBUG_HOOKS`编译时，boost 库在任意 boost 智能指针调用析构函数之前添加了一个回调钩子。这个钩子可用于在实际析构函数执行之前禁用观察者。此外，`boost::signals2`库[3]提供了一个简单且线程安全的通知机制。

原始 QuantLib 观察者/可观察接口的相应线程安全实现可以在[这里](http://hpc-quantlib.de/src/observable.zip)找到。为每个源文件设置预处理器指令 BOOST_SP_ENABLE_DEBUG_HOOKS。替换/添加 observable.hpp 和 observable.cpp 文件并重新编译 QuantLib 库和 QuantLib-SWIG 模块。

注意：如果你想要使用与 QL 1.2 一起的补丁而不是用于 trunk，请参阅 gk 下面的注释。

[1] 简化包装器与接口生成器，[SWIG](http://swig.sourceforge.net/)

[2] 陈硕，[析构函数与线程的相遇](http://www.slideshare.net/chenshuo/where-destructors-meet-threads)

[3] Douglas G., Mori Hess F., [Boost.Signals2](http://www.boost.org/doc/libs/1_48_0/doc/html/signals2.html)
