<!--yml
category: 未分类
date: 2024-05-18 06:32:33
-->

# Moving from Stories to Code | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2012/12/04/moving-from-stories-to-code/#0001-01-01](https://mdavey.wordpress.com/2012/12/04/moving-from-stories-to-code/#0001-01-01)

## Moving from Stories to Code

Over the years I’ve worked with numerous projects/teams which follow the agile path.  The usual problem occurs with a degree of projects; the team is newly formed, and there are a lot of differing views on what “agile” really means in a day to day project activity.  Ignoring the general agile coaching that occurs on these types of projects, there still appears to be one area that is in my view, painfully manual:  transitioning from stories acceptance criteria/tests to coded (integration) tests.

A story often starts out from being written by the product owner (PO), business Analysis (BA) or User Experience (UX) team.  Acceptance criteria/tests are added as appropriate to provide a “box” for the story, so everyone is clear on the scope and testing of the story further down the road.  Ideally the list of acceptance criteria/tests increases as appropriate so everyone is clear when the story can be moved into the “done” state.

The issue comes when transitioning from the story [card](http://www.stellman-greene.com/blog/wp-content/uploads/2009/05/search-and-replace-user-story-card.png) form to a code base with unit and integration tests.  The acceptance criteria/tests effectively map to integration tests.  In the ideal world the story card acceptance criteria/tests would be written in a DSL and effectively allow auto generation of .feature or similar code files, thus avoiding the dual keying of data.

This leads to a few thoughts around an story acceptance criteria/test DSL/fluent readable language:

Net out, one thought is to push a DSL up to the story card level, and thus educate the PO, BA, UX and QA to write acceptance tests in a more “appropriate” format to reduce down stream “time”

~ by mdavey on December 4, 2012.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)