<!--yml
category: 未分类
date: 2024-05-18 05:27:43
-->

# Testing and Metrics | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2018/01/11/testing-and-metrics/#0001-01-01](https://mdavey.wordpress.com/2018/01/11/testing-and-metrics/#0001-01-01)

Executive Summary: testing provides confidence that requirements have been implemented (acceptance criteria/tests) prior to delivery into production, metrics provide a steer on confidence that the product/service/application is delivering as per the objectives, in production.

Writing code has become easier in recent years with the improvements in IDE’s, build and deploy chain tooling, GitHub and tutorials and samples available on the web. In many cases it is possible to find code lying around the web which may solves part of the problem you are attempting to code. That said, writing good code is an art. Code that is well structured, tested, and that delivers a solution to the problem statement is continues to be a high bar.

Testing is, and will continue to be, a debated topic, with multiple divergent approaches being common, for example:

*   Unit vs integration vs end to end
*   Code then test, Test Drive Development (TDD), Behaviour Driven Development (BDD), or other.

Any testing is better than no testing; and in most cases, an individual’s viewpoint on testing is strongly influenced by their notion of what makes a quality product, and how quality is measured. Improving upon a viewpoint, however well informed, requires articulated hypothesis and data points of validation found in collected [metrics](https://www.entrepreneur.com/article/237326).

AWS’s recent blog posting on the [roulette](http://www.businessinsider.com/amazon-web-services-uses-the-wheel-to-run-big-meetings-2017-12) wheel reminds us of how a data-driven culture is driving productivity and innovation at Amazon. Amazon has embraced metrics in defining objectives, and ensuring that products, services and processes meet expectation and can be optimised without reliance on “point of view”. Testing, backed by metrics, provides confidence that the delivered service will meet the expected criteria.

We can think of metrics and testing as providing a solid basis for confidence in application code as it progresses through the Software Development Life Cycle (SDLC), indeed, in the case of Amazon, Metrics Driven Development (MDD) are at the core of the SDLC. Metrics that validate the Definition of [Done](https://en.wikipedia.org/wiki/Scrum_(software_development)) (of a story), not only validate software during test but provide real-time data-driven evidence of performance to specification in production.

Returning to testing: software engineers who prefer not to follow the agile path of acceptance criteria/tests, as a required part of a story, risk failing to codify the story in a way that evidences how the requirement has been satisfied.

~ by mdavey on January 11, 2018.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)