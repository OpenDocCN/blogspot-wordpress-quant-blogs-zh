<!--yml

分类：未分类

日期：2024-05-12 19:42:11

-->

# PyEval_AcquireLock( ) | 编写市场代码

> 来源：[`etrading.wordpress.com/2008/06/20/pyeval_acquirelock/#0001-01-01`](https://etrading.wordpress.com/2008/06/20/pyeval_acquirelock/#0001-01-01)

## PyEval_AcquireLock( )

### 2008 年 6 月 20 日

Python 文档[解释](http://docs.python.org/api/threads.html)说，同一个线程不应该多次调用 PyEval_AcquireLock( )：“如果这个线程已经拥有锁，就会产生死锁”。我在编写 C++/Python 应用程序框架时遇到了这个问题。在工作中，我很幸运地使用了一个专为构建电子交易系统而设计的优秀的专有 C++应用程序框架。它集成了发布/订阅消息传递、RPC、监控、故障转移、持久性、缓存、版本控制和日志记录等功能。尽管 C++是框架的本机语言，但 Java、C#和 Python 也得到支持。

Python 支持是通过 CPython 使用[Python C API](http://docs.python.org/api/api.html)实现的。C++框架回调被调度到 Python 中。在调度之前和之后，GIL 通过 PyEval_AcquireLock 和 PyEval_ReleaseLock 获取和释放。一切都很顺利，直到 Python 回调调用一个 C++函数，而这个函数又调用另一个 Python 函数，导致第二次调用 PyEval_AcquireLock 从而产生死锁。如果你的进程正在处理 RFQ，这可不是什么好事！

解决方案是使用 Python 2.2 中引入的 PyGILState_Ensure 和 PyGILState_Release。
