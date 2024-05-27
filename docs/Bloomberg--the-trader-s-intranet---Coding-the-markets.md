<!--yml

category: 未分类

date: 2024-05-12 19:52:37

-->

# Bloomberg：交易员的内部网 | 编码市场

> 来源：[`etrading.wordpress.com/2006/06/15/bloomberg-the-traders-intranet/#0001-01-01`](https://etrading.wordpress.com/2006/06/15/bloomberg-the-traders-intranet/#0001-01-01)

## Bloomberg：交易员的内部网

### 2006 年 6 月 15 日

我之前已经提到过，交易大厅的屏幕空间是多么珍贵。交易员经常运行的东西之一是他们的[Bloomberg](http://www.bloomberg.com)终端。与我们这些编码人员不同，他们不会有网络、电子邮件和聊天客户端占用那宝贵的屏幕空间。不过，Bloomberg 无论如何都提供电子邮件和聊天功能。因此，当交易员想向大厅的同事发布一些内容时，他们会想要在 Bloomberg 上发布。这些内容可能是一些指标报价或估值。

除了他们的 Bloomberg 之外，交易员总是运行 Excel。因此，我们通过一个[XLL](https://etrading.wordpress.com/excel/)来支持他们的发布需求，该 XLL 可以将 Excel 工作表发送到 Bloomberg 的 GPGX 页面。那是一个 GPGX，不是 GDCO，后者用于可执行报价。点击一个按钮，交易员的自由格式表就出现在 Bloomberg 上。结果：交易员高兴了。

这样做的一个结果是，作为一个组织，我们越来越多地被锁定在那些 Bloomberg 的费用中：每个终端一个月一千美元。
