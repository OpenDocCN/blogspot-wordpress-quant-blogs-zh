<!--yml
category: 未分类
date: 2024-05-18 04:54:21
-->

# Magmasystems Blog: Microsoft CEP - Part 2

> 来源：[http://magmasystems.blogspot.com/2009/05/microsoft-cep-part-2.html#0001-01-01](http://magmasystems.blogspot.com/2009/05/microsoft-cep-part-2.html#0001-01-01)

Over the next few days, I hope to blog a bit about the new Microsoft

CEP

product, code-named "Orinoco".

To get yourself a bit more familiar with what was said at the announcement, you may want to go over to Richard

Seroter's

blog for a

[great post](http://seroter.wordpress.com/2009/05/12/teched-2009-day-2-session-notes-cep-first-look/)

that summarizes the session at

TechEd

in which the Microsoft

CEP

product was announced.

I first got wind of Orinoco in the Spring of 2008 during conversations with some members of the

SQL

Server group at Microsoft. The Orinoco group maintained radio silence until January of this year, when I got an invitation to come out to Redmond for a

Design

Review Session. I was joined there by several internal and external Microsoft customers, and we spent 2 days going over Orinoco from front to back.

I will blog a bit more about the technology of Orinoco in some future blog posts. But, I would like to say that Orinoco has the potential to radically change the

CEP

marketplace.

Orinoco will use

LINQ

as the "surface language". This builds upon the good work of people like Kevin Hoffman, whose

CLINQ

is used heavily at

Liquidnet

. The ability to embed

CEP

operations within a normal C# application is extremely powerful. You can take advantage of the power of the C# language and you can go back to using mechanisms like

inheritance

and generics in your

CEP

applications. This approach combines the expressive power of something like Streaming

SQL

with the flexibility of something like

Apama's MonitorScript

.

I don't think that Microsoft has defined their final marketing strategy around Orinoco (although Charles mentions that it will be part of SS 2008 R2) . When I met with the Orinoco team in April, they were still gathering feedback from potential customers as to how to market the CEP technology. But, I can imagine that for the immediate future, Orinoco will be free to users of SQL Server. I can also imagine that some part of Orinoco will be free to Visual Studio users (like

SQL

Server Express) and that an Enterprise version will be licensed like

SQL

Server. Perhaps a free developer version will come with

MSDN

? Perhaps it will be a free add-on to

SQL

Server in the same way that Reporting Services is free. This can be used to drive more

SQL

Server sales, and put a damper on competitive products like

Sybase

RAP. It can also be a compelling factor for developers to choose Windows instead of Linux for their

CEP

servers.

This means that every .Net developer will have access to

CEP

technology at a price point that will make it extremely attractive.

CEP

vendors like

CorAleri

,

Streambase

, and

Apama

will inevitably find themselves under a degree of pricing pressure. When the 2-ton gorilla bursts into the room with a free or low-cost offering, everyone has to sit up and take notice.

Orinoco is still a while away from being as polished as some of the commercial

CEP

products. But, the prospect of using

LINQ

, the integration with Microsoft

HPC

, and the ability to use Visual Studio as the

IDE

have gotten us pretty excited.

More later....

©2009 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.