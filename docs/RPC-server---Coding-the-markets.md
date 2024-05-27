<!--yml

分类：未分类

日期：2024-05-12 19:41:32

-->

# RPC 服务器 | 编写市场代码

> 来源：[`etrading.wordpress.com/2008/08/18/rpc-server/#0001-01-01`](https://etrading.wordpress.com/2008/08/18/rpc-server/#0001-01-01)

## RPC 服务器

### 2008 年 8 月 18 日

刚刚完成了我的 RPC 服务器的第一次切割，这是用 Python 编写的。在浏览器中运行的客户端 JavaScript 代码订阅了 Liberator 主题，这会在 RPC 服务器中触发一个订阅请求。服务器将缓存的静态数据通过 Liberator 主题发送回客户端。数据以序列化的 Python 字典形式发送。因此，在服务器端我们只需对 Python 字典应用 str()。当数据到达浏览器时，我们可以使用 JavaScript eval()将其转换为 JavaScript 对象。简单而灵活！
