<!--yml
category: 未分类
date: 2024-05-18 05:35:58
-->

# Check != Test. Discovery != Testing – Delivering Quality Software | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/03/10/check-test-discovery-testing-delivering-quality-software/#0001-01-01](https://mdavey.wordpress.com/2016/03/10/check-test-discovery-testing-delivering-quality-software/#0001-01-01)

For some while there’s be discussion in the quality space of software engineering around [checking](http://devblog.songkick.com/2016/02/15/move-fast-but-test-the-code/) and [testing](http://www.satisfice.com/articles/cdt-automation.pdf).  Many of these discussion provide a sensible step forwards in thinking and process.  What is clear is that label’s come with baggage – especially in the context of “testing” and “automation” – an ambiguous word these days in the software engineering community.

If we start at the beginning of the process of software development, we essentially have “discovery”, and the capture of requirements – how the feature/story will behave when implemented.  In many ways the capture of these requirements in BDD syntax offers at least a machine readable format that hopefully reduces ambiguity, and cuts out a degree of the issues of parse/translate from the n page requirements document.

“Checking” (or old school “validation”) is an acceptable label for ensuring that once the code is deemed “Done”, that the code has implemented the expected behaviour, and passed the acceptance criteria that came out of the the discovery (requirements) phase for the story.  Anyone with a Kanban board might want to go with “In Checking” rather than “In Test” 🙂

“Test Automation” (although very ambiguous) is really the reduction of manual “checking” by using code to perform the activity in a more efficient manor.

This leads us to “testing”.  One [view](http://devblog.songkick.com/2016/02/15/move-fast-but-test-the-code/) of testing is the following:

> Testing involves exploring the system in creative ways in order to discover the things that you forgot about

In many ways, “testing” as defined above, is really a continuation of “discovery”.

“Discovery” is about understanding an agile feature/story, getting into the detail so that the story can be implemented in code based on the requirements, with an agreed way to check that the requirements have actually been implemented (acceptance criteria).

“Testing” feels based on the definition above to be an extension of discovery, which is going to be confusing if we now have two words to define how to discovery the required behaviour of a story.  Unless a huge amount of time and effort in spent in the initial discovery of a stories requirements, not all the behaviour and acceptance criteria will be captured – its unfortunately life.

In summary, I don’t like ambiguous labels.  Further, overloading label that have been around a long time, is in my view dangerous unless you have a way of reminding everyone of the new label definition.  My suggestion is that to improve quality of software, we spend a little more time “engaging” in discovery, “check” the story once “done”, and then use the implemented feature to “discovery” is we’ve missed any edge cases, that will allow us to refine the acceptance criteria, and improve our automation checks.

~ by mdavey on March 10, 2016.

Posted in [Agile](https://mdavey.wordpress.com/category/agile/)