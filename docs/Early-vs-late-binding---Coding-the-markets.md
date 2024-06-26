<!--yml

类别：未分类

日期：2024-05-12 19:34:37

-->

# 早绑定 vs 晚绑定 | 编码市场

> 来源：[`etrading.wordpress.com/2012/01/29/early-vs-late-binding/#0001-01-01`](https://etrading.wordpress.com/2012/01/29/early-vs-late-binding/#0001-01-01)

## 早绑定 vs 晚绑定

### 2012 年 1 月 29 日

我基本上同意 [Jeff 的观点](http://blog.jvroom.com/2012/01/28/choosing-your-programming-language-the-inside-scoop/)，即强类型、静态绑定语言与弱类型、晚绑定系统。但我不同意我们必须偏向前者。没有一种语言适合所有场景，我认为正确的方法是使用早绑定和晚绑定的混合。当我们需要效率、紧凑和速度时使用早绑定。当我们需要表现力和快速上市时间时使用晚绑定。电子交易系统是一个完美的例子，我们需要在同一个系统中拥有所有这些矛盾的优点。一种语言的组合是满足所有这些要求的唯一方式。布拉德·科克斯（Brad Cox）在 1990 年的《Planning the Software Industrial Revolution》中以极高的预见性阐述了这一方法。我们需要的是一个允许我们随意混合语言的开发环境。当我们检查带有不同语言的堆栈时，调试器能够无缝处理。跨运行时的一致线程模型。以及一致的内存管理模型。微软通过 .Net CLR 最接近实现了这一点。Java VM 也可以托管多种语言，但工具的质量不如 .Net CLR。

就我个人而言，我喜欢 C++ 和 Python 的组合。但在构建具有这种混合的系统时存在紧张关系。第一个是线程模型。如果你从事服务器工程，你必须了解 GIL。一个单独的 C++ 线程与 Python 配合得很好。一些用于专用任务的有限数量的 C++ 线程，其中只有一个调用 Python，也可以很好地工作。多个 C++ 线程作为使用锁来协作执行相同逻辑的池化工作者，并且每个线程都调用 Python，这种情况将无法很好地工作。

另一个紧张关系是不同的内存管理模型。Python C 运行时组织了自己的 PyObject* 分配内存池。不同类型有不同的子池，对字符串、整数和较大对象的管理规则也不同。Python 的内存池往往只增长，不像 C++ 程序，我们可以看到当 C RT lib 将内存返回给操作系统时其内存配置的下降。

因此，如果我们在同一运行时有多种语言，最大的挑战之一就是做出正确的架构决策，使这些语言在不同方式下利用相同的 OS 提供的资源的情况下进行合作。
