<!--yml

分类：未分类

日期：2024-05-18 06:14:01

-->

# OData 感想 | 交易台故事

> 来源：[`mdavey.wordpress.com/2010/06/15/thoughts-on-odata/#0001-01-01`](https://mdavey.wordpress.com/2010/06/15/thoughts-on-odata/#0001-01-01)

## OData 感想

我今天参加了微软的 OData[路演](http://www.odata.org/roadshow)，有 11 人参加，由[道格拉斯·珀迪](http://www.douglaspurdy.com/)和[乔纳森·卡特](http://www.lostintangent.com/)（微软雷丁三号大楼）推动。很高兴看到道格拉斯有一个 iPad:)

+   网络 API 是世界的中心

+   **NetFlix**（[链接](http://odata.netflix.com/)）在上午的讨论中作为 OData 服务使用。

+   OData 通过 URL 过滤器相当[酷](http://odata.netflix.com/Catalog/Titles?Sfilter=AverageRating%20gt%204%20and%20ReleaseYear%20eq%202008)。

+   页面、顶部、[选择](http://odata.netflix.com/Catalog/Titles('BVeKh'))等均支持 OData

+   目前你无法将自定义 MIME 类型插入到 OData 中，所以你只能使用通常的嫌疑人 - JSON 等

+   根据实体框架使用 Edm 数据模型。

+   在 OData 服务上可以访问[元数据](http://odata.netflix.com/Catalog/%24metadata)。

+   历史悠久的 OData：从 ASMX 到 WS*再到 OData。微软押注于 XML（WS*），但可能是错误的赌注。OData 是赌 HTTP。OData 对浏览器友好！

+   开放数据协议 = HTTP / ATOM + 查询 + JSON + 元数据

+   **IBM**（[链接](http://www.douglaspurdy.com/2010/01/28/websphere-extreme-scale-supports-odata/)）已经在 WebSphere 上实现了 OData。

+   **LINQPad**（[链接](http://dougfinke.com/blog/index.php/2009/12/16/new-linqpad-beta-supports-data-in-the-cloud-odata/)）支持**OData**（[链接](http://odataprimer.com/Default.aspx?Page=UseLinqPadToQueryODataServiceWithLINQ&NS=&AspxAutoDetectCookieSupport=1)）:)

+   OData Objective-C 库可用于 iPad 支持

+   当向 Visual Studio 添加 OData 服务（服务引用）时，可以选择“查看图表”菜单选项以生成服务的好元数据视图

+   微软有一个标准的表达树（LINQ 到 URL）的规范，使 LINQ 表达树能够使用 OData URL 语法，反之亦然在服务器上

+   与乔纳森讨论了一下，财务部门如何使用流媒体服务器而不是 Web 服务来构建 RIA。净额微软正在追求 80%的数据案例，而在金融界（实时网络）中数据的流传输（推送）只是当今世界的一个小子集，因此并没有包含在当前的愿景中。

+   SQL Azure OData [服务](http://blogs.msdn.com/b/netservices/archive/2010/04/20/how-to-use-the-odata-for-sql-azure-with-appfabric-access-control.aspx)

+   自定义[IQueryable](http://weblogs.asp.net/cibrax/archive/2010/03/15/odata-to-the-rescue-exposing-the-eventlog-as-a-data-feed.aspx) OData 对我而言最感兴趣

+   Windows [“达拉斯”](http://www.microsoft.com/windowsazure/dallas/)——数据版本的 iTunes 商店。提供安全、商业模式和托管服务。目前有若干数据[提供商](https://www.sqlazureservices.com/Catalog.aspx)正在利用这个基础设施，好奇是否会有金融服务加入这个行列（也许从贸易研究的角度来看）。

+   道格拉斯个人观点似乎认为，网络（浏览器）是唯一跨平台的解决方案。因此史蒂夫·乔布斯和他的 Adobe Flash 似乎是正确的观点——HTML5 和开放网络标准。而 Adobe Flash 和微软 Silverlight（RIA 世界）是原生平台）。因此 OData 赌的是 HTTP，并且是为网络而设计的。

~ mdavey 于 2010 年 6 月 15 日。

发布于[未分类](https://mdavey.wordpress.com/category/uncategorized/)

标签：[微软](https://mdavey.wordpress.com/tag/microsoft/)
