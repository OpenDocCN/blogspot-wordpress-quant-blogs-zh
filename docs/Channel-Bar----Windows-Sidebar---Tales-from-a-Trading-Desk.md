<!--yml

分类：未分类

日期：2024 年 5 月 18 日 06:04:31

-->

# 频道栏 -> Windows 侧边栏 | 交易台的故事

> 来源：[`mdavey.wordpress.com/2006/07/14/channel-bar-windows-sidebar/#0001-01-01`](https://mdavey.wordpress.com/2006/07/14/channel-bar-windows-sidebar/#0001-01-01)

## 频道栏 -> Windows 侧边栏

今天一个同事提醒我 Windows 98 的 [活动桌面频道栏](http://www.smartcomputing.com/editorial/article.asp?article=articles/archive/2win98/29824/29824.asp&guid=)。稍微花点时间看了一下 [Windows 侧边栏](http://www.microsoft.com/windowsvista/features/foreveryone/sidebar.mspx)，我可以看到与 Windows 98 之间的联系。我想知道最初的频道栏开发者是否帮助了 Windows 侧边栏。微软的小工具网站是你查看如何构建 [小工具](http://microsoftgadgets.com/) 的第一站。

查看 [开发概览](http://microsoftgadgets.com/Sidebar/DevelopmentOverview.aspx) 文档，似乎没有太多关于安全性的描述。考虑到部署机制是 CAB/ZIP，没有签名过程，而且 [对象模型](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/sidebar/sidebar/reference/refs.asp) 似乎允许执行 [命令](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/sidebar/sidebar/reference/objects/systemshell/drive.asp) 并访问 [驱动器/文件夹](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/sidebar/sidebar/reference/objects/systemshellfolder/systemshellfolder.asp)，我假设必须有一些安全机制存在？

~ 由 mdavey 于 2006 年 7 月 14 日发布。

发布在[未分类](https://mdavey.wordpress.com/category/uncategorized/)中。

标签：[微软](https://mdavey.wordpress.com/tag/microsoft/)
