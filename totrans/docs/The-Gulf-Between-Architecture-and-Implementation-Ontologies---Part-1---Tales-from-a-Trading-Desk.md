<!--yml
category: 未分类
date: 2024-05-18 05:51:18
-->

# The Gulf Between Architecture and Implementation Ontologies – Part 1 | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/04/15/the-gulf-between-architecture-and-implementation-ontologies-part-1/#0001-01-01](https://mdavey.wordpress.com/2014/04/15/the-gulf-between-architecture-and-implementation-ontologies-part-1/#0001-01-01)

Architecture and Design are terms often not heard enough within project teams – 😦 .  It almost feels like these words where left behinds in the Computer Science universities.  Two interesting books on the topic are:

What follows is a brief overview of the first book.  Another blog posting will cover the 2nd book.  Net out, I feel the Software Architecture in Practice book could have done more to embrace agile, and the concept of “done”

**Book: Software Architecture in Practice**

Page 4 start with a relevant definition:

> The software architecture of a system is the set of structures needed to reason about the system, which comprise software elements, relations among them, and properties of both.

Architecture structures can be divided into three categories: Modules, Component-and-Connector (C&C), Allocation Structures. (Page 10)

Reason for why architecture are important are offered on page 25.

Business Goals drive Quality Attributes and Architecture (page 50) leads to an interesting read on page 68 on the topic of specifying quality attributes in a common form.  In many ways this sounds like an opportunity for BDD, or at least the way to describe the architecture behaviour in Cucumber format to avoid the dreaded parse-translate issues that normally happens with requirements documents.

Anyone working in fiancé should be familiar with the system availability table on page 81.  Planning For Failure, page 82 reminds me of the Let It Die ………..

Defect Faults, page 87, offer the usual suspects, heartbeats, voting, monitoring.

Interoperability, Modifiability and Performance (Chapters 6-8) offer good reading.  Chapter 9, Security, is often overlooked, or thought about to late in the architecture.  Security requirements will often influence the architecture of an application in ways not anticipated at the start of a project.  One thing that is missing from “Further Reading”, page 157, is the Oracle Security Coding standards, given that a large majority of code these days in financial corporations is written in Java.  Further, I would also say Data Model security should also take account of any legal implications of where the data is allowed to be located.

Testability, chapter 10, states that for a well engineered system, “30-50% (or in some cases more)” of the cost goes into testing – page 374 offer a view of 30-90% of the development budget. Thankfully, page 16 offers details of NetiFlix’s monkeys.  However, chapter 10 doesn’t offer a view on leveraging the behaviour of the application as a source of truth for testing – BDD again.  Opportunity lost.  Page 170 does however offer some good insight into test data – which is often overlooked due to the complexity/pain of getting test data.  Page 171 also calls out automated testing – large systems can’t/shouldn’t be tested manually.

Architectural Tactics and Patterns (chapter 13) offers a catalog of usual suspects – MVC, Pipe-and-Filter, Client-Server, Peer-to-Peer, SOA, Pub-Sub.

Architecture in Agile Projects (chapter 15) offers an interesting read, which a set of six principles, Incremental  Commitment Model.

Chapter 16, Architecturally Significant Requirements (ASR) are possibly the closest thing to BDD.  Documenting Behaviour, page 351, again unfortunately missed the opportunity to mention BDD.

Moving from Architecture to implementation is always interesting (page 363).  How do you validate that the implementation is what was architected?  Frameworks and code templates are obvious contenders.  UML is the de facto architecture description language, but as discussed on page 369, there is still a gap between architecture and implementation.

Again, 19.2 (page 370) missed the opportunity to discuss BDD.  Further, if the architected application is to deliver a certain set of behaviours, then maybe the developers and testers should work from the same set of behaviour to ensure the application is tested appropriately.

Architecture Tradeoff Analysis Method (ATAM) (page 400) offers an interesting read, which proposed agenda and architecture presentation.  There is also a Lightweight Architecture Evaluation (page 415) that offers a reduction in time from 20-30 person-days to a single day – see agenda on page 416.

Competencies of Software Architecture comes in many forms.  Page 468 offers a dew duties that an organisation can perform to aid successful architecture.  My personal view is that architects need to still understand “code” else, we end up in world where architects are not respected by the implementation team.

~ by mdavey on April 15, 2014.

Posted in [Agile](https://mdavey.wordpress.com/category/agile/)