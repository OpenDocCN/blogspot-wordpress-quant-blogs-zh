<!--yml

类别：未分类

日期：2024-05-12 19:31:59

-->

# Excel | 编码市场

> 来源：[`etrading.wordpress.com/excel/#0001-01-01`](https://etrading.wordpress.com/excel/#0001-01-01)

**编写 C++ 交易员 Excel 插件时需要知道的东西**

Excel 插件是一种特殊的 DLL —— XLL —— 它导出了 Excel 期望找到的某些函数签名。例如 xlAutoOpen、xlAutoClose 和 xlAddInManagerInfo。编写 XLL 意味着你可以用 C++ 实现工作表函数和命令。工作表函数可以从 Excel 公式中调用，命令可以从你在初始化代码中添加到 Excel 菜单栏中的菜单项中调用。要掌握所有这些，你需要…

+   MS Excel 97 SDK – 在[此处](http://support.microsoft.com/default.aspx?scid=kb;EN-US;152152)获取。下载 Frmwrk32.exe。本质上，SDK 由两个文件组成：xlcall.h 和 xlcall32.lib。

+   你需要一本 Steve Dalton 的[《C/C++ 中的 Excel 插件开发》](http://www.amazon.co.uk/exec/obidos/ASIN/0470024690)的副本。不要吝啬花 40 英镑，你真的需要这本书。

+   另一篇微软知识库[文章](http://support.microsoft.com/kb/178474/EN-US/)给出了一个简单的 XLL 实例。这将为你提供一些样板代码来开始工作。

如果你想将实时数据导入工作表，你必须掌握 DDE 的奥秘，否则就走 Excel RTD 的路线。我没用过 RTD，所以不在这里评论。我用过 DDE。这是一个[有用的起点](http://support.microsoft.com/?kbid=279721)。

为什么我们需要 DDE？因为你只能这样做…

Excel4( xlSet, &xRet, 2, (LPXLOPER)&xRef, (LPXLOPER)&xValue);

…来自 Excel 自己的主线程。也就是说，只有在 Excel 调用你，并且你在提供的工作表函数的堆栈上下文中时，才能进行该调用。当你将实时数据推送到工作表时，通常会从发布/订阅消息 API（如 TIB RV 或其他）的另一个线程上收到回调。你不能从该线程调用 Excel API，因此你使用 DDE 将 Windows 消息放入 Excel 的消息队列中，希望它很快会被 Excel 的主事件循环捕获到。在你的 Excel 进程中运行多个线程并执行插件中的代码是没有问题的。当然，只要你的代码是线程安全的！因此，你的消息处理回调将进行 DDE 调用以向 Excel 的主线程发送消息。

要记住，有一些指导方针你应该遵循…

+   始终记住，Excel 实际上是单线程的。

+   你每个 Excel 进程只能有一个实时数据源。对于一个定价表格来说，这可能意味着只有一个期货合约。不要尝试在同一个 Excel 实例中拥有两个由两个期货合约驱动的工作表：Excel 的重新计算会变慢。

+   如果你的表格在收到一个新的 tick 后进行大量的计算，你将需要一个能够意识到你的计算周期的节流机制。否则你可能会发现自己在上一个计算周期结束之前启动了一个新的计算周期！

+   要注意字符串池。如果你正在使用 /GF 进行发布构建，可能会收到“不是有效的插件”消息框。这个 [KB 文章](http://support.microsoft.com/kb/824459) 描述了这个问题和解决方法。

当你的插件和定价或风险表正在运行，并且你想要将其服务化时，请看看 [SpreadServe](http://spreadserve.com)。

**一些其他有用的内容**
