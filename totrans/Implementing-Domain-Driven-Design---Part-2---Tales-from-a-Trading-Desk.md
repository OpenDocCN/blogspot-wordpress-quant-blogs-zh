<!--yml
category: 未分类
date: 2024-05-18 05:46:07
-->

# Implementing Domain-Driven Design – Part 2 | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/09/30/implementing-domain-driven-design-part-2/#0001-01-01](https://mdavey.wordpress.com/2014/09/30/implementing-domain-driven-design-part-2/#0001-01-01)

Continuing with [Vaughn’s](http://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577) book, page 22 table 1.4 offer a nice view of writing code that models the business – physical and conceptual domains.  Page 25 hits the nail on the head with reference to software engineers not being able to pursue technologies and techniques just because they sound cool – well said Mr [Vernon](http://www.informit.com/articles/article.aspx?p=1944876&seqNum=2)!

Page 33 touches on the issues of data-centric models, compared to business domain behaviours.  All to often we see in code bases that the data payloads have become some warped domain model within the code base, leaking though every layer possible.

I feel page 37 should have referenced two three letter acronyms, BDD and TDD.  However, at least early on in the book reference to test-first development was made 🙂

Back to page 26, and selling DDD to your boss.  If you in software development, and your boss doesn’t know about DDD, then you have bigger problems that just selling DDD.

Page 113, over use of architecture patterns speaks to the ivory tower that one often find with architects. I’ve been in too many banks where the ivory tower enterprise architects perceive they know best, yet have become disconnected from the business, and usage of architecture patterns within real-applications. Further, using architecture to mitigate the risk of failure provides an ROI that offers true value, rather than an anti ROI value based on architecture alone – justification of architecture married to the function requirements! Page 144 harps back to my view of the sweet shop – using architectural styles and patterns because they are cool tools 😦

Layer’d architecture (page 119) reminds me of how often I worryingly see applications where basic architecture has been forgotten, leading to leakage throughout the application. This in itself leads to tighter coupling, which will inevitable cause problems in the future.

Event sourcing, page 160, is an appropriate read, aggregate state snapshots 🙂

Type of tests – page 239\. Unit tests and behavioural tests both have their place. Embrace change.

“Design you data model for the sake of your domain model, not your domain model for the sake of the data model” – page 250

Modelling events (page 288) and publishing events (page 296) offers an appropriate read, coupled with one of my favourite diagrams for modelling interactions – the sequence diagram (page 299). Think distributed systems. Be thoughtful of timestamps on events – clock slippage.

“Problems always arise with integration when developers who are unfamiliar with the principles of distributed system gloss over its inherent complexity” – classic statement (page 451). Reminds me of all the software engineers who have told me they can write thread safe code, and yet fail to understand the complexity of cores, latency and more

Appendix A offer a good read on event sourcing, with an appropriate 🙂 selection on testing and specification – Given-When-Expect

~ by mdavey on September 30, 2014.

Posted in [Agile](https://mdavey.wordpress.com/category/agile/)
Tags: [DDD](https://mdavey.wordpress.com/tag/ddd/)