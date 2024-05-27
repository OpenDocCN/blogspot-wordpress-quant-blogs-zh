<!--yml

分类：未分类

日期：2024-05-18 15:43:12

-->

# Python 交易：如何设置 Python 开发环境

> 来源：[`tradingwithpython.blogspot.com/2011/11/how-to-setup-python-development.html#0001-01-01`](http://tradingwithpython.blogspot.com/2011/11/how-to-setup-python-development.html#0001-01-01)

如果你想要从这篇博客开始玩代码并编写自己的代码，你首先需要设置一个开发环境。我已经在这篇博客上总结了工具和软件包的概要。

[工具页面](http://tradingwithpython.blogspot.com/p/setting-up-development-environment.html)

为了让它变得更容易，这里是你需要遵循的步骤，以开始运行：

1\. 安装

[PythonXY](http://code.google.com/p/pythonxy/wiki/Downloads)

. : 这包括 Python 2.7 和工具 Spyder，Ipython 等。

2\. 安装

[Tortoise SVN](http://tortoisesvn.net/downloads.html)

. 这是一个工具，你可以使用它从 Google Code 拉取源代码

3\. 安装

[Pandas](http://pypi.python.org/packages/2.7/p/pandas/pandas-0.5.0.win32-py2.7.exe#md5=c2badf1d82d48a57abcff72228d28cd9)

(时间序列库)

现在所需要的全部东西就是这些。

要获取代码，请使用在安装 Tortoise SVN 后可用的'Svn 检出'窗口资源管理器上下文菜单。像这样进行检出（将检出目录更改为您想要的位置，但该位置应以

*tradingWithPython*

):

如果一切顺利，文件的最新版本将被下载。我会编写更多的代码并改进现有的代码，你可以通过使用'svn 更新'上下文菜单来同步我的代码。

最终步骤是启动 Spyder（通过 pythonXY 启动器或开始菜单），并将刚刚上方的目录添加到'

*tradingWithPython'*

（在我的例子中是 C:\Users\jev\Desktop') 目录添加到 python 路径。通过'工具'->'PYTHONPATH 管理器'进行此操作。

好的，全部完成，现在你可以从\cookbok 目录运行示例了。
