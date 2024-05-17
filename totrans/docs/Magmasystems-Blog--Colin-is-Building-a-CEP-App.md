<!--yml
category: 未分类
date: 2024-05-18 04:58:46
-->

# Magmasystems Blog: Colin is Building a CEP App

> 来源：[http://magmasystems.blogspot.com/2008/09/colin-is-building-cep-app.html#0001-01-01](http://magmasystems.blogspot.com/2008/09/colin-is-building-cep-app.html#0001-01-01)

Colin Clark, is starting to blog about OMICRON 5000, a

CEP

-based order router/liquidity finder that he wants to build. I am not sure if Colin is going to just sketch the system out on his blog, or if he is

going

to get down and dirty and start coding this thing. But, I will follow his upcoming exploits very closely, as Colin implies that he will keep us informed during every step of the development process.

I don't know what technology platform Colin is going to choose ... Windows or Linux, C# or C++ or Java. If Colin is very public about this new effort, then I might expect some vendors to throw him some complimentary software, as it would be a tremendous marketing coup for the

CEP

vendor who eventually is chosen.

Colin's evaluation will take place a year after we did our initial evaluation, and I am interested to see how he ends up choosing the

CEP

engine. Colin is a company of one. *IF* Colin can get his hands on some

CEP

software, he will not have the same luxury that we did --- 4 months devoted to research --- to make a prolonged evaluation.

Let's see what a company of one can do to get bootstrapped into the world of

CEP

.

How will Colin get his hands on the

CEP

software to evaluate? Coral8 is free to download, and it is very easy to get started with their developer version. You can download

Aleri

, but from what I remember, it comes with a 30-day license. Progress

Apama

would not let me download their software without requiring a dog-and-pony show.

Streambase

gave us their software, so I don't know anything about their evaluation process.

Esper

is totally free (at least, their non-HA version is). I wonder if Paul Vincent will throw Colin a copy of Business Events to play with.

Once Colin chooses a

CEP

engine, how much will he have to spend to get a production license for the software?

Esper

is free. The others require a minimum outlay of $60,000, not including yearly maintenance fees. You can play with your downloaded version of Coral8 all you want, but you cannot deploy it into a production app without purchasing a license.

Colin says that OMICRON needs a database. I assume that MySQL is still free, even after the Sun purchase. You need to find a

CEP

engine that has MySQL adapters.

OMICRON needs a FIX engine. The only free one that I know of is

QuickFix

. Will Colin build an in-process or out-of-process FIX adapter for his

CEP

engine?

OMICRON needs market data.

OpenTick

is free to use, and all you need to do is pay the exchange fees. Worse comes to worse, you can write a service that scrapes Yahoo Finance, but I am sure that will not satisfy Colin (although it is useful for early-stage development).

Finally, Colin needs a GUI. If Colin uses C#/.NET, there are plenty of controls that come with Visual Studio, and there are tons of others that you can find on sites like

CodeProject

. I am assuming that all OMICRON needs is a simple grid, with perhaps some real-time updating of the cells.

It seems that a single developer can get away with totally free, Open Source software if he was going to choose Esper. There might be CEP engines systems from universities that you can use.

I will eagerly follow Colin's blog and kibbitz on his every move....

©2008 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.