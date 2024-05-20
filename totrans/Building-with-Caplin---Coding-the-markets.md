<!--yml
category: 未分类
date: 2024-05-12 19:41:56
-->

# Building with Caplin | Coding the markets

> 来源：[https://etrading.wordpress.com/2008/07/08/building-with-caplin/#0001-01-01](https://etrading.wordpress.com/2008/07/08/building-with-caplin/#0001-01-01)

## Building with Caplin

### July 8, 2008

So, let’s imagine you’re building a brand new single dealer channel for your bank with [Caplin Trader](http://www.caplin.com/caplintrader) from [Caplin Systems](http://www.caplin.com/about/). You picked Caplin because it’s the clear leader in the streaming [comet server](http://cometdaily.com/) space, and you want to deliver your etrading app into the browser so it’s zero install on the client desktop. There are other vendors with viable offerings that compete with Caplin’s [Liberator](http://www.freeliberator.com/documentation/) as comet servers – [Lightstreamer](http://www.lightstreamer.com/) is the clear number two. There are interesting new vendors entering the sector like [Kaazing](http://www.kaazing.com/), and there are [open source products](http://cometdproject.dojotoolkit.org/) too. But none of them is as mature or as widely deployed in live production etrading apps as Caplin Liberator.

A server to stream live ticking prices to a browser is just one part of the puzzle of building a web 2.0 etrading app. You need to build the GUI in the browser, and you need an execution system that will handle RFQ/RFS. Unlike the other vendors Caplin provide this in the shape of the Caplin Trader GUI and the Trading Data Source. The GUI is based on the JavaScript widget kit from [SoCentric](http://www.socentric.com/), and the Trading Data Source provides configurable state machines that keep GUI and server side state in lock step during the lifetime of an RFQ ticket.