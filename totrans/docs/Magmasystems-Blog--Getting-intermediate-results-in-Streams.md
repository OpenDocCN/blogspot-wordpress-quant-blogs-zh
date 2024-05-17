<!--yml
category: 未分类
date: 2024-05-18 05:05:47
-->

# Magmasystems Blog: Getting intermediate results in Streams

> 来源：[http://magmasystems.blogspot.com/2007/12/getting-intermediate-results-in-streams.html#0001-01-01](http://magmasystems.blogspot.com/2007/12/getting-intermediate-results-in-streams.html#0001-01-01)

Let's say that we want to keep a running total of the number of shares that we have traded, and at 4:00 PM every day, we want to dump out the total. In Coral8, we can do something like this:

CREATE LOCAL STREAM Totals (TotalShares INTEGER);INSERT INTO TotalsSELECT SUM(shares) FROM TradeInputStream KEEP EVERY 1 DAY OFFSET BY 16 HOURS OUTPUT EVERY 1 DAY OFFSET BY 16 HOURS;

This looks pretty straightforward. The Totals stream retains the totals until 4:00PM. At 4:00 every day, it outputs the total shares to any other stream that is "subscribed" to Totals, and then resets itself to start accumulating new totals.

This is something that

CEP

engines are good at, whether it be Coral8,

Aleri

, or

Esper

.

Now, let's enhance this a little bit.

Let's say we give the traders a .NET GUI application, and on this GUI is a "Status" button. The traders can press this button any time they want to know how many shares have been traded so far that day. So, at 2:00, a trader pushes a button on the GUI and we need to return to him the number of orders seen so far that day, the number of shares seen, the notional value of all orders, etc.

So, there are two questions:

1) How can we "dump out" these accumulators on demand? In other words, is there a way to tell these

CEP

engines to give me the contents of an aggregation stream AS OF THIS MOMENT ?

2) How can we "call into" our

CEP

engine to retrieve these values? Do the

CEP

engines support an

API

that I can use from within the GUI to say "Give me the current value of a certain variable in my module"? Something like

IntegerFieldValue field = Coral8Service.GetObject("ccl://localhost:6789/Default/SectorFlowAnalyzer", "sum(Shares)") as IntegerFieldValue; int shares = field.Value; 

In a standard C# application, this would be as simple as putting a Getter on a variable, and just calling the getter. If I was using Web Services, then I could call into a Web Service and just ask for the values of some variables or for some sort of object.

***But, from a C# app, how can I get the current value of a stream that is aggregating totals?***

Another way of accumulating the total number of shares in a

CEP

engine is to step into the procedural world, and just define a variable. In Coral8, it would be something like this:

CREATE VARIABLE TotalShares INTEGER = 0;ON TradeInputStreamSET TotalShares = TotalShares + TradeInputStream.shares;

Then, we would need a "pulse" to fire at 4:00PM every day, and upon this pulse firing, we could send the

TotalShares

to another stream.

I am sure that there are patterns in every CEP engine for accessing intermediate results, but something that is a no-brainer in a procedural language may not be so easy in a CEP vendor variant of SQL.

©2007 Marc Adler - All Rights Reserved