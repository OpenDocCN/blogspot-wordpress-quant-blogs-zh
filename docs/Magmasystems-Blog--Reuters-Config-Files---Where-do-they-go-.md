<!--yml

分类：未分类

date: 2024-05-18 04:57:30

-->

# Magmasystems 博客：路透社配置文件 - 它们去了哪里？

> 来源：[`magmasystems.blogspot.com/2008/11/reuters-config-files-where-do-they-go.html#0001-01-01`](http://magmasystems.blogspot.com/2008/11/reuters-config-files-where-do-they-go.html#0001-01-01)

如果您正在使用路透社 RFA 6.x API 消费市场数据，您知道 RFA 需要找到三个配置文件。这些配置文件是

+   RFA.CFG

+   appendix_a

+   enumtype.def

通常，如果您正在运行控制台或 WinForms 应用程序，您将这些配置文件放在可执行文件的同一目录中。

但是，如果您正在运行一个

Windows 服务

使用了 RFA 的服务或可执行文件？

经过一些实验，我们发现您需要将文件存储在这些位置：

+   Windows 32 - 将文件放在 c:\WINNT\system32

+   Windows 64 - 将文件放在 c:\WINNT\SysWow64

使用 RFA 的服务或可执行文件（市场数据 API，而不是 OMM API）使用 32 位 DLL。这是因为路透社还没有为 RFA 提供 64 位 DLL。因此，您需要使用

[CorFlags.exe](http://msdn.microsoft.com/en-us/library/ms164699%28VS.80%29.aspx)

在 64 位的 Windows 2003 服务器上运行，以便使您的应用程序运行。

感谢 SysInternals 提供的 wonderful Procmon 工具，它帮助我们解决了这个问题。

©2008 Marc Adler - 版权所有。

这里的所有观点都是个人的，与我的雇主无关。
