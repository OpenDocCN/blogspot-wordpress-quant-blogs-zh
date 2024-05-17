<!--yml
category: 未分类
date: 2024-05-18 05:35:16
-->

# Software Cost Curve and Context-Driven Testing (CDT) | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/03/16/software-cost-curve/#0001-01-01](https://mdavey.wordpress.com/2016/03/16/software-cost-curve/#0001-01-01)

## Software Cost Curve and Context-Driven Testing (CDT)

Cost of [defects](http://swreflections.blogspot.co.uk/2013/09/the-real-cost-of-change-in-software.html) isn’t something most teams worry about.  Most teams are primarily concerned with getting software built, accepting defects will be found in the testing cycle, and accepting defects will occur in production.  Unfortunately, this is a naive way of thinking about software in the 21st century.

[Examining the Agile Cost of Change Curve](http://www.agilemodeling.com/essays/costOfChange.htm) offer some thoughts on the subject.  Figure 3 is of particular interest.  Pay now or pay later for defects, later will cost more.  Unfortunately, most stake holders/product owner wants features, and only features, and don’t understand or care about software engineer, and the cost until its often to late 😦

Particularly telling on figure 3 is the cost of “Requirement defects found via traditional acceptance testing”.

Which brings us to the latest fad in software engineering (at least in the testing space), Context-Driven Testing ([CDT](http://context-driven-testing.com/)).

Rally has a posting on [CDT](http://www.developsense.com/blog/2016/01/a-context-driven-approach-to-automation-in-testing/) and [agile](https://www.rallydev.com/blog/engineering/context-driven-testing-agile-teams) teams which offers some interesting data points:

*   “Understanding what we’re testing is the cornerstone of quality for the end product.” – can’t disagree with that 🙂
*   “It’s a tester’s job to ask questions: why, what, where, how, what if, and so on. They need to ask questions at every stage but even more before coding starts, rather than later in the process” – I think this data point is particularly key.  I’m always concern of testers who only discuss testing in terms of their CV centric viewpoint/ego, ignoring the need to be part of a team, leveraging their testing skillset as part of a collaborative process to delivery quality software.  Hence “every stage” and “even more before coding starts” resinate well with my view of software engineering. 🙂
*   “business value” – nothing more needs to be said 🙂
*   “The purpose is not to find any defect, but the defects that matter” Agreed 🙂
*   “As a tester, it’s very easy to get sidetracked with defects in areas of the product that may not be as important.” – Unfortunately true, I call this “off-roading”

Which brings me to [CDT](http://context-driven-testing.com/), and the Seven Basic Principles:

*   “People, working together, are the most important part of any project’s context” – 100% agree.  That is why testers like other team members on a project need to collaborate as a team to deliver great software.  Get into the discovery discussion of a story, and stop accepted code, and thinking the game is to find defects.  Testing highlights often issues elsewhere in an agile team.  Look for root causes, and collaborate to fix the process before code is written and tested.
*   “Good software testing is a challenging intellectual process.” – this principle feels like testers are attempting to validate their intellectual capacity compared to developers. This shouldn’t be needed on a team were everyone is of equal value, and every is collaboration to delivery a software product that the team is proud of within the context of the business.

We can probably end with the Check != Test [discussions](http://www.satisfice.com/blog/archives/856) that have evolved over the last few years.  Thought needs to be given to the concept of checking and testing though-out the full lifecycle of a story (agile).  Otherwise defects will continue to climb.  Story discovery and elaboration that usually generate acceptance criteria discussion needs to also be consider in the context of CDT.  CDT can’t just be a silo at the end of the pipeline where tester site in the new CDT shiny world.

Final word, a lot of CDT [articles](http://www.satisfice.com/articles/cdt-automation.pdf) don’t touch on how CDT (Check != Test) work with kanban or scrum (agile) teams.

~ by mdavey on March 16, 2016.

Posted in [Agile](https://mdavey.wordpress.com/category/agile/), [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)