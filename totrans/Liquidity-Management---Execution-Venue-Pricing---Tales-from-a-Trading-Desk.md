<!--yml
category: 未分类
date: 2024-05-18 05:56:44
-->

# Liquidity Management – Execution Venue Pricing | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/12/03/liquidity-management-execution-venue-pricing/#0001-01-01](https://mdavey.wordpress.com/2013/12/03/liquidity-management-execution-venue-pricing/#0001-01-01)

## Liquidity Management – Execution Venue Pricing

During some late night code sessions, I’ve refactored the previous blogged actor liquidity management code, and borrowed a few lines of code from Typesafe’s Reactive Stock [sample](http://typesafe.com/activator/template/reactive-stocks) – specifically the price generator:

```
  // A random data set which uses stockQuote.newPrice to get each data point
  var stockHistory: Queue[java.lang.Double] = {
    lazy val initialPrices: Stream[java.lang.Double] = (new Random().nextDouble * 800) #:: initialPrices.map(previous => stockQuote.newPrice(previous))
    initialPrices.take(50).to[Queue]
  }

  // Fetch the latest stock value every 75ms
  val stockTick = context.system.scheduler.schedule(Duration.Zero, 75.millis, self, FetchLatest)

```

I also made a basic start to adding [Testkit](http://doc.akka.io/docs/akka/current/scala/testing.html) test coverage:

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

~ by mdavey on December 3, 2013.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/)