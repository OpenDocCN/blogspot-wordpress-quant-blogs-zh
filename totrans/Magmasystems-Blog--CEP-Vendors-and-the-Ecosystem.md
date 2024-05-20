<!--yml
category: 未分类
date: 2024-05-18 05:05:05
-->

# Magmasystems Blog: CEP Vendors and the Ecosystem

> 来源：[http://magmasystems.blogspot.com/2007/12/cep-vendors-and-ecosystem.html#0001-01-01](http://magmasystems.blogspot.com/2007/12/cep-vendors-and-ecosystem.html#0001-01-01)

While my wife and son cavort around Australia and New Zealand for the next few weeks (I get to stay home and watch my daughter, who only has one week off from high school), I hope to be able to catch up on some of the blog posts that I owe people.

One of the things that is most important for me in choosing a

CEP

vendor is the ecosystem that surrounds the

CEP

engine. In a company such as mine, we need to interface with many different legacy systems. These legacy systems can hold crucial data, such as historical orders, customer trades, market data, volatility curves, customer and security reference data, etc. This data may reside statically in a database, be published out as flow over some kind of

middleware

, or interfaced with an object cache or data fabric. We have every color and shape of database technology in our firm, whether it be more traditional relational databases like Oracle,

SQL

Server, and

Sybase

, or newer tick databases like

KDB

+.

From the input and output points of the

CEP

engine, we need seamless integration with all sorts of systems. Most

CEP

engines have the concept of in-process and out-of-process adapters. In-process adapters are more

performant

that out-of-process adapters. We would love to see as many in-process adapters delivered out-of-the-box by our

CEP

vendor. We do not want to spend time writing our own in-process adapters.

So far, none of the

CEP

vendors support

KDB

+ as an out-of-the-box solution. In fact, many of the

CEP

vendors did not even know what

KDB

+ was. (Is the same true for

Vhayu

as well?) My feeling is that, if a

CEP

vendor is going to be successful on Wall Street, then they must support

KDB

+. Is it even feasible for the

CEP

vendors to provide an abstraction layer around

KDB

+, and let the

CEP

developer write all queries in

SQL

instead of writing them in K or Q?

One of the most important things that I would like to see from the

CEP

vendors are tools to enable the analysis of all of the data that pass through the

CEP

engine. Many groups might not have the budget to hire a specialized mathematician or

quant

to perform time-series analysis on the data. Learning specialized languages like R or

SPlus

might not be possible for smaller groups that do not have a mathematical bent. The same goes for packages like

Mathematica

and

Matlab

.

Would it be worth it for the

CEP

vendors to come out with a

pre

-packaged "stack" for various financial verticals that incorporates analysis tools? Or, would writing a detailed cookbook be better? And, where does the responsibility of the

CEP

vendor end? Should we expect the

CEP

vendor to provide a one-stop shop for all of our needs, or should be just expect the

CEP

vendors to provide strong integration points?

Better yet, does this open up an opportunity for a third party company to provide this service? Like the many laptop vendors who buy a motherboard (the

CEP

engine), and slap together a disk drive, CD drive, screen and keyboard to make a complete system?

In examining the various

CEP

vendors, I have come to the conclusion that the offerings from

Streambase

, Coral8 and

Aleri

are very similar. Given another year, I might expect each vendor to fill in the gaps with regards to their competitors' offerings, and at that point, we might have practically

identical

technologies from 3 different vendors.

***In my opinion, the real win for these CEP vendors will come in the analysis tools they provide.***

©2007 Marc Adler - All Rights Reserved