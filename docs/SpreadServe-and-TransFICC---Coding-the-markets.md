<!--yml

category: 未分类

date: 2024-05-12 19:29:32

-->

# SpreadServe 和 TransFICC | 编码市场

> 来源：[`etrading.wordpress.com/2017/08/11/spreadserve-and-transficc/#0001-01-01`](https://etrading.wordpress.com/2017/08/11/spreadserve-and-transficc/#0001-01-01)

## SpreadServe 和 TransFICC

### 2017 年 8 月 11 日

今年夏天早些时候，我完成了一个**SpreadServe**与**TransFICC**的 POC 集成。对于那些不熟悉的人来说，TransFICC 的创始团队有前**LMAX**成员，它是一家新的 ECN 网关市场参与者。从技术上讲，它们的关键差异化优势是云托管和高性能工程技术。对于 TransFICC 客户来说，唯一在本地运行的是 Java API，它为所有常用的固定收益 ECN 提供了相同的正交化接口，并连接到云托管的网关进程。

自从我上次在 Java 中构建非平凡项目以来已经有一段时间了，所以我非常惊喜地发现 Java 生态系统已经变得多么先进。**Gradle**已经改变了依赖和包管理。在 Python 和 C++世界中流行的单线程异步方法终于来到了 Java，得益于**Netty**。你可以在[GitHub 上找到代码](https://github.com/SpreadServe/TFWebSock)。
