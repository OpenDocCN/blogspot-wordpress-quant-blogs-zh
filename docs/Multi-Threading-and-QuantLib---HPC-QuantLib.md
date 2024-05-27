<!--yml

类别：未分类

日期：2024-05-13 00:13:35

→

# 多线程与 QuantLib – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2013/07/26/multi-threading-and-quantlib/#0001-01-01`](https://hpcquantlib.wordpress.com/2013/07/26/multi-threading-and-quantlib/#0001-01-01)

更新 23.11.2015：最新的[版本](https://wordpress.com/post/hpcquantlib.wordpress.com/1376)现在是官方 QuantLib 1.7 发布版的一部分。

更新 22.09.2015：请在此处找到 QuantLib 1.6.2 的最新补丁版本：[链接](https://hpcquantlib.wordpress.com/2015/09/20/quantlib-1-6-2-multithreading-patch-for-jvm-net/)。

更新 28.02.2015：请在此处找到 QuantLib 1.5 的最新补丁版本：[链接](http://hpc-quantlib.de/src/observer15.zip)。

更新 11.05.2014：请在此处找到 QuantLib 1.4 的最新补丁版本：[链接](http://hpc-quantlib.de/src/observer.zip)。

QuantLib 本身不是线程安全的。利用多个核心的标准方法是生成几个独立进程。Riccardo 的[线程安全单例补丁](https://sourceforge.net/p/quantlib/patches/71/)允许在多线程应用程序中使用 QuantLib，只要在不同线程间没有显式共享对象。实际上这个补丁将单例模式转变为线程局部单例模式。这个补丁的一个可能用例是使用多线程测试运行器来加速测试套件，例如，在一个 i7@3.2Ghz 具有四个核心加四个 HT 核心的系统上，多线程测试套件大约运行两分钟，而单线程版本需要大约八分钟。

通过 SWIG 层在 Java/Scala/C#或 F#应用程序中使用 QuantLib 违反了多线程要求，因为垃圾收集器在不同的线程中运行，因此 QuantLib 对象在不同线程中共享。这导致 QuantLib 实现观察者模式的问题，具体讨论请[点击这里](https://hpcquantlib.wordpress.com/2012/02/27/quantlib-swig-and-a-thread-safe-observer-pattern-in-c/)。

基于 boost::signals2 的观察者模式改进实现，以及 Riccardo 的线程安全单例补丁和多线程测试运行器，可以从[github](https://github.com/klausspanderen/quantlib)获取。在 Linux/MacOS 下使用

```
./configure --enable-thread-safe-observer-pattern
```

以启用线程安全单例和线程安全观察者模式。在 Windows 下相应的预处理器指令

```
#define QL_ENABLE_THREAD_SAFE_OBSERVER_PATTERN
```

在文件 userconfig.hpp 中已经设置。为了启用 boost shared_ptr 钩子，将预处理器变量 BOOST_SP_ENABLE_DEBUG_HOOKS 更改为 BOOST_SP_ENABLE_DEBUG_HOOKS_2 在文件中

```
boost/smart_ptr/detail/sp_counted_impl.hpp
```

背景：原始预处理器变量 BOOST_SP_ENABLE_DEBUG_HOOKS 会改变类 boost::shared_ptr 的内存布局，这可能导致与使用 boost::shared_ptr 的其他预编译库出现问题。

这项工作的回报是一个稳定的 SWIG 接口，支持 Java/Scala/C#/F#，以及一个线程局部单例实现，这使得只要 SWIG/QuantLib 对象不在不同线程之间显式共享，就能在多线程应用程序中使用 QuantLib。
