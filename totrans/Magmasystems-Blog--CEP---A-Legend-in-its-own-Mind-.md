<!--yml
category: 未分类
date: 2024-05-18 04:57:54
-->

# Magmasystems Blog: CEP - A Legend in its own Mind?

> 来源：[http://magmasystems.blogspot.com/2008/10/cep-legend-in-its-own-mind.html#0001-01-01](http://magmasystems.blogspot.com/2008/10/cep-legend-in-its-own-mind.html#0001-01-01)

In the wake of the current financial crisis, several enterprising journalists have been trying to link the use of

CEP

, EDA, and

SOA

with the prevention of further financial woes. I have been sitting back and chuckling at many of these attempts to equate a three-letter acronym with financial salvation, especially ones written by people who don't actually work in finance and have never set foot on a trading floor. However, I cannot remain silent anymore.

I am reading an article that just appeared in

Wall Street & Technology

magazine titled

[Wall Street Firms Using CEP to Measure and Manage Risk](http://www.wallstreetandtech.com/feed/showArticle.jhtml?articleID=211300559&cid=RSSfeed_WST_All)

. Directly under the title of the article is the proclamation:

**New complex event processing applications promise to help firms get a better handle on their risk exposure, but can CEP erase Wall Street’s risk management woes?** 

This is an example of the sensationalistic headlines that have been crossing the various blogs and trade magazines in the past few weeks. All of a sudden,

CEP

has become a three-letter word for Financial Nirvana.

People .... I have news for you ....

CEP

systems are simple tools. They take streams of data and produce some output whenever something in the streams fit a certain condition. That's all it is!

CEP

systems do not do predictive analysis. They won't tell you when you will be losing money in the future.

They are like compilers. Saying that

CEP

can help with risk management is the same thing as saying a C++ compiler can help you with risk management. CEP products and C++ compiler are merely tools. You are supposed to be providing the logic and the interpretive abilities.

All banks have risk management systems, and most (if not all) have NOT been written using

CEP

products. Most of them are old, legacy systems written in C++. And, most of them do the same things that

CEP

products do. They take real-time streams of market data, positions, trades, and P&L, and they crunch them together to produce some useful output. And believe it or not, they work well despite the fact that they are not using commodity

CEP

technology!

And, many risk systems are run as an end-of-day processes. They are not real-time. They produce management reports which are read every morning. It is not the fault of the risk management system or the underlying technology if management chooses to ignore a risk report or chooses to put on an exotic trade whose risk can't be measured, or chooses to go all-in with

subprime

mortgages.

Risk management systems were here long before

CEP

became a buzzword and will remain long after all of the commodity

CEP

products have vanished.

I can imagine that, with the journalistic feeding frenzy associating

CEP

and risk management, smart marketeers like Terry Cunningham, Mark Palmer, and Don

DeLoach

are grinning from ear to ear. Not only grinning, but also doing their bit to fan the flames, as any smart entrepreneur would do.

Let's look at the article a bit.

But CEP vendors say their software can give risk managers a better view of such counterparty risk. "No software can replace [good] judgment," says Jeff Wooten, VP of [Aleri](http://www.aleri.com/). "What [CEP] software can do is give you better information with which to make those judgments and a better understanding of where you stand."

Ugh. Why could a system written with

Aleri

give you a

better

view of your risk than a custom-coded system? Will

Aleri

help you write more sophisticated detection rules?

Undoubtedly, Aleri will enable you to write a new risk management system much quicker than if you were to code one from scratch. But, I don't see that the CEP system will give you "better information". (To be fair, since Aleri has a real-time OLAP product, you might get better information by using the Aleri-specific visualization tool. Maybe that is what Jeff was implying.)

"Our software can't help you predict what's going to happen with your counterparty; it can't help you predict that Lehman will declare bankruptcy," Wooten adds. "But it can help you know what your exposure to Lehman is."

Knowing your exposure to Lehman is

conceptually

a very simple task that can be done without the help of a CEP system. However, what if your exposure is tied up in complex derivatives? How would a CEP system help you there? I am pretty sure that all of the people who lost money in Lehman bonds knew precisely what their exposure was, without the help of a CEP system.

"It's predictive; it's [based on] probability and in some cases the CEP engine will grab something it doesn't need," Greene acknowledges. "But when you look at more-complex instruments that can take weeks or months to settle because of issues on the back end, the CEP engine that can help them automatically grab information ahead of time behind the scenes speeds that up."Hmm

..... Can anyone decipher Spence's words for me? I think that Spence is kinda hinting about what I mentioned above, with the complexities involved in figuring out your P&L based on very complex structured products. But I would like to know exactly how Tibco Business Events assists in figuring out this exposure, and why it would be harder to do if you were to use some custom code or Excel.

Despite CEP vendors' promises, though, there are those who feel the value of CEP technology to risk management is finite, pointing to limitations of the technology itself and to the fact that risk management involves more than looking at numbers.

Bingo! And, directly after this statement, Tim Bass weighs in with some of his very correct opinions.

Another dissenting voice is Miles Kumaresan, head of quantitative trading at proprietary trading firm TransMarket Group. "The problem we have right now is the credit market, and that has nothing to do with complex risk models," he told WS&T in late September. "To do risk assessment you don't need CEP. It's much more important to actually use the risk numbers that are already available."

Double Bingo!

CEP

vendors sell a tool. This tool enables you to take various real-time streams of data, and allows you to correlate the various streams in various ways. They are very useful tools. But, if you have a working risk management system, you don't need to go out and start

rearchitecting

your systems right away. The current crisis is bigger than any risk management system. No risk management system would have stopped SAC and

Greenlight

Capital from losing billions of dollars on the

Volkswagon

short squeeze. There is a herd mentality on Wall Street, and

CEP

/

SOA

/EDA was not going to stop SAC from accumulating this particular short position.

Where would a

CEP

system be useful? I might use

CEP

if I would build a new risk system that aggregates output from other legacy risk systems in order to present an enterprise-wide view of risk. I would use

CEP

to build a brand new risk management system, but only if I could not find one from a vendor that fit my needs. (And, if I might allow myself to jump on a fashionable buzzword, I might eventually find risk management applications in "the cloud", maybe as a service offered in Microsoft Azure?)

CEP

,

SOA

, EDA are concepts and there are tools that implement these concepts. Don't ever mistake them for something that will give you immediate safety from all of the wolves out there.

©2008 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.