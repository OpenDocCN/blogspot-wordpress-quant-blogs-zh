<!--yml

类别：未分类

date: 2024-05-18 08:09:38

-->

# Using Quantlib on a Windows (32bit) machine | Quant Corner

> 来源：[`quantcorner.wordpress.com/2011/01/24/usin-quantlib-on-a-windows-32-bit-machine/#0001-01-01`](https://quantcorner.wordpress.com/2011/01/24/usin-quantlib-on-a-windows-32-bit-machine/#0001-01-01)

在这篇文章中，我们展示了在在**Windows 32**计算机上使用**Quantlib**之前所需的步骤。我们使用**MS Visual Studio 2010**安装这个强大的量化库。而且，这也适用于 MS**Visual Studio Express 2010**。我们基于**Quantlib**库官方网站的“安装”部分，即[`quantlib.org/install/vc9.shtml`](http://quantlib.org/install/vc9.shtml)。正如这个网址本身所表明的，这是为较早版本的 MS Visual Studio（即 MS**Visual Studio 2008**版本）的安装文档。我们的工作是获取并安装最新的 Quantlib 文件。

**Quantlib**库需要**Boost**库在你的机器上可用。因此，我们也将安装后者。最后，我们将安装一个用户友好的软件，即**TortoiseSVN**，以获取这两个库文件的最新版本。

**让我们开始**：

– 下载**Boost**库安装程序，该安装程序可在[`www.boostpro.com/download`](http://www.boostpro.com/download)免费获得。截至编写本文时，最新可用的版本是 BoostPro 1.44.0 安装程序。

– 遵循[`quantlib.org/install/vc9.shtml`](http://quantlib.org/install/vc9.shtml)的“Boost 安装”段落。不过，你会安装**Visual C++ 10.0**（**Visual Studio 2010**）二进制文件。

– 从[`sourceforge.net/projects/quantlib/files/QuantLib`](http://sourceforge.net/projects/quantlib/files/QuantLib)下载**Quantlib**库。选择库的最新版本，然后开始下载。

– 从[`tortoisesvn.net/downloads.html`](http://tortoisesvn.net/downloads.html)下载**TortoiseSVN**。这是一个用于**Windows**的 subversion 客户端程序。它易于使用，并将允许你获取 Boost 和**Quantlib**的最新文件版本。这个软件也有很好的文档资料([`tortoisesvn.net/docs/release/TortoiseSVN_en`](http://tortoisesvn.net/docs/release/TortoiseSVN_en)）。

– 使用**TortoiseSVN**从[`svn.boost.org/svn/boost/trunk`](http://svn.boost.org/svn/boost/trunk)获取**Boost**文件的最新版本。

– 同样地，从[`quantlib.svn.sourceforge.net/svnroot/quantlib/trunk`](http://quantlib.svn.sourceforge.net/svnroot/quantlib/trunk)更新你的**Quantlib**文件版本。

– 在你的硬盘上**C:\ … \Quantlib\QuantLib**目录中找到**QuantLib_vc10.sln**文件。双击它。Visual Studio 将同时打开 14 个项目。

– 现在，让**Boost**头文件和库对**Quantlib**可用。在解决方案资源管理器中右键点击**QuantLib**项目，然后将你的**C:\ … \boost_1_44**目录添加到**Visual Studio**的“包含文件”目录中（我们假设你没有重命名任何文件）。接下来，将**C:\ … \boost_1_44\lib**添加到“库文件”目录中。

– 你已经准备好构建**Quantlib**库了。在**Visual Studio**的解决方案资源管理器窗口中，右键点击“解决方案‘Quantlib_vc10’（14 个项目）”，并选择“构建解决方案”以构建这 14 个项目。

***– 完成啦！–***

你可以在构建或发布模式下构建解决方案。这真的不重要。重要的是你将不得不以与**Quantlib**相同的模式构建你的未来项目。既然如此，你为什么不在你的电脑上同时以两种模式构建**Quantlib**呢？*
