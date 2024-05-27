<!--yml

分类：未分类

date: 2024-05-12 19:46:23

-->

# Python 2.5.1 | Coding the markets

> 来源：[`etrading.wordpress.com/2007/06/18/python-251/#0001-01-01`](https://etrading.wordpress.com/2007/06/18/python-251/#0001-01-01)

## Python 2.5.1

### 2007 年 6 月 18 日

Windows 下载的 Python 2.5.1 标准二进制文件是用 Visual C++ 7.1 构建的，这意味着提供的 python25.dll 引用了 msvcr71.dll。如果你正在链接 python25.lib 并且使用 Visual C++ 8 进行构建，你将会遇到核心转储。

幸运的是，源代码压缩包中有一个 VC8 项目文件，可以立即构建。所以生成一个使用 msvcr80.dll 的 python25.dll 真的不是什么麻烦事。为 Python 开发者们有一个井井有条的构建过程点赞…
