<!--yml

分类：未分类

date: 2024-05-13 00:11:00

-->

# Python, QuantLib 和 多线程 – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2021/11/29/python-quantlib-and-multithreading/#0001-01-01`](https://hpcquantlib.wordpress.com/2021/11/29/python-quantlib-and-multithreading/#0001-01-01)

Python 是——得益于 [GIL](https://en.wikipedia.org/wiki/Global_interpreter_lock) ——并不是现代多线程编程的首选语言，而且 QuantLib 也不是真正线程安全的，尽管线程安全的观察者模式实现和线程安全的单例初始化有助于降低风险（简单来说，作为一般建议，不要在线程之间共享对象，不要以不可控的方式更改全局状态，例如评估日期，并启用 QL_ENABLE_THREAD_SAFE_OBSERVER_PATTERN 选项）。

即便如此——除了 Java/Scala/C# 或 C++ 以外的其他语言——在 Python 中默认情况下并没有太多可以获得的优势，因为由 [SWIG](http://www.swig.org/) 生成的接口代码在运行 C++ 代码时不会释放 GIL。因此，当运行长时间持续的 QuantLib 计算时，所有除了一个线程外的所有线程都会被阻塞。但并非完全绝望，可以通过命令行参数“-threads”指示 SWIG 在调用 QuantLib 方法前释放 GIL。这里的唯一注意事项是，QuantLib 的 SWIG 接口文件中包含了一些低级别的 Python C API 调用，例如 Py_XDECREF。每个包含低级别 Python C API 调用的块都需要在块的开始处用 SWIG_PYTHON_THREAD_BEGIN_BLOCK 宏来获取 GIL，总共 60 次。

作为回报，当在 Python 中运行 QuantLib 代码时，GIL 将被释放，并且可以使用多线程来加速相同方式下的多个长时间持续的 QuantLib 调用，就像在其他语言中一样。
