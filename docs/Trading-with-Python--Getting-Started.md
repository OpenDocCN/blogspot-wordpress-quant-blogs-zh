<!--yml

分类：未分类

date: 2024-05-18 15:43:33

-->

# Python 交易：入门

> 来源：[`tradingwithpython.blogspot.com/2011/09/getting-started.html#0001-01-01`](http://tradingwithpython.blogspot.com/2011/09/getting-started.html#0001-01-01)

首先，我必须承认，即使考虑从 Matlab 转向 Python，我也花了很长时间。我已经使用 Matlab 超过十年了，我必须说，它是一个进行研究的优秀工具。然而，在我的专业和私人工作中，有许多情况下 Matlab 不是完成工作的最佳工具。这迫使我学习了一些像 Labwindows 和 C# 这样的东西来进行 GUI 编程，学习 PHP 来构建网站。不要忘记 Matlab 不是一个免费（不仅仅是言论自由，也不是啤酒自由）的产品。

然而，我尝试转向的主要原因，是 Python 是一把“编程的瑞士军刀”。它可以用来用 Qt 制作出色的 GUI，用 SciPy 进行研究，编写动态网站等。

本博客上的所有文章都将基于以下工具：

+   作为基础发行版，我使用的是 [PythonXY](http://code.google.com/p/pythonxy/wiki/Welcome)，这是一个包含（几乎）进行 Python 科学编程所需的一切的优秀包。

+   为了连接到 Interactive Brokers，你还需要[IbPy](http://code.google.com/p/ibpy/)。
