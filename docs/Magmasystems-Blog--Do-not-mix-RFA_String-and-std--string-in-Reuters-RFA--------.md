<!--yml

类别：未分类

日期：2024-05-18 04:57:10

-->

# Magmasystems Blog: 在路透社 RFA 中不要混合使用 RFA_String 和 std::string !!!!!!!!!!!!!!!!

> 来源：[`magmasystems.blogspot.com/2008/11/do-not-mix-rfastring-and-stdstring-in.html#0001-01-01`](http://magmasystems.blogspot.com/2008/11/do-not-mix-rfastring-and-stdstring-in.html#0001-01-01)

有时候， Always Be Coding. 今天，这不是好事。

我刚刚花了一整天的时间来追踪一个问题的解决，试图将路透社 OMM API 整合到我们的基于 MarketFeed 的应用程序中。感谢 Apurva，他引导我查看了 Readme 文件中的一小段话，内容如下：

已知的缺陷- 在应用程序接口和实现中混合使用 RFA_String 和 std::string

一旦我在代码中移除了 std::string 引用，一切就神奇地正常工作了！

©2008 Marc Adler - 版权所有。

这里所有的观点都是个人的，与我的雇主无关。
