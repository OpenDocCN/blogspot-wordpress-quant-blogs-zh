<!--yml

分类：未分类

日期：2024-05-12 19:31:04

-->

# 升级 SpreadServe GUI | 编码市场

> 来源：[`etrading.wordpress.com/2015/09/19/upgrading-the-spreadserve-gui/#0001-01-01`](https://etrading.wordpress.com/2015/09/19/upgrading-the-spreadserve-gui/#0001-01-01)

## 升级 SpreadServe GUI

### 2015 年 9 月 19 日

最近我一直在更新[SpreadServe](http://spreadserve.com)的 JavaScript 网络 GUI。 livesheet 页面上的编辑功能相当原始。它使用了一个[bootstrap-editable](https://vitalets.github.io/x-editable/)在消息框中弹出一个编辑字段。并不是真正的无缝用户体验，所以我升级到了支持现场编辑的 JavaScript 网格。最终结果是用户体验更接近 Excel 本身。我选择使用[webismymind 的 editablegrid](https://github.com/webismymind/editablegrid)，因为它可以附着到现有的 HTML 表格上。在 SpreadServe 的情况下，HTML 表格是在运行中的电子表格发布到[RealTimeWebServer](http://spreadserve.readthedocs.org/en/latest/config.html?highlight=realtimewebserver)时，由 C++代码在[SpreadServeEngine](http://spreadserve.readthedocs.org/en/latest/guide.html)内生成的。我将 C++代码更改为给表格和 tr 元素添加属性，editablegrid 使用这些属性来锁定。我对 editablegrid 的 JavaScript 做了一些小修改，使 isEditable 和 modelChanged 回调传递更多信息。我的 isEditable 实现需要获取 DOM 元素以及行列地址，以便检查是否有 ssedit 属性。 modelChanged 需要元素 ID，以便它可以带有唯一 ID 将更改后的数据发送回 RealTimeWebServer。 RealTimeWebServer 将更新后的值发送回 SpreadServeEngine。我在[github 上](https://github.com/osullivj/editablegrid)分叉了带有我更改的 editablegrid。在做这个 JS 开发时，我发现了两个非常有用的资源： [Oscar Rotero 的 jQuery 速查表](http://oscarotero.com/jquery/)，以及[Chrome 调试器](https://developer.chrome.com/devtools)。我曾经是 Firefox 的倡导者很长时间，因为 Firebug 是我使用的第一个 JavaScript 调试器。Chrome 调试器就是更快，更敏捷，设置断点更容易，检查 DOM 和变量也更好。
