<!--yml

category: 未分类

date: 2024-05-12 19:32:48

-->

# C++库和 ABI 兼容性 | 编写市场代码

> 来源：[`etrading.wordpress.com/2014/05/14/c-libs-abi-compatilibilty/#0001-01-01`](https://etrading.wordpress.com/2014/05/14/c-libs-abi-compatilibilty/#0001-01-01)

## C++库和 ABI 兼容性

### `2014 年 5 月 14 日`

当你构建一个将支持 C++ API 的服务器产品时，你需要考虑你的 ABI——二进制接口。通常，C++ API 被分发为头文件和库文件。如果你的 API 导出的函数包括使用 std::string 等参数，你立即就会遇到问题，因为你要求客户端代码使用与你相同的 STL 实现来构建库。如果客户端代码有源代码访问权限，并且可以重新构建，则这没问题。但是商业的专有产品通常不会分发源代码。那么如何避免强制 API 客户端代码依赖？我搜索了一些资源，找到了两个特别好的资源我不得不标记出来。

这是[Thiago Macieira 关于二进制兼容性的演示](http://events.linuxfoundation.org/sites/events/files/slides/Binary_Compatibility_for_library_devs.pdf)：一个提供了库作者指南的优秀演示。这是 Thiago 建议的摘要...

1.  使用 pimpl 习惯隐藏对象大小

1.  在函数签名中使用普通的旧数据类型

1.  不要传递指针或引用给内部对象

1.  不要内联函数

1.  所有的类都需要一个非内联虚拟函数；可能是析构函数

1.  避免在模板类中使用虚拟函数

1.  不要重新排序或删除公共成员，或更改访问级别

`2` 表示函数参数中不使用 STL 或 Boost 类型。我将通过避免在 API 中使用模板来解决问题 `6`。

[这篇文章](http://www.agner.org/optimize/calling_conventions.pdf)是由[Agner Fog](http://www.agner.org)撰写的，它是对数据大小和对齐方式的细致调查，堆栈对齐，寄存器使用和参数处理的调用约定，名称混淆方案以及所有主要 x86 和 x64 操作系统和 C++编译器的 COFF 对象文件格式的调查。强烈推荐。
