<!--yml

类别：未分类

日期：2024 年 05 月 18 日 06:16:55

-->

# BUILD：Windows Server 8 – Thoughts | 交易台的故事

> 来源：[`mdavey.wordpress.com/2011/09/21/build-windows-server-8-thoughts/#0001-01-01`](https://mdavey.wordpress.com/2011/09/21/build-windows-server-8-thoughts/#0001-01-01)

## BUILD：Windows Server 8 – Thoughts

Metro 一直是 BUILD 的主要博客话题，很少有人写过在多个 BUILD 会议中展示的 Windows Server 8。Windows Server 8 是云优化的，提供了一些对金融服务应用程序相关的有趣功能：

+   大型系统 – 支持 640 个逻辑处理器和 4 TB 内存

+   Windows 客户端和服务器正在利用相同的代码库

+   Registered IO (RIO) – Winsock 扩展 API，将缓冲区固定在用户空间，减少了每个消息的 CPU 处理

+   接收端扩展（RSS）将 TCP/UDP 接收流量分配到节点

+   Windows Server Core 是首选的部署选项 – 最终 GUI 已死（尽管如果你真的需要的话仍然可用），PowerShell 主导着服务器管理世界

+   WebSockets 添加到 ASP.NET、IIS 8.0 和 WCF、.NET 4.5 – 微软终于通过 W3C 获得了 Web PUSH，但仅限于 W3C

~ 由 mdavey 于 2011 年 9 月 21 日发布。

发布于[未分类](https://mdavey.wordpress.com/category/uncategorized/)

标签：[BUILD](https://mdavey.wordpress.com/tag/build/)，[Microsoft](https://mdavey.wordpress.com/tag/microsoft/)
