<!--yml

分类：未分类

日期：2024-05-18 04:51:13

-->

# Magmasystems Blog：首次使用 RX 框架的实验

> 来源：[`magmasystems.blogspot.com/2009/12/first-experiment-with-rx-framework.html#0001-01-01`](http://magmasystems.blogspot.com/2009/12/first-experiment-with-rx-framework.html#0001-01-01)

首次使用 RX 框架的实验。这为 4 只不同的股票生成了 5 个股价。

```

using System;
using System.Collections.Generic;
using System.Linq;

namespace RXStockGenerator
{
    class TestRX
    {
        public TestRX()
        {
            using (new StockPriceGenerator().Subscribe(q => Console.WriteLine("Quote: " + q)))
            {
                Console.WriteLine("Press any key to unsubscribe");
                Console.ReadKey();
            }
        }
    }

    class StockPriceGenerator : IObservable<StockQuote>
    {
        private readonly Random m_random;

        public StockPriceGenerator()
        {
            this.m_random = new Random();
        }

        public IDisposable Subscribe(IObserver<StockQuote> observer)
        {
            List<IObservable<StockQuote>> generators = new List<IObservable<StockQuote>>
            {
                this.Generate("AAPL", 200.00, 100),
                this.Generate("IBM", 120.00, 150),
                this.Generate("MSFT", 30.00, 125),
                this.Generate("GE", 15.00, 175),
            };

            return generators.Merge().Subscribe(observer);
        }

        public IObservable<StockQuote> Generate(string symbol, double startPrice, int delay)
        {
            return Observable.Generate(
                0,
                i => i < 5,
                _ => new StockQuote(symbol, startPrice + this.m_random.NextDouble()),
                _ => TimeSpan.FromMilliseconds(delay),
                i => i + 1);
        }
    }

    class StockQuote
    {
        public string Symbol { get; set; }
        public double Price { get; set; }

        public StockQuote(string symbol, double price)
        {
            this.Symbol = symbol;
            this.Price = price;
        }

        public override string ToString()
        {
            return string.Format("{0}/{1:##.#0}", this.Symbol, this.Price);
        }
    }
}

```
