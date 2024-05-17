<!--yml
category: 未分类
date: 2024-05-18 05:43:41
-->

# Code Ownership | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/02/26/code-ownership/#0001-01-01](https://mdavey.wordpress.com/2015/02/26/code-ownership/#0001-01-01)

## Code Ownership

Jay Field’s has an interesting [posting](http://blog.jayfields.com/2015/02/experience-report-weak-code-ownership.html) on code ownership, “Experience Report: Weak Code Ownership”.  “Too many cooks in the kitchen” is unfortunately a problem I suspect we have all seen to many times on medium to large projects.  Stating the obvious, encourage consistency on a large code base over n years is difficult – its unfortunate that stakeholders who haven’t come from a software engineering background don’t really grasp the issues of such problems.

Primary Code Ownership approach sounds interesting, and reminds me of similar approaches from n years ago on projects which entailed a small team on the server and client portion of a project, with a primary owner for each team.   Clearly splitting a project into microservices style can only aid the project by avoiding a single individual attempting to set and govern code ownership of a large code base.

Its probably also worth noting Chris Conley’s recent comments on paired programming, and the killing of code [reviews](http://eatcodeplay.com/why-we-killed-off-code-reviews/).  I think all to often code reviews are over hyped as a silver bullet solution.

> We now fully understand the [overhead](http://blog.codinghorror.com/the-multi-tasking-myth/) of branches and pull requests. It’s not just the act of checking out a branch, writing a great pull request or the 200 LOC/hour for the reviewer.

~ by mdavey on February 26, 2015.

Posted in [Agile](https://mdavey.wordpress.com/category/agile/)