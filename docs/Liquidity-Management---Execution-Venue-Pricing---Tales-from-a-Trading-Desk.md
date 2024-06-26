<!--yml

日期：2024-05-18 05:56:44

```diff

-->

# 来源：[`mdavey.wordpress.com/2013/12/03/liquidity-management-execution-venue-pricing/#0001-01-01`](https://mdavey.wordpress.com/2013/12/03/liquidity-management-execution-venue-pricing/#0001-01-01)

> ~ mdavey 于 2013 年 12 月 3 日。

## 分类：未分类

流动性管理——执行场所定价

```
  // A random data set which uses stockQuote.newPrice to get each data point
  var stockHistory: Queue[java.lang.Double] = {
    lazy val initialPrices: Stream[java.lang.Double] = (new Random().nextDouble * 800) #:: initialPrices.map(previous => stockQuote.newPrice(previous))
    initialPrices.take(50).to[Queue]
  }

  // Fetch the latest stock value every 75ms
  val stockTick = context.system.scheduler.schedule(Duration.Zero, 75.millis, self, FetchLatest)

```

我也开始增加对[Testkit](http://doc.akka.io/docs/akka/current/scala/testing.html)测试覆盖的基本内容：流动性管理——执行场所定价 | 交易桌面故事

```

class TieredPricerSpec(_system: ActorSystem)
  extends TestKit(_system)
  with ImplicitSender
  with ShouldMatchers
  with FlatSpec
  with BeforeAndAfterAll {

  def this() = this(ActorSystem("LiquidityManagementSpec"))

  override def afterAll: Unit = {
    system.shutdown()
    system.awaitTermination(10.seconds)
  }

  "An TieredPricer" should "be able to store a price" in {
    val actor = TestActorRef(Props[TieredPricer])
    actor ! CorePrice("GBPUSD", 1.5)
    actor.underlyingActor.asInstanceOf[TieredPricer].prices("GBPUSD") should be(1.5)
  }

  it should "be able to store two price" in {
    val actor = TestActorRef(Props[TieredPricer])
    actor ! CorePrice("GBPUSD", 1.5)
    actor ! CorePrice("GBPEUR", 1.15)
    actor.underlyingActor.asInstanceOf[TieredPricer].prices("GBPUSD") should be(1.5)
    actor.underlyingActor.asInstanceOf[TieredPricer].prices("GBPEUR") should be(1.15)
  }

  it should "be able able to provide a price given an RFQ" in {
    val actor = TestActorRef(Props[TieredPricer])
    actor ! CorePrice("USDEUR", 1.15)
    actor ! RFQ("USDEUR")
    expectMsgType[TieredPrice].price should be(1.15)
  }
}

```

在一些深夜编码 session 中，我重构了之前博客中发布的演员流动性管理代码，并从 Typesafe 的 Reactive Stock [示例](http://typesafe.com/activator/template/reactive-stocks)中借用了几行代码——具体是价格生成器：

发表于 [Languages](https://mdavey.wordpress.com/category/languages/)
