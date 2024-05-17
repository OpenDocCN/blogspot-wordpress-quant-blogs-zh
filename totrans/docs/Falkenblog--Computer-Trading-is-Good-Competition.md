<!--yml
category: 未分类
date: 2024-05-12 21:52:59
-->

# Falkenblog: Computer Trading is Good Competition

> 来源：[http://falkenblog.blogspot.com/2009/07/computer-trading-is-good-competition.html#0001-01-01](http://falkenblog.blogspot.com/2009/07/computer-trading-is-good-competition.html#0001-01-01)

Paul Wilmott today

[warns us](http://www.nytimes.com/2009/07/29/opinion/29wilmott.html?_r=1&ref=opinion)

against the scourge of computer trading, and it seems everyone has an opinion on it (see

[NYTimes](http://www.nytimes.com/2009/07/24/business/24trading.html)

,

[Trader Magazine](http://www.tradersmagazine.com/issues/20_296/-103978-1.html?zkPrintable=true)

,

[Chuck Schumer](http://www.nytimes.com/reuters/2009/07/28/business/business-us-financial-regulation-flash.html)

,

[Tyler Cowen](http://www.marginalrevolution.com/marginalrevolution/2009/07/highfrequency-trading.html)

). Alas, this covers such a broad umbrella of strategies, one can be against this only like one may dislike unpopular books. The panic piece begins as follows:

> The idea is straightforward: Computers take information — primarily “real-time” share prices — and try to predict the next twitch in the stock market. Using an algorithmic formula, the computers can buy and sell stocks within fractions of seconds, with the bank or fund making a tiny profit on the blip of price change of each share.

This has been ongoing with Moore's law. In the bad old days orders were given to a human (called a 'specialist') who then had the ability to accept, or back away, from orders as they came in. With electronic exchanges, much of this is being done not by a priviledged specialist, but rather computers. They basically do the same thing, only now their is much more competition. Remember back in the 1990s when

[Harris, Christie and Schultz](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=5657)

and reported tha Nasdaq quotes bizarrely omitted 'odd eigths'. That is, the could post a bid-ask as 3/8-1/2, but instead regularly posted 1/4-1/2\. This was for many very large companies such as Microsoft and Apple, that even then traded millions of shares a day. This was collusion, and shortly after the publication of this piece these stocks magically began trading at odd eigths, though no one was ever convicted of any collusion.

Stock specialists who consolidate retail orders to buy and sell have been ripping off customers since trading began. The first head of the SEC was Joe Kennedy, who was a master stock manipulator in the 1920's. He was a master of the stock pool (bucket shop), a then-legal stunt in which a few traders conspired to inflate a stock's price, selling out just before the bubble burst. Regulation to protect the integrity of the investor invariably meant stiflying competition, allowing the big exchanges (NYSE and AMEX) to make easy money by being 'in the club'. For generations, specialists would sit on trades for minutes, not milliseconds, while they decided how to maximize their profits. I know one guy who worked for a specialist around 2000, and he noted his boss lost money only a handful of days every year. Specialists would emphasize the risk they took in providing liquidity, yet on big gap days like October 19 1987 they did not step in and exacerbated the situation. The risk they took on providing orderly markets was a license to steal for decades, and they now scream 'unfair!' as their order flow evaporates.

With electronic exchanges, the competition is much greater. Bid-ask spreads are only a penny for most S&P500 companies (as opposed to 25 cents 20 years ago), and they are generally very deep. It is rumored that Renaissance's flagship hedge fund (not the long only fund) makes most of its money as an off-the-exchange market maker. They invested a lot of money in computers, and algorithms that efficiently set bids and offers given recent order flow, the depth of the market (level 2 quotes), and their own inventory. Good for them.

There are basically three types of algorithmic trading strategies. In one, you are basically slicing a big order into littler bits to minimize trade impact. No longer do you need a human to work a 5000 share order, rather, a machine spits it into digestable chunks and by the day you are done, and don't owe anyone a big holiday basket for their hard work. In another, you basically have a machine implement relative value trades. The famous pairs trading, where if Pepsi rises, but Coke stays flat, you sell Pepsi and buy coke, is based on this idea. But it can be generalized to indices versus sectors, or baskets against each other based on statistical properties, or even oil futures vs. Exxon. Lastly, there are the market making algorithms that try to capture the spread in the market by correctly anticipating the future distribution of retail order flow based on the current book, and this strategy can complement a relative value trading algorithm. Many times these algorithms try to reverse engineer future trades via the way current trades are coming in. As many trades come in each second, for many stocks the best bids and offers are adjusted several times a second.

One article noted that some algorithms basically infer the price increase from trades, getting rid of the profits otherwise available. But these are all short term scenarios, and basically make a market efficient. That is, say Apple announces good news, suggesting a sharpe bounce in the stock. An investor tries to buy, and would like to trade 1MM shares, but clearly that's too much, so he puts in an order for 1000, then next minute, another 1000, and another. A machine might sense the pattern and basically jump on for the ride with him, diluting his profits. Is that bad news? Only for the short-term trader. For the longer run investor oblivious to this, who was on the other side, they got to sell at a higher price (the price rose faster than otherwise). The short-term speculator basically makes less because the algorithm reverse engineers his insight. This is the essence of an informationally efficient market, where news gets into the price asap. That those at the bleeding edge are making a profit is not a bug, it's a feature.

Several bloggers have made a big deal out of

['flash trading' article](http://www.tradersmagazine.com/issues/20_296/-103978-1.html?zkPrintable=true)

in Traders Magazine, where exchanges give priviledged access to order flow, letting them accept or reject these trades prior to hitting the general market. Normally this would upset me, but they have an option lasting only 30 milliseconds (30 thousandths of a second). For a computer, this is enough time to make a decision. This is certainly enough time to make a tenth of a cent or so on market orders by leaning on the existing book. That is, if the market is bid-ask at 10.03-05, with 100 shares on each, a market order to buy 100 shares might make you hit the offer at 10.05 because you know there is 100 shares following you, and you hope the price increases based on this flow. This is known as 'front running'. Or you might see more buying coming in at a limit price of 10.02, and decide to increase your bid at 10.03 because you know your downside is now limited to a penny, as you can sell at 10.02 in size. This is known as pennying a bid, because you basically use the other person's limit orders as a backstop, giving you a penny downside risk. As tendencies move probabilistically, on any one trade such shenanigans are worth much less than a penny, but it can add up for the one doing it. For your average investor, in contrast, it is totally irrelevant. In the context of buying a $20 stock, does the fact that a highly competitive group can make tenths of a cent on market transactions bother me? No. It is orders of magnitude lower than 10 years ago, which is orders of magnitude lower than 30 years ago. Commissions for most investors are at least a penny. Of all the financial skullduggery in the world today, Flash Trade front running worth a fraction of a penny is small beer.

But Wilmott paints a scary picture:

> the problem with the sudden popularity of high-frequency trading is that it may increasingly destabilize the market. Hedge funds won’t necessarily care whether the increased volatility causes stocks to rise or fall, as long as they can get in and out quickly with a profit. But the rest of the economy will care.

I surmise that poor Paul has not been invited to consult on these algorithms, and like many experts, finds those excelling at something in his field of expertise is useless at best, but probably damaging. After all, if it was important and useful, he should be a player, because that's his wheelhouse, right? Of course, given the many different types of algorithms extant, it

could

be they glom on to some vicious positive-feedback loop, but given the profits they are chasing, these are micro-bubbles, a couple pennies. An algorithm chasing micropennies does not instigate trends the way portfolio insurance did in the 1987 crash, because in that case long-only funds were looking at their total long position, selling into declines (emulating a put option). The current algorithms generally look at relative value trades between sectors or issues, momentary order imbalances, a very different beast. Trade imbalances have always and will continue to move prices, but that isn't the computers fault. If there's continually 10x as many sell orders as buy orders, the result is going to be lower prices no matter what market is created. When buys and sells are coming in with equal size, price stability will be restored. To suggest the computers could exaggerate a movement is hysterical fear mongering in this context, because while anything is possible, it's a baseless hypothetical. Maybe we should regulate financial textbook writers as they popularize models that create things like CDO's that were so prominent in our latest financial crisis? Perhaps he is diverting our attention from his crime of the century?

Paul then concludes:

> Buying stocks used to be about long-term value, doing your research and finding the company that you thought had good prospects. Maybe it had a product that you liked the look of, or perhaps a solid management team. Increasingly such real value is becoming irrelevant. The contest is now between the machines — and they’re playing games with real businesses and real people.

He is bringing up the perenial idea that investors

should

trade less, which I think is good practice. But earlier he suggested insiders make too much money off short term trades, implying higher trading costs. Isn't this then a disincentive to trade? So what should it be? When you propose two conflicting ideas why you are against something this reveals you aren't arguing on principle. And aren't

houses

the prototypical asset with high transaction costs and long investment horizons that should make them immune to bubbles? Remember, before there were maniacal machines making money in a competitive market, there was a a government-backed oligopoly or monopoly of trade execution.

Basically, people who do not understand a market where some participants are making a lot of money are often eager to call for regulation of that market because it seems obviously unfair. The solution, however, is invariably to merely entrench a status quo with a bigger shield against competition, but one where the profits can be shared equally by the exchanges, their member firms, and their regulators (through revolving door employment at the top ranks between exchanges, firms, and government). There was little 'change' on the exchanges prior to the 1990 computer revolution, and they robbed the public blind the whole time because they had a monopoly on order flow, all the while regaling their friends at the country club about their deft risk management skills and financial acumen ('the market was down and I still made money!').

Leave the market alone. It is very competitive, and if some electronic exchanges have different rules where people feel their orders are treated more fairly, volume will flock there (there are about 5 electronic exchanges). Competition is the best regulator ever invented. If you think someone making a tenth of a cent on your order is a big problem, you trade too much.