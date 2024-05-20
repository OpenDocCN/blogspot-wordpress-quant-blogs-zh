<!--yml
category: 未分类
date: 2024-05-18 06:03:20
-->

# The Design of a Team | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/08/07/agile-the-design-of-a-team/#0001-01-01](https://mdavey.wordpress.com/2013/08/07/agile-the-design-of-a-team/#0001-01-01)

Bit of a random walk, based on speaking, reading and dealing with numerous team learnings over a duration of time.

David [Hanna](http://dave-hanna.net/) provides a awesome quote that is worth re-reading to make sure you fully understand it:

> **All organizations are perfectly designed to get the results they get.**

Team bashing to deliver results may not be the solution, although its unfortunately often the “management” style used when the results are not what the organization wants.  Now think about the quote above.  Maybe the organization has constructed the team, such that the team has essentially been set up to fail?

This lead to Paul [Drucker](http://en.wikipedia.org/wiki/Peter_Drucker) when considering “management”. Mr Drucker provide 5 basis [tasks](http://guides.wsj.com/management/developing-a-leadership-style/what-do-managers-do/) of a manager.  Success provide a good [view](http://www.success.com/articles/1115-peter-drucker-the-father-of-management-theory) on Mr Drucker’s management theory, likewise [BusinessWeek](http://www.businessweek.com/stories/2005-11-27/the-man-who-invented-management).  A few classic [comments](http://sourcesofinsight.com/lessons-learned-from-peter-drucker/) from Mr Drucker:

*   Most of what we call management consists of making it difficult for people to get their work done.
*   The most important thing in communication is hearing what isn’t said
*   The productivity of work is not the responsibility of the worker but of the manager.

More recently Chris [Parsons](http://chrismdp.com/) offered an insightful [talk](http://chrismdp.com/2013/05/leading-software-teams-well/) at the Scottish Ruby conference earlier this year, “[Leading](http://vimeo.com/66884238) Software [Teams](http://chrismdp.com/tag/team/) Well”.  The session is well worth listening to, specifically because it re-iterates some age old points, which are unfortunately often still lost today due to bad leadership and management.  A few key points:

*   Management structure often gets in the way
*   [Leadership](http://en.wikipedia.org/wiki/Good_to_Great) is NOT management.  Management as per an assembly line is legacy in software engineering – you can’t control people!
*   Task [delegation](http://chrismdp.com/2012/09/task-assignment-is-a-team-anti-pattern/) 😦 An agile anti pattern if ever there was one.
*   Job titles – I’ve always found job [titles](http://chrismdp.com/2012/09/job-titles-team-anti-pattern/) to generate the silo mentality on [teams](http://chrismdp.com/2011/04/the-team-is-the-atomic-unit/), generating Microsoft Excel resource movements 😦  Trial before hire is definitely the best approach is possible – compromised hires will cost you and your company serious money
*   Stop the finger [pointing](http://chrismdp.com/2011/04/the-team-is-the-atomic-unit/) within a team!
*   Raise your replacement!

This leads me to BDD, and the issue I have with CV’s that says they follow BDD, but actually a person just followings general “testing”.  This is better clarified by surfing over to the Agile Alliance web site, and the [BDD](http://guide.agilealliance.org/guide/bdd.html) page, which in my view provide some very well written points on “Sign of use”.  Specifically, think about the implications of following compared to you usage of “testing” today, and the possible breakage from story (with acceptance criteria/tests) to code:

*   A team using [BDD](http://www.manning.com/smart/) should be able to provide a significant portion of “functional documentation” in the form of User Stories augmented with executable scenarios or examples
*   Rather than refer to “the unit tests of a class”, a practitioner or a team using BDD prefers to speak of “the specifications of the behavior of the class”. This reflects a greater focus on the documentary role of such specifications: their names are expected to be more expressive, and, when completed with their description in given-when-then format, to serve as technical documentation.

Which brings up another anti-pattern – Cucumber is a testing tool.  If your of this view, then consider having a [read](http://chrismdp.com/2013/06/rack-usermanual/) of this [posting](http://chrismdp.com/2012/09/cucumber-isnt-a-testing-tool/).  Dan North provides further BDD samples [here](http://dannorth.net/whats-in-a-story/), specifically around story’s being “the result of [conversations](http://chrismdp.com/2012/09/cucumber-isnt-a-testing-tool/) between the project stakeholders, business analysts, testers and developers”.  For me, a well written story with acceptance tests (AT) which generates code and “tests” that don’t leverage the work put into Given-When-Then AT’s seems like a broken pipeline – even more so if the AT’s are leveraging a DSL when written prior to coding.

~ by mdavey on August 7, 2013.

Posted in [Agile](https://mdavey.wordpress.com/category/agile/)