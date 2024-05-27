<!--yml

category: 未分类

date: 2024-05-12 19:35:25

-->

# **__getattr__ considered harmful | Coding the markets**

> 来源：[`etrading.wordpress.com/2011/03/08/__getattr__-considered-harmful/#0001-01-01`](https://etrading.wordpress.com/2011/03/08/__getattr__-considered-harmful/#0001-01-01)

## **__getattr__ considered harmful**

### March 8, 2011

今天的编码让我想起为什么要避免在 Python 中使用 __getattr__。FYI，一个实现了 __getattr__ 方法的类会覆盖成员访问操作符“.”。因此，简单地引用 object.member 会调用 object.__getattr__(member)。在 Python 中的一种典型调试技术是在代码中随处打印 object.member。猜猜如果你在 __getattr__ 方法内部使用这种调试技术会发生什么？像，duh？! 😉
