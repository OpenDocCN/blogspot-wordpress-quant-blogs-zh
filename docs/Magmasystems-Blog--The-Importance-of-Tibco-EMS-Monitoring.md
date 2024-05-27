```yaml

分类：未分类

日期：2024-05-18 05:01:37

的命令行应用程序。

# Magmasystems Blog: Tibco EMS 监控的重要性

> 来源：[`magmasystems.blogspot.com/2008/06/importance-of-tibco-ems-monitoring.html#0001-01-01`](http://magmasystems.blogspot.com/2008/06/importance-of-tibco-ems-monitoring.html#0001-01-01)

如果你正在使用

Tibco

EMS，你应该知道有一个不错的工具随

Tibco SDK

允许你监控在你经纪人中进行的所有活动。在目录

***c:\tibco\ems\bin***

，你会发现一个名为

***tibemsmonitor.exe***

。如果你运行这个实用程序，你可以看到每一个连接/断开，每一个主题或队列的创建和销毁的

消息生产者

和

MessageConsumer

，每一个主题或队列的创建。

为了优化我们的代码，我开始监视 EMS 和我们的应用程序之间的交互。我发现我们正在创建

MessageProducers

太多次了...对于一个做大量实时消息处理的程序来说，次数太多。

我很好奇地想看看创建消息生产者和消费者的背后发生了什么。所以，我启动了非常有价值的 Reflector（来自

Lutz Roeder

）并窥视了

***Tibco.EMS.dll***

汇编。我发现的是，每次创建一个消息生产者或消费者时，该

***Tibco.EMS._CreateMessageProducer***

函数构建消息，将其发送到经纪人，并同步等待响应。这需要花费大量的时间并产生大量的开销。

我修改了我们的代码，现在我们缓存并重复使用

MessageProducers

。我必须说，我们的代码看起来现在运行得快多了。快得多....

由于这个问题中的代码是我两年前写的，我以为它没问题，因为咱们公司有大约十几个小组在使用这个代码。而且，它确实运行良好，除了产生了大量不必要的开销。对于这个错误，我愿意接受十下湿面条的鞭刑 ....

学到的教训是：

1) 优化，优化，优化

2) 那些你正在使用的构成你框架基础的旧代码可能需要监控。

3) 使用 Reflector 来查看底层库正在做什么。

***©2008 Marc Adler - All Rights Reserved.*** ***所有在这里的意见都是个人的，与我雇主无关。***
