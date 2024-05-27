<!--yml

分类：未分类

日期：2024-05-12 19:17:50

-->

# 量化交易：MATLAB 作为自动化交易系统

> 来源：[`epchan.blogspot.com/2009/05/matlab-as-automated-execution-system.html#0001-01-01`](http://epchan.blogspot.com/2009/05/matlab-as-automated-execution-system.html#0001-01-01)

我刚刚发布了一篇文章 "

[MATLAB 作为自动化交易系统](http://www.epchan.com/subscription/matlabexecution.pdf)

". (它对我的书读者和我的

[高级内容](http://www.epchan.com/subscriptions.html)

网站读者开放。它包含了

[示例 MATLAB 代码](http://epchan.com/book/bollinger.m)

执行一个简单的 Bollinger 带高频 E-mini 交易策略。

如我之前提到的，我现在发现 MATLAB 不仅仅是一个好的回测平台，也是一个好的自动化交易平台。当然，并非所有经纪商都有连接到 MATLAB 的 API。我的示例代码是用于向 Interactive Brokers 账户自动提交订单的。

总的来说，我发现用 MATLAB 编写执行程序比用 C++、Java 甚至 C# 都要简单。MATLAB 程序的开发时间大约是 C++ 程序的 1/5。任何性能限制可能都不是 MATLAB 造成的，而是因为你的经纪商更新持仓和订单状态的延迟。
