<!--yml

分类：未分类

date: 2024-05-18 05:15:25

-->

# Magmasystems Blog: 对象缓存考虑因素（第二部分）

> 来源：[`magmasystems.blogspot.com/2006/11/object-cache-considerations-part-2.html#0001-01-01`](http://magmasystems.blogspot.com/2006/11/object-cache-considerations-part-2.html#0001-01-01)

**对象版本控制**

你可以将对象的“版本”看作是两回事。

在第一种情况下，一个对象的“版本”可以代表该对象被写入的次数。当一个对象第一次被创建时，它的版本号被设置为 1，然后每次客户端更新该对象时，版本号都会增加。因此，我们可以在对象缓存中调用一个 API，以检查我们是否持有最新版本：

if (!ObjectCache.IsCurrent(object))

object = ObjectCache.Get(object.Key);

或者，如果我们使用的是具有到缓存的代理的对象，我们可以这样做：

if (!object.IsCurrent())

object.Refresh();

在第二种（并且复杂得多）情况下，“版本”可以代表对象类的实际布局或形状。考虑一个 Trade 对象：

public class Trade : CachedObject

{

public int SecurityId;

public double Price;

}

这是该类的 1.0 版。

假设我们有一个必须 24x7 运行的交易系统，这是当前的趋势。24x7 运行的系统在理论上没有重启的机会。即使是 24x6.5 运行的系统也有维护窗口。我们的交易系统拥有 Trade 对象的 1.0 版。

假设我们现在有一个请求，需要将销售归因添加到交易系统中，因此现在我们需要添加执行交易请求的销售交易员的 id。

public class Trade : CachedObject

{

public int SecurityId;

public double Price;

public int BrokerId;

}

这是该课程的 1.1 版。

我们的对象缓存包含 1.0 版对象，所有订阅者也持有 1.0 版对象。但是，现在假设将新交易写入对象缓存的系统现在必须写入 1.1 版对象。我们该怎么办？

这里有几件事情需要考虑。我们如何表示缓存中的对象？因为我们在使用名称/值对，所有新对象都将具有 BrokerId/

<id>字段已添加。旧的 1.0 对象不需要更改。

对象缓存可能希望向所有订阅者广播一条消息，告诉他们 Trade 对象的版本号已更改。由于订阅者可能是必须 24x7 运行的系统，因此系统可能无法重新启动以重建其交易缓存。系统必须能够读取和写入新版本 1.1 对象，同时继续支持旧版本 1.0 对象。但是，我们能否动态地重新配置对象的结构呢？

我们可能会考虑使用字典的字典来表示应用程序的对象缓存，而不是使用 C#对象。但这是一种不同的编程模型。我们不是编写：

Trade obj = ObjectCache.Get("102374");

经纪人 = obj.BrokerId;

我们可能需要做以下事情（利用 C# 2.0 的可空类型）:

TradeDictionaryObject obj = ObjectCache.Get("1002374");

int? 经纪人 = obj.GetInt("BrokerId");

多么混乱啊！

这告诉我们什么？在为 24x7 系统使用对象缓存时，确保你第一次就获得你的类定义正确，并避免对象版本化！

©2006 Marc Adler - 版权所有</id>
