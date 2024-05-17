<!--yml
category: 未分类
date: 2024-05-18 06:24:30
-->

# FSM and Event Sourcing | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/05/28/fsm-and-event-sourcing/#0001-01-01](https://mdavey.wordpress.com/2013/05/28/fsm-and-event-sourcing/#0001-01-01)

## FSM and Event Sourcing

For some while I’ve been kicking around various Proof of Concepts (PoCs) that leverage Finite State Machines (FSM) and Event Sourcing to solve various financial problems.  It’s thus nice to read what other people are doing in a similar space.  Although old, Ruminations of a Programmer, has an interesting read on the use of Akka coupled with Event Sourcing and FSM.  What’s even better is that the [posting](http://debasishg.blogspot.co.uk/2012/01/event-sourcing-akka-fsms-and-functional.html) provides an example from a Trade perspective 🙂  Debasish has a [presentation](http://phillyemergingtech.com/2012/system/presentations/debasish_ghosh-phillyete-12.pdf) from the Emerging Technologies For The Enterprise [conference](http://phillyemergingtech.com/2012/sessions/building-applications-with-functional-domain-models-event-sourcing-and-actors) that provides further reading.

CQRS as a tenet of Even Sourcing, coupled with FSM, provides an interesting solution to the problem of  globally distributed events.  Leveraging the [command-model](http://martinfowler.com/bliki/CQRS.html) (FSM) coupled with the query-model (Event [Source](http://martinfowler.com/eaaDev/EventSourcing.html)) allows the [building](http://architects.dzone.com/news/asynchronous-event-sourcing) of reliable distributed systems at a worldwide scale where state at certain [points](http://www.allthingsdistributed.com/2008/12/eventually_consistent.html) are relevant, and needed, but that asynchronous communication is acceptable if achieved over a reliable transport.

~ by mdavey on May 28, 2013.

Posted in [Cloud](https://mdavey.wordpress.com/category/hpc/cloud/)
Tags: [EventSourcing](https://mdavey.wordpress.com/tag/eventsourcing/), [FSM](https://mdavey.wordpress.com/tag/fsm/)