<!--yml

category: 未分类

date: 2024-05-17 23:40:20

-->

# Inter-Thread Communication using Lock-Free Algorithms – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2012/05/18/inter-thread-communication-using-lock-free-algorithms/#0001-01-01`](https://hpcquantlib.wordpress.com/2012/05/18/inter-thread-communication-using-lock-free-algorithms/#0001-01-01)

In his blog [Martin Fowler](http://martinfowler.com) discusses the [LMAX architecture](http://martinfowler.com/articles/lmax.html), a high throughput retail financial trading platform. A remarkable detail of the architecture is the central business logic processor, which is implemented as a single threaded Java program. The supporting pre- and post-processing is running as a multi threaded application using [lock-free](http://en.wikipedia.org/wiki/Non-blocking_algorithm) ring buffers.

In general lock-free algorithms are implemented using atomic read-modify-write primitives which are provided by modern CPUs. Probably the most used lock-free algorithm in the boost library is the reference counting in boost::shared_ptr. On popular hardware platforms these reference count updates are based on atomic increments/decrements using  [compare-and-swap](http://en.wikipedia.org/wiki/Compare-and-swap) (CAS) operations. The performance improvements over normal mutex exclusion locks are significant as the following little experiment shows. Basis for this experiment is a function which increments an integer counter 500 million times in a loop [1]. This loop is carried out in

+   simple single threaded loop

+   single thread loop using atomic increments

+   single thread loop acquiring a mutex exclusion lock for every pass.

+   two threads using atomic increments

+   two threads using mutex exclusion locks

A Java and the C++ implementation is available [here](http://hpc-quantlib.de/src/cas.zip). The Java code uses the package java.util.concurrent.atomic and the C++ code uses boost::detail::atomic_count to implement the atomic increments. The run times are measured on a Core i3@3GHz.

![](https://hpcquantlib.wordpress.com/wp-content/uploads/2012/05/plot.png) Lock-free algorithms are difficult to implement and to debug. Tim Blechmann has written a little gem library boost::lockfree (Parts of the library are now in the boost release 1.53.0). Among others this library contains a wait-free single-producer/single-consumer ring buffer. This ring buffer is e.g. tailor-made to separate the Monte-Carlo path generation from the pricing of a derivate. With a few lines of code the path generation can then run in a different thread.

代码可在[此处](http://hpc-quantlib.de/src/buffereddatafactory.zip)找到，其中包含基于 boost::lockfree::ringbuffer 类的 BufferedDataFactory 和一个对 QuantLib 测试案例 HybridHestonHullWhiteProcessTest::testZeroBondPricing 的略微修改版。在这个测试案例的版本中，路径生成在分离的线程中运行，并使用 BufferedDataFactory 将数据传递给定价线程。

[1] [Disruptor](http://disruptor.googlecode.com/files/Disruptor-1.0.pdf)：用于在并发线程之间交换数据的、高性能的有界队列的替代品。
