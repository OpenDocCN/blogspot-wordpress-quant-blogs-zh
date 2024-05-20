<!--yml
category: 未分类
date: 2024-05-12 20:19:36
-->

# Falkenblog: Mauboussin on Success and Luck

> 来源：[http://falkenblog.blogspot.com/2012/10/mauboussin-on-success-and-luck.html#0001-01-01](http://falkenblog.blogspot.com/2012/10/mauboussin-on-success-and-luck.html#0001-01-01)

My 5-year old daughter recently was very excited to discover a new solution to a pressing problem. Her mother had told her she was not allowed to eat cookies and left the room. 5 minutes later Izzie told me she had a great idea: I give her a cookie but

*we don't tell mom*

, so mom wouldn't be upset.  Win-win! Her pride in independently discovering the tactic of lying reminded me that many skills are no less interesting to others simply because I know them.  Such it is with Michael Mauboussin's book,

[The Success Equation](http://www.amazon.com/Success-Equation-Untangling-Business-Investing/dp/1422184234/ref=sr_1_1?s=books&ie=UTF8&qid=1351732312&sr=1-1)

, which investigates how to navigate in a world filled with skill and chance.

The book spends a couple pages explaining the reversion to the mean by noting Galton's original observation on the heights of parents and their children, and much of the book involves the concept of bayesian updating. These aren't new ideas.  Yet, when he noted that while small schools are overrepresented in data on excellent and really bad schools, it reminded me that this is a real problem because invariably they are used as templates for some system-wide initiative, neglecting the fact that often some very unique circumstances as opposed to any efficient method are at work. Like everyone, I need reminding of some of these patterns sometimes.

The author recounts a fortunate interview he had with Drexel back in the days this was one of the most coveted positions out of college. He astutely noticed the senior interviewer had a Redskins trash can and so mentioned something casually about football, after which the interview went extremely well, talking mainly about football.  Clearly, that wasn't just luck, but after the fact appeared the key to him getting hired, creating a career path that would never be the same. Most big events, good and bad, are a mix of skill and chance.

In dealing with success and luck Mauboussin presents a useful model:

estimate=population mean + c*(sample mean - population mean)

c is a constant between 0 and 1, 1 for activities involving all skill, 0 for those that are purely chance. So, a chess, which is mainly skill, should have a c, or 'shrinkage factor', near 1, hockey games something near 0\.  This is like updating a prior belief with new data (see

[here](http://en.wikipedia.org/wiki/Conjugate_prior)

for how to do this more formally for various distributions). More relevant to investing, if your backtest generates a Sharpe of 2, one should remember most investment strategies have Sharpe's near 0, and so adjust your sample mean (ie, backtest) closer to that population mean. Any new idea does worse than its backtests because these aren't population data, but rather selective sample data.

He could have added something on how to address robustness as he did with his shrinkage factor approach to bayesian updating, say by showing how you could optimize over a set of parameters from different subsamples.

The book mentions research by Pinker, Gazzaniga, and Haidt, and I love these authors so I found all that very interesting.  Some of his other inspirations I'm less fond about. He calls Peter Bernstein 'one of the investment industry's greatest thinkers', though I'm at a loss as to what Bernstein insight might deserve such praise.  And then he mentions my favorite flâneur, Nassim Taleb, and suggests his great insight is that when payoffs are uncertain and complex, these are great situations to go long, specifically, go long out-of-the-money options.

Out-of-the-money options aren't underpriced on average. Sure, you will do well when the market tanks, but it's expensive insurance. Remember, when you cross the spread on a 3-delta put, your are giving away a lot of vig. If you think you can trade at mid or close you are being naive (I hear Taleb has a new book out advocating the same thing, buying gamma).

Also riffing on Taleb, he says we are better off using no model than a faulty one. This is a straw man. A faulty model is harmful almost by definition.  Yet  if you are acting, you are acting on

*some*

kind of theory, which is at some level

a

kind of model. One is better served by an attempt to formalize as well as possible one's strategy rather than to merely trade on intuition, the key being how well one deals with the uncertainty by simplifying the functional form, or accurately calibrating the probability of loss, or the time series nature of losses, etc. When people say they have an atheoretical or non-parametric approach they are neglecting a meta-assumption: any idea about how the world behaves involves a theory at some level, which can also be some kind of model (eg, a Venn diagram, or an if-then statement, a linear best-fit through an ellipsoid of data).

I'm not the audience for this book, but as most people are prone to overfitting, it has an audience, such as people who like Taleb's books.

Lastly, I noted he has 5 children, and I'm always  amazed when I read a sustained argument written by someone around my age with more kids than me. Having children is like putting a bowling alley in your head, and makes writing very difficult.  That's skill.