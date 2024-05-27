<!--yml

category: 未分类

date: 2024-05-12 19:32:55

-->

# Hardcore Windows debugging | Coding the markets

> 来源：[`etrading.wordpress.com/2014/05/10/hardcore-windows-debugging/#0001-01-01`](https://etrading.wordpress.com/2014/05/10/hardcore-windows-debugging/#0001-01-01)

## Hardcore Windows debugging

### 2014 年 5 月 10 日

在我的[POC](https://etrading.wordpress.com/2014/02/16/poc-m1-running/)项目中，我开始使用[windbg](http://msdn.microsoft.com/en-gb/library/windows/hardware/ff551063%28v=vs.85%29.aspx)。我一直是 Microsoft 的 Visual Studio 调试器的粉丝。甚至在 90 年代末，当我深受 Eric Raymond 的《大教堂与市集》的催眠，陷入反微软阶段时，我也从未停止对调试器的评价。Visual Studio 调试器非常出色，但 windbg 却是另一种东西。这是微软自己用来调试 Windows 的调试器。是的，与 VS 调试器相比，界面有点臃肿，但命令集的强大超乎想象。它内置了自己的脚本系统，因此你可以构建自定义断点：例如，当这个整数大于 100 时第 5 次进入循环时中断。它还有一个 API，因此调试引擎可以从[Python 等其他语言](http://pydbgeng.sourceforge.net/)进行操作。就我个人而言，我非常喜欢发现 windbg 的强大之处。在我这么做的同时，我在[这里](https://etrading.wordpress.com/windbg/ "windbg")记录了一些提示和技巧。
