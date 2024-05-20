<!--yml
category: 未分类
date: 2024-05-18 05:04:53
-->

# Magmasystems Blog: Aleri Evaluation

> 来源：[http://magmasystems.blogspot.com/2007/12/aleri-evaluation.html#0001-01-01](http://magmasystems.blogspot.com/2007/12/aleri-evaluation.html#0001-01-01)

Just a small word about the

Aleri

evaluation. Several of you have repeatedly pinged me to find out what I thought of

Aleri

, so I am going to write down some of my impressions. The usual disclaimers apply, such as this is my opinion and does not necessarily represent the opinions of my employer.

My impressions were formed after a superficial evaluation of

Aleri

against some of the other vendors. I have not gotten to the point yet where I am testing the latency and throughput of the

CEP

engines. I have not soaked and stressed the

CEP

engines to see if any of them are leaking memory. I have not tried them on a variety of processors, and I have not examined their performance under

multicore

processors.

In a nutshell, my biggest area of concern with

Aleri

was the "spit-and-polish" of the product. They very well might have the fastest

CEP

engine out there. However, I was stymied by the quality of the documentation, and my perceptions of their

Aleri

Studio. It also seemed that they were more of a "system integrator" that some of the other

CEP

firms, taking separate products like

OpenAdaptor

and

JPivot

and trying to fit them into a holistic offering.

An example of this was reflected in the difficult time I had in getting

Aleri

integrated with

SQL

Server 2005 through Open Adaptor. The documentation was non-obvious, and it took many hours with their sales engineer to finally get it connected. I compare this to

Streambase

and Coral8, where it took all of 5 minutes to hook up an

SQL

Server 2005 database to their systems (disclaimer: there is a problem getting

Streambase

, Vista and

SQL

Server to work together, although

Streambase

has not yet released an official version for Vista).

That being said, the salient points are:

1)

Aleri's

management team (Don

DeLoach

and Jeff

Wootton

) fully realize their short-comings in the department of

aesthetics

, and have promised me that they are actively addressing it. I would highly recommend that

Aleri

look at

Streambase

, whose total package is good with regards to documentation and tutorials. (However, I still find a lot of pockets of

geekiness

in the

Streambase

documentation.)

2) The

Aleri

sales engineering team, led by Dave, got a variant of my initial use case to work. However, there are features that

Aleri

does not yet have, such as jumping windows and pattern matching, that make Coral8 and

Streambase

stand out.

3) Going through Open Adaptor is not fun.

Streambase

and Coral8 make it simple to write adapters in C#. The

Aleri

sales engineer told me that he usually has to help clients to get adapters to work. That is really not the message that a company wants to hear if they have many legacy systems to interface with.

4)

Aleri

has real-time

OLAP

, using

JPivot

. To my knowledge, they are the only

CEP

company to offer real-time

OLAP

. I did not really get to see this feature, but

***true***

real-time

OLAP

is something that a lot of financial companies are interested in. We want to be able to slice and dice our order flow in real time over different dimensions.

5) The

Aleri

Studio uses Eclipse, just like

Streambase

, and the icons even look exactly like

Streambase's

icons. However, the user interaction seemed a bit shaky at times, and there were moments when I got myself into "trouble" with the

Aleri

Studio by clicking on one thing before clicking on another thing. Again,

Streambase

seems more solid. And, Coral8 does not try to impose a GUI builder on the developer. The guys at

Aleri

told me that they are addressing these issues.

I was really pulling for

Aleri

, since the development center is about 15 minutes from my house in New Jersey. They are right down the block from the hallowed halls of Bell Labs in Mountainside, and some of the developers live in the next town over from me. You couldn't meet a company of nicer guys, and the CEO is a very low-key guy compared to other

CEOs

that I have met. I was impressed by the fact that, at the

Gartner

conference on

CEP

, he stood up in front of the audience and

exhorted

us to try different

CEP

products.

I anxiously look forward to the 3.0 version of

Aleri's

offerings, and to see tighter, easier integration between their various components, enhanced documentation, enhanced support for .NET, and a cleaner version of their

Aleri

Studio. Given the quality of the developers there, I am sure that this version will kick some butt.

©2007 Marc Adler - All Rights Reserved