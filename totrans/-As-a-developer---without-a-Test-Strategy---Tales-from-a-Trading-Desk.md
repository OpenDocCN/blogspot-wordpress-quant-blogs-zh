<!--yml
category: 未分类
date: 2024-05-18 05:39:21
-->

# “As a developer…” without a Test Strategy | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/10/14/as-a-developer-without-a-test-strategy/#0001-01-01](https://mdavey.wordpress.com/2015/10/14/as-a-developer-without-a-test-strategy/#0001-01-01)

## “As a developer…” without a Test Strategy

Testing for me is critical on any project – obvious, but worth stating.  What I don’t get are the teams who are happy to code without tests, especially given the amount that has been written over the years about testing – TDD and BDD.  Personally, I’m pro-BBD.  BDD allows we to clarify how I want the software to work before I’ve written a line of code – anything else in my view is hacking.  We can all hack.  BDD forces the brain to clarify the behaviour of the application (and thus code), forcing a better design prior to any code being written, rather than an immediate refactor after the first x lines are written.

This leads to a number of issues which I don’t quite understand why people appear willing to accept on projects:

*   A lack of awareness of the testing [pyramid](http://martinfowler.com/bliki/TestPyramid.html)
*   No definition of done – green bar on tests etc
*   Lack of [integration](http://jamescrisp.org/2011/05/30/automated-testing-and-the-test-pyramid/) tests, and specifically validation of payloads
*   The believe that the performance framework should testing a different set of behaviours not tested anywhere else.  Shouldn’t the performance framework test differing frequencies of behaviours from the overall behaviours set that an application has been design to exhibit?
*   Acceptance of the [cupcake](https://www.thoughtworks.com/insights/blog/introducing-software-testing-cupcake-anti-pattern) anti-pattern
*   No care in the world of keeping the automated tests green that run in Continuous [Delivery](https://en.wikipedia.org/wiki/Continuous_delivery) process
*   The disconnect between Quality (Assurance) and Software Engineering which allows either duplication of tests, or more worryingly, the anti-pattern Split-Brain Testing Strategy – each party has a different view of behaviours that the application should adhere to.
*   Lack of any test results database to allow analysis

I’m not a fan of the Quality Assurance (QA) word.  My preference is Quality Engineering, simple because if quality doesn’t start in the software engineering codebase, then there is no hope of real quality.  The entire team has to embrace quality to make an application successful.

~ by mdavey on October 14, 2015.

Posted in [Agile](https://mdavey.wordpress.com/category/agile/)