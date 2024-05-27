<!--yml

分类：未分类

日期：2024-05-18 05:56:53

-->

# 通过演员和未来的流动性管理 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2013/11/28/liquidity-management-through-actors-and-futures/#0001-01-01`](https://mdavey.wordpress.com/2013/11/28/liquidity-management-through-actors-and-futures/#0001-01-01)

基于 Typesafe 最近[博客](http://typesafe.com/blog)关于[akka](http://doc.akka.io/docs/akka/snapshot/scala/actors.html)的酷炫帖子，以及最近一天晚上稍晚些时候——实际上我觉得是午夜过后，但谁在乎呢。我决定采用标准的流动性管理[高级](http://wp.marketfactory.net/aggregator/)级别[架构](http://www.smart-trade.net/products/liquidityfx/)，使用 akka 和[futures](http://doc.akka.io/docs/akka/snapshot/scala/futures.html)实现简单/基本流程。与 Typesafe 最近的[调查](http://typesafe.com/blog/akka-survey-2013-and-roadmap-update)提供的观点类似，我未能利用[TestKit](http://doc.akka.io/docs/akka/current/scala/testing.html) 😦

```

import akka.actor.{ ActorSystem, Props, Actor, Inbox }
import scala.collection.mutable._
import scala.concurrent.ExecutionContext
import akka.util.Timeout
import scala.concurrent.duration._
import scala.concurrent.Future
import akka.pattern.{ ask, pipe }
import ExecutionContext.Implicits.global

case class CorePrice(instrument : String, price : Double)
case class TieredPrice(instrument : String, price : Double)
case class MarketData(instrument : String, price : Double)
case class FIXRFQRequest(instrument : String)
case class RFQ(instrument : String)

class LiquidityConnector(venue : String) extends Actor {
  override def preStart(): Unit = {
    println(s"LiquidityConnector preStart for $venue on $self.path")
  }

  def receive: Actor.Receive = {
    case MarketData(instrument, price) => {
      println(s"Received MarketData from $venue $instrument $price")

      val actor = context.actorSelection("../Aggregator")
      println(s"Sent MarketData to $actor")
      actor ! MarketData(instrument, price)
    }
  }
}

class Aggregator extends Actor {
  override def preStart(): Unit = {
    println("Aggregator preStart " + self.path)
  }

  def receive: Actor.Receive = {
    case MarketData(instrument, price) => {
      println(s"Received MarketData message, sending to CorePricer $instrument $price")
      val actor = context.actorSelection("../CorePricer")
      actor ! MarketData(instrument, price)
    }
  }
}

class CorePricer extends Actor {
  val prices = new HashMap[String, Double]

  def receive: Actor.Receive = {
    case MarketData(instrument, price) => {
      println(s"Received MarketData sending to TieredPricer $instrument $price")
      val currentPrice = if (prices.contains(instrument)) prices(instrument) else 0
      if (currentPrice > 0)
        prices += (instrument -> ((price + currentPrice)/2))
      else
        prices += (instrument -> price)

      val actor = context.actorSelection("../TieredPricer")
      println(s"Received MarketData sending to TieredPricer $instrument $prices(instrument)")
      actor ! CorePrice(instrument, prices(instrument))
    }
  }
}

class TieredPricer extends Actor {
  val prices = new HashMap[String, Double]

  def receive: Actor.Receive = {
    case CorePrice(instrument, price) => {
      prices += (instrument -> price)
    }
    case RFQ(instrument) => {
      val price = prices(instrument)
      println(s"TieredPricer - Sending TieredPrice for RFQ $instrument $price to $sender")
      sender ! TieredPrice(instrument, price)
    }
  }
}

class LiquidityDistributor extends Actor {
  def receive: Actor.Receive = {
    case RFQ(instrument) => {
      val actor = context.actorSelection("../TieredPricer")
      println(s"Sent RFQ to $actor")

      implicit val timeout = Timeout(5 seconds)
      val future : Future[TieredPrice] = ask(actor, RFQ(instrument)).mapTo[TieredPrice]
      pipe(future) to sender
    }
  }
}

class VenueConnectivity(venue : String) extends Actor {
  override def preStart(): Unit = {
    println(s"VenueConnectivity preStart for $venue on $self.path")
  }

  def receive: Actor.Receive = {
    case RFQ(instrument) => {
      println(s"Received RFQ from $venue $instrument")
      val actor = context.actorSelection("../LiquidityDistributor")
      println(s"Sent RFQ to $actor")

      implicit val timeout = Timeout(5 seconds)
      val future : Future[TieredPrice] = ask(actor, RFQ(instrument)).mapTo[TieredPrice]
      pipe(future) to sender
    }
  }
}

object LiquidityManagement extends App {

  val system = ActorSystem("LiquidityManagement")

  val bloombergActor = system.actorOf(Props(classOf[LiquidityConnector], "Bloomberg"), name="Bloomberg")
  val fxAllActor = system.actorOf(Props(classOf[LiquidityConnector], "FxAll"), name="FxAll")
  val aggregator = system.actorOf(Props[Aggregator], "Aggregator")
  val core = system.actorOf(Props[CorePricer], "CorePricer")
  val tiered = system.actorOf(Props[TieredPricer], "TieredPricer")
  val distributor = system.actorOf(Props[LiquidityDistributor], "LiquidityDistributor")
  val hotSpotActor = system.actorOf(Props(classOf[VenueConnectivity], "HotSpot"), name="HotSpot")

  bloombergActor ! MarketData("USD", 12.23)
  fxAllActor ! MarketData("USD", 12.235)

  val inbox = Inbox.create(system)
  inbox.send(hotSpotActor, RFQ("USD"))
  val TieredPrice(instrument, price) = inbox.receive(5.seconds)
  println(s"RFQ Response: $instrument $price")

  system.shutdown();
}

```

~ mdavey 于 2013 年 11 月 28 日。

发表在[语言](https://mdavey.wordpress.com/category/languages/)中

标签：[akka](https://mdavey.wordpress.com/tag/akka/)
