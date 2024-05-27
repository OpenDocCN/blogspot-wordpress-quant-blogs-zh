<!--yml

类别：未分类

date: 2024-05-18 04:57:45

-->

# Magmasystems Blog：微软奥索洛（Microsoft Oslo）SDK 安装失败

> 来源：[`magmasystems.blogspot.com/2008/11/microsoft-oslo-sdk-setup-failure.html#0001-01-01`](http://magmasystems.blogspot.com/2008/11/microsoft-oslo-sdk-setup-failure.html#0001-01-01)

看起来你需要安装 SQL Server 2008 才能使用奥索洛。微软在任何地方都没有提到这一点，它的安装程序也没有警告你。以下是我在尝试在笔记本电脑上安装奥索洛的经历。

1) 我从微软网站下载了奥索洛 SDK CTP。

2) 我解压了文件，并运行了安装程序。安装程序顺利完成，没有警告和错误信息。到目前为止还好。

3) 我的电脑安装了 Windows Vista SP1，同时安装了 SQL Server 2005 和 SQL Server Express 2005。我打开 SQL Server Management Studio 并搜索了奥索洛仓库的任何痕迹。没有找到。

4) 在目录

C:\Users\Marc\AppData\Local\Temp

，我发现了一个名为

Oslo_Repository_Setup.log

. 我用记事本打开了这个文件，并发现了以下几行：

Property(C)：ExecuteSilentCmd = "C:\Program Files\Microsoft Repository\CreateRepository.exe" /v+

Property(C): WIXUI_EXITDIALOGOPTIONALTEXT = 警告：仓库数据库创建失败。请查看 %temp%\RepositorySetup.log 以获取更多详细信息。

然而，在文件的末尾，我发现了以下几行：

MSI (c) (B0:48) [06:51:33:985]：产品：微软代号“奥索洛”仓库 -- 安装成功。

MSI (c) (B0:48) [06:51:33:987]：Windows Installer 安装了产品。产品名称：微软代号“奥索洛”仓库。产品版本：3.0.1342.0。产品语言：1033。安装成功或错误状态：0。

所以，看起来安装程序认为安装成功，尽管无法创建仓库。

5) 在 RepositorySetup.log 文件中，我发现了以下几行：

message: 创建仓库数据库...

错误：不能为局部变量分配默认值。

必须声明标量变量 "@login"。

[11/3/2008 - 6:51:24]已完成执行： "C:\Program Files\Microsoft Repository\CreateRepository.exe" /v+

6) 我们看到其他用户也遇到了

[已报告此问题](https://connect.microsoft.com/oslo/feedback/ViewFeedback.aspx?FeedbackID=378415)

. 微软表示这并非一个错误，而是“设计如此”。

7) 在

[这个链接](http://social.msdn.microsoft.com/Forums/en-US/oslo/thread/c0ee4730-4595-4971-a2f3-a988997c4616)

，我们发现微软的卡洛斯·戈麦斯（Carlos Gomez）留下了一条评论：

我们完全不支持 SQL Server 2005，因为一些仓库功能依赖于 SQL Server Katmai。

换句话说，你需要安装 SQL Server 2008。嗯，我们公司还在用 SS 2005，所以我猜奥索洛（Oslo）将只在我的个人实验中使用，至少在可预见的未来是这样。

©2008 Marc Adler - 保留所有权利。

在此表达的所有意见都是个人的，与我的雇主无关。
