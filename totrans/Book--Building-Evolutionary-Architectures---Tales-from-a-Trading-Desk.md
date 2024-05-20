<!--yml
category: 未分类
date: 2024-05-18 05:27:09
-->

# Book: Building Evolutionary Architectures | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2018/05/28/book-building-evolutionary-architectures/#0001-01-01](https://mdavey.wordpress.com/2018/05/28/book-building-evolutionary-architectures/#0001-01-01)

## Book: Building Evolutionary Architectures

Had this [book](https://www.thoughtworks.com/books/building-evolutionary-architectures) for some time, just took a while to write up my notes 🙂

*   Page 7, Fitness Functions – objective function used to summarise how close a prospective design solution is to achieving the set aims
*   Page 12, structure of teams around service boundaries.
*   Page 35, QA in Production.  I’ve used this over the last n years, to great effect 🙂
*   Page 36, Chaos Monkey, Simian Army, and [Conformity Monkey](https://github.com/Netflix/SimianArmy/wiki/Conformity-Home).  Design with Chaos Monkey in mind to ensure architectures have resilience built in from day 1 🙂  Conformity Monkey checks services to ensure they follow architect-defined best practices.
*   Hypothesis [driven](https://medium.theuxblog.com/hypotheses-driven-ux-design-c75fbf3ce7cc) UX design
*   Page 48, Domain-Driven Design.  Forget the unified class across all services concept.  Allow each service to define their own, and reconcile differences at integration points (bounded context)
*   Page 96, Use Deployment Pipelines to Automate Fitness Functions.  Cycle Time is the measure of engineering efficiency.
*   Page 98, the biggest single common impediment to building evolutionary architecture is intractable operations.
*   Page 128, Anti-pattern – Code Reuse Abuse
*   Page 131, Pitfall – Resume-Driven Development.  We’ll all seen this one
*   Page 133, Forced [Decoupling](https://www.infoq.com/news/2014/11/gotober-wunderlist-microservices)
*   Page 133, Goldilocks Governance model – pick three technology stacks for standardisation: Simple, intermediate and complex.
*   Page 144, Product over project 🙂  Like this concept a lot 🙂
*   Page 154, Testing.  Obvious, but constantly needs to be re-iterated 😦

Great book.  Sensible length.  Easy to consume 🙂

~ by mdavey on May 28, 2018.

Posted in [Agile](https://mdavey.wordpress.com/category/agile/), [Languages](https://mdavey.wordpress.com/category/languages/)