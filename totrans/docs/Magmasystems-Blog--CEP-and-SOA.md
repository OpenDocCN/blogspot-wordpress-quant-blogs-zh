<!--yml
category: 未分类
date: 2024-05-18 05:04:41
-->

# Magmasystems Blog: CEP and SOA

> 来源：[http://magmasystems.blogspot.com/2008/01/cep-and-soa.html#0001-01-01](http://magmasystems.blogspot.com/2008/01/cep-and-soa.html#0001-01-01)

There has been a lot of activity in the

CEP

blogs about the uses of that mythical beast, the Service Oriented Architecture (

SOA

). This beast means different things to different people. From my standpoint, let me tell you what it means to me, and let me tell you what I need.

For my company, the possible adoption of

CEP

will mean a huge seed-change in the way that we develop applications and share information. Right now, we have the most important information in the trading and risk process going directly into huge, monolithic

Gui's

. Important order and risk information is being sucked into a GUI application, much like a

vacuum

cleaner sucks up a trail of dust.

Already, the

CEP

effort has been able to transform the order-monitoring GUI into an Order Service, publishing order information to subscribers over a message bus. If the

CEP

project is a total bust, then at least the one tangible is the liberation of order flow information.

As all of the

important

data --- orders, risk, positions --- gets published out by the source systems and gets consumed by other applications, we need to have a global

*catalog*

that developers can browse where they can find out how to access data and what operations can be performed on the data.

For example, if I needed to get a real-time flow of Greeks for certain vanilla US equity derivatives, I might use the catalog to ask a question like this:

"Where can I find real time flows of

greeks

for IBM,

INTC

,

MSFT

, and DELL options? I prefer to have this flow come through as XML, but if no XML is available, then give the data to me in any format. In addition, I need to know if you have a remote function that I can call that calculates theta on a certain security."

The catalog service might respond:

"You can get the US Equity

Deriv

Greek flows by subscribing to a

Tibco

EMS message bus. You need to subscribe to the

Tibco

broker at

*tcp://megacorpbroker:7001*

, using functional ID "foo" and password "

baz

". This service is publishing out each

greek

as a

JMS MessageMap on the EMS topic *equities.derivatives.greeks.us*

, and here is a list of properties that you can access in each message. Sorry, but we don't support XML.

Furthermore, here are a list of request/response operations that the Greeks Web Service supports. If you want to generate the proxy code to use these operations, the URL of the

WSDL

for the Greeks Web Service is at

[*http://greekserver:8042/webservice.wsdl*](http://greekserver:8042/webservice.wsdl)

.

As an added bonus, if you send this XML string as a

JMS TextMessage

in the following format to this the EMS queue named

*equities.derivatives.greeks.services*

, then you will get a response on your private EMS temporary queue."

This is like a super-charged UDDI, but knows about things like message buses and JMS queues and topics. For me, this is what we need out of SOA. Everyone publishing and consuming real-time flows. Everyone making services available, both as Web Services and as request/responses over a message bus.

The catalog should be real-time itself. In other words, if a new flow or a new service becomes available, the catalog itself should notify listeners that something has changed. So, all applications might subscribe to a "catalog control" topic where real-time changes to the catalog services are broadcast.

Imagine now that we have a GUI in which users can pick and choose from various flows, dynamically create queries that will be registered with the CEP engine, and dynamically define derived events that will be created when the queries detect a situation. Most of the CEP engines support an API which makes this possible.

***Should we write this SOA catalog ourselves? Can you recommend a product that already does this?***

©2007 Marc Adler - All Rights Reserved