<!--yml

category: 未分类

date: 2024-05-18 14:35:26

-->

# XLLoop 框架 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/12/08/xlloop-framework/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/12/08/xlloop-framework/#0001-01-01)

今天我想强调 [XLLoop 框架](http://xlloop.sourceforge.net/)：Excel 用户自定义函数可以用任何语言编写。

[XLLoop](http://xlloop.sourceforge.net/) 由两个主要组件组成：

+   一个 Excel 插件实现（用 c++ 编写的 XLL）。

+   一个用 R（或其他许多语言）编写的服务器和框架。

[XLLoop](http://xlloop.sourceforge.net/) 允许您以非常简单的方式连接 Excel 和 R，几乎不需要安装。

**要开始**，请下载并解压 [xlloop-basic.zip](http://www.systematicportfolio.com/xlloop-basic.zip) 存档，其中包含使我的示例应用程序正常工作所需的所有文件。

**接下来**，启动 Excel 并添加 [XLLoop](http://xlloop.sourceforge.net/) 插件。

即在 Office 2007/2010 中点击 文件->选项->加载项，按 Alt+G，点击浏览并定位到 xlloop-0.3.2.xll。

在 Office 2003 中，点击 工具->加载项，点击浏览并定位到 xlloop-0.3.2.xll。

**接下来**，编辑从 zip 存档中提取的 runr.bat。输入正确的路径到你的 R 安装。

**最后**，执行 runr.bat，你会看到一个命令窗口弹出，然后转到 Excel 并键入以下公式。

=FS(“ProductTest”, 32, 1886.5)

如果一切顺利，你会看到 60368。

这可能看起来有点像黑魔法，所以让我解释一下发生了什么：

runr.bat 批处理文件启动一个新的 R 会话并执行 rstart.r 脚本。在 rstart.r 脚本中，我们加载/定义要在 Excel 中访问的任何库/函数。接下来，我们加载 XLLoop 服务器的代码并启动服务器。以下是 rstart.r 脚本中的代码。

```

# define function
ProductTest <- function(x, y) x*y

# start xlloop server
source('xlloop.R')
XLLoopServer()

```

接下来，在 Excel 中访问 R 功能，我们使用 FS 函数，第一个参数是我们想要执行的 R 函数，后面跟着函数参数。例如 =FS("ProductTest", 32, 1886.5) 公式调用 ProductTest R 函数，其中 x = 32，y = 1886.5。

*如果你收到“无法连接到服务器”的错误消息，请确保 runr.bat 批处理正在运行（即有一个命令窗口），然后尝试重新计算 Excel（即按 F9）*

一旦你完成了在 Excel 中的工作，你可以关闭 runr.bat 批处理文件创建的命令窗口。

我在 xlloop.xls 中包含了一些示例供你探索。

我将在下一篇文章中展示更多关于 [XLLoop 框架](http://xlloop.sourceforge.net/) 的示例。

在你尝试 [XLLoop](http://xlloop.sourceforge.net/) 时遇到的问题，请告诉我。

一则旁注。连接 Excel 和 R 有许多选项。例如，我以前展示过使用 [RExcel](http://en.wikipedia.org/wiki/RExcel) 执行 R 函数并在 Excel 中显示其输出的示例。
