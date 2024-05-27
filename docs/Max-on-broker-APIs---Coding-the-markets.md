<!--yml

类别：未分类

日期：2024-05-12 19:38:10

-->

# Max 关于经纪 API 的观点 | 编码市场

> 来源：[`etrading.wordpress.com/2009/11/23/max-on-broker-apis/#0001-01-01`](https://etrading.wordpress.com/2009/11/23/max-on-broker-apis/#0001-01-01)

## Max 关于经纪 API 的观点

### 2009 年 11 月 23 日

[Max](http://www.maxdama.com) Dama 最近在[经纪 API](http://www.maxdama.com/2009/11/api-translation.html)上[发表了几篇文章](http://www.maxdama.com/2009/11/thoughts-on-apis-ib-lime-wex.html)。在他最近的一篇帖子中，他在谈到 IB、Wex 和 Lime 时提到了一个有趣的附言：“我没有使用过这三家公司的 FIX API”

这让我想到一个问题：为什么不是呢？为什么我们要针对一个专有 API 编程，而不是一个行业标准协议。我自己对 FIX 用于固定收益产品的体验并不愉快，所以我猜测的原因可能是…

+   便利性：直接使用 Java 或.Net API 比选择 quickfix.org 等 FIX 实现和/或协议实现更快，然后进行集成。

+   有状态性：据我所知，FIX 并没有解决诸如“订单提交”、“订单在册”、“订单取消”等状态问题。一个组织良好的 API 搭配一个良好的回调接口可以更早地实现这类功能。FIX 只是一个协议，让你自己来构建这些功能。

+   速度：减少基础设施意味着减少延迟。

我想知道 FIX 在提供连接服务的卖方公司中是否比买方更受欢迎。从 Max 的帖子来看，他正在为构建自动化交易系统的对冲基金做连接工作，使用的就是他提到的那些经纪 API。我很想知道这些公司选择使用专有 API 的原因…
