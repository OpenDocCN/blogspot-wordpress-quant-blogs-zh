<!--yml
category: 未分类
date: 2024-05-18 05:43:36
-->

# Event-Driven Architecture Pattern Topologies | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/03/02/event-driven-architecture-pattern-topologies/#0001-01-01](https://mdavey.wordpress.com/2015/03/02/event-driven-architecture-pattern-topologies/#0001-01-01)

## Event-Driven Architecture Pattern Topologies

O’Reilly Radar has an interesting article on event-driven [architecture](http://radar.oreilly.com/2015/02/variations-in-event-driven-architecture.html), “Variations in event-driven architecture”.  Mark Richard’s eBook is available [here](https://mdavey.wordpress.com/2015/02/19/user-story-map/ "User Story Map") if you want the full read.

Its probably worth pointing out that I’ve come across a number of people worried about the number of event queues when using the Mediator topology – a strange thought process in my view unless the architect is proposing to use a single queue for all event types 😦

> It is common to have anywhere from a  dozen to several hundred event queues in an event-driven architecture

Its also worrying that a lot of people forget about the Open Source available integration hubs, and instead just straight into coding their own variant – lack of ROI

> The simplest and most common implementation of the event mediator is through open source integration hubs such as Spring Integration, Apache Camel, or Mule ESB.

Its nice to see reference to Space-Based architectures in Mark’s eBook.  Its surprising how many people look at me blankly when I mention Space-Based architectures 😦

~ by mdavey on March 2, 2015.

Posted in [Trading](https://mdavey.wordpress.com/category/trading/)