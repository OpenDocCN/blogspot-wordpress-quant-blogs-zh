<!--yml

category: 未分类

date: 2024-05-18 05:14:45

-->

# Magmasystems 博客：Getting Started with CAB

> 来源：[`magmasystems.blogspot.com/2006/11/getting-started-with-cab.html#0001-01-01`](http://magmasystems.blogspot.com/2006/11/getting-started-with-cab.html#0001-01-01)

由于各种无法启齿的原因，我们将使用 Microsoft 的 Composite Application Block 来启动客户端框架的“顶部部分”。我很高兴终于有机会学习 CAB，并带领团队为我的投资银行做新的客户端框架。

我将尝试记录我学习 CAB 的过程，这样我可以为我的继任者节省一些痛苦。

**CAB 及其附件的安装**

按顺序下载并安装以下文件（确保在安装 GAT 之前安装 GAX）：

1)

[下载](http://www.gotdotnet.com/codegallery/releases/checkForDownload.aspx?id=22f72167-af95-44ce-a6ca-f2eafbf2653c&releaseid=e3136cf0-67dc-41aa-83ff-c10e024503af)

C# 的 Composite Application Block (CAB)

2)

[下载](http://msdn.microsoft.com/library/?url=/library/en-us/dnpag2/html/EntLib2.asp)

Enterprise Library 2006 (

**EntLib**

)

3)

[下载](http://www.microsoft.com/downloads/details.aspx?familyid=C0A394C0-5EEB-47C4-9F7B-71E51866A7ED&displaylang=en)

the Guidance Automation Extensions (

**GAX**

)

4)

[下载](http://www.microsoft.com/downloads/details.aspx?FamilyId=E3D101DB-6EE1-4EC5-884E-97B27E49EAAE&displaylang=en)

the Guidance Automation Toolkit (

**GAT**

)

(此时，在安装智能客户端软件工厂之前，您必须使用位于目录 *C:\Program Files\Microsoft Composite UI App Block\CSharp* 中的 *CompositeUI.sln* 解决方案文件构建 CAB。您还必须在安装 SCSF 之前关闭 Visual Studio。)

5)

[下载](http://www.microsoft.com/downloads/info.aspx?na=47&p=1&SrcDisplayLang=en&SrcCategoryId=&SrcFamilyId=7B9BA1A7-DD6D-4144-8AC6-DF88223AEE19&u=details.aspx%3ffamilyid%3d2B6A10F9-8410-4F13-AD53-05A202FBDB63%26displaylang%3den)

智能客户端软件工厂（2006 年 6 月版）(

**SCSF**

)

6)

[下载](http://www.microsoft.com/downloads/details.aspx?familyid=AB44F082-3ABE-4583-8844-7252FF7C9638&displaylang=en)

CAB 实践实验室

7)

[下载](http://www.gotdotnet.com/codegallery/releases/viewuploads.aspx?id=22f72167-af95-44ce-a6ca-f2eafbf2653c)

[CAB 入门文档](https://wiki.example.org/intro_to_cab_document) 和 CAB 帮助文件（你可能想要在桌面上创建这些文件的快捷方式）。

8) 下载示例可视化

如果卸载 GAX 或 GAT 出现问题，请阅读

[此处](http://forums.microsoft.com/MSDN/ShowPost.aspx?PostID=525052&SiteID=1)

.

**资源**

·

[CAB 主页](http://practices.gotdotnet.com/projects/cab)

位于 GotDotNet 的 Microsoft Patterns and Practices 领域

·

[CabPedia](http://www.cabpedia.com/index.php?title=Main_Page)

·

[MSDN Magazine 文章](http://msdn.microsoft.com/msdnmag/issues/06/09/SmartClients/default.aspx)

·

[CAB 入门](http://weblogs.asp.net/bsimser/archive/2006/07/27/Composite-UI-Application-Block-_2D00_-Soup-to-Nuts-_2D00_-Getting-Started.aspx)

在 Fear and Loathing 博客上

·

[理解 CAB](http://geekswithblogs.net/kobush/archive/2006/01/06/65033.aspx)

在 Szymon 的博客上的一系列文章

**类层次结构**

以下是 CAB 中主要类的图表：

![](http://photos1.blogger.com/blogger/138/258/1600/CAB%20Class%20Hierarchy.jpg)

©2006 Marc Adler - 版权所有
