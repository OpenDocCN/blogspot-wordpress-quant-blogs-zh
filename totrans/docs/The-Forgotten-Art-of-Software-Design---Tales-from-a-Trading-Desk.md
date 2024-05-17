<!--yml
category: 未分类
date: 2024-05-18 06:28:16
-->

# The Forgotten Art of Software Design | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/04/06/the-forgotten-art-of-software-design/#0001-01-01](https://mdavey.wordpress.com/2013/04/06/the-forgotten-art-of-software-design/#0001-01-01)

I think Katelyn touches on an important [point](http://katgleason.tumblr.com/post/47257463324/talk-about-the-problem-not-the-solution) in “Talk about the problem not the solution”.  I’d also say that a “solution” designed before understanding the “problem” also implicitly mean that the solution fails on the “smell test” from a general software architecture and design validation.  Development has  designed a solution without considering the “problem” and hence the business requirements of the “problem” have been missed, which is the grant scheme of things means “refactoring”, modification request, and more than likely a buggy code base due to the churn.

Taking this a step further, from an agile perspective, the agile story may often begin to take on a “technical” bias due to the solution before the problem, with a lack of acceptance criteria/tests, which continues to lead to a solution development want to implement that isn’t actually fully solving the problem. Bad smell!

This problem/solution is partly driven in some quarters through the believe that the latest framework/library is the thing that needs to be part of the solution.  Which nicely brings me to [Making Software](http://www.amazon.co.uk/Making-Software-Really-Works-Believe/dp/0596808321).  So much of development is based on claims that are not verifiable.  Read chapter 12 on TDD – I’m not saying I’m anti TDD, but just using TDD as an example.  Chapter 25, “Where do most software flaws come from?” offers the following view:

> Problems with requirements, design, and coding accounted for 34% of the total (modification requests) MRs. Requirements account for about 5% of the total MRs and, although not extremely numerous, are particularly important because they have been found so late in the development process, a period during which they are particularly expensive to fix

Which to Katelyn point, that failure to understand the problem, will clearly result in future rework of the solution.

One of the many issues I believe agile team fail to understand about agile is that agile doesn’t stop software architecture and design from happening, it merely attempt to avoid the issue of big up-front architecture and design happen at the start when there are lots of unknowns.

Which brings me round the circle and back to the start of this posting.  Before an agile story goes into development, the story needs to capture the problem clearly, and concisely with acceptance criteria/tests, though User Experience (UX) assets, the team needs to have architecture/designed a solution to solve the business problem, and not a solution looking for a problem.

~ by mdavey on April 6, 2013.

Posted in [Agile](https://mdavey.wordpress.com/category/agile/)