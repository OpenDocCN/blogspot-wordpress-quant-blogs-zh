<!--yml
category: 未分类
date: 2024-05-18 06:16:55
-->

# BUILD: Windows Server 8 – Thoughts | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2011/09/21/build-windows-server-8-thoughts/#0001-01-01](https://mdavey.wordpress.com/2011/09/21/build-windows-server-8-thoughts/#0001-01-01)

## BUILD: Windows Server 8 – Thoughts

Metro has been the main blogging topic from BUILD, few have blogged about Windows Server 8 that was featured in a number of BUILD sessions. Windows Server 8 is cloud optimised, offering a number of interesting features that are relevant to financial services applications:

*   Large scale systems – 640 logical processors are supported and 4 Terebytes of memory
*   Windows client and server are leveraging the same codebase
*   Registered IO (RIO) – Winsock extension API’s that pin’s buffers in user space, which reduces CPU processing of each message
*   Receive Side Scaling (RSS) distributes TCP/UDP receive traffic across nodes
*   Windows Server Core is the preferred deployment option – finally the GUI is dead (although still available if you really need it) and PowerShell runs the server admin world
*   WebSockets added to ASP.NET, IIS 8.0 and WCF, .NET 4.5 – Microsoft finally gets web PUSH but only via W3C

~ by mdavey on September 21, 2011.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [BUILD](https://mdavey.wordpress.com/tag/build/), [Microsoft](https://mdavey.wordpress.com/tag/microsoft/)