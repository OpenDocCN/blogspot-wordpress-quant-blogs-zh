<!--yml

分类：未分类

日期：2024-05-18 05:19:05

-->

# Magmasystems Blog: Comments Added and WMI Blues

> 来源：[`magmasystems.blogspot.com/2006/08/comments-added-and-wmi-blues.html#0001-01-01`](http://magmasystems.blogspot.com/2006/08/comments-added-and-wmi-blues.html#0001-01-01)

我忘记批准和发布经过审查的评论（感谢 Craig）。所以现在，大约有 30 条评论，从 5 月底开始。

我一直在想为什么没有人祝贺我新的工作:-)

开始尝试使用微软的 WMI 来监控应用程序。我需要批评微软，因为他们不让您编写基于.NET 的 WMI 提供程序，这些提供程序允许方法调用和属性设置器。您所能做的所有.NET WMI 提供程序只能接收事件和执行属性获取。您不能通过属性设置来更改一个值，也不能通过调用提供程序上的方法来管理一个应用程序。

似乎如果您想编写一个功能完整的 WMI 提供程序，那么您必须下降到 COM（甚至使用 ATL）和 C++。

这个限制非常严重。这意味着我无法编写一个可以通过.NET 提供程序管理的.NET 应用程序。这意味着，如果我想要编写一个监控和管理仪表板（用于监控，比如说，一个基于.NET 的交易系统），我必须拿出我的旧 COM/ATL 书籍并编写非托管代码。ugh！

似乎好像

[很多人](http://groups.google.com/groups/search?ie=UTF-8&q=WMI+.NET+provider+methods&qt_s=Search)

在新闻组上分享我的痛苦。

©2006 Marc Adler - 版权所有
