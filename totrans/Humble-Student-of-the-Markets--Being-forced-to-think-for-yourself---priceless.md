<!--yml
category: 未分类
date: 2024-05-18 03:41:58
-->

# Humble Student of the Markets: Being forced to think for yourself...priceless

> 来源：[https://humblestudentofthemarkets.blogspot.com/2014/03/being-forced-to-think-for.html#0001-01-01](https://humblestudentofthemarkets.blogspot.com/2014/03/being-forced-to-think-for.html#0001-01-01)

When I started this blog, I had been advocating that quantitative analysts think long and hard about the underlying assumptions of their models, otherwise known as conducting a "sanity test" on model results. Cullen Roche of

[Pragmatic Capitalism](http://pragcap.com/models-are-great-if-you-understand-their-limitations)

recently said the same thing when he wrote about the limitations of economic models. He believed that economists overly obsess over the mathematical elegance of their models (emphasis added):

> And that’s the key. I think that economic modelling is very useful. It helps conceptualize important points and gives us a general framework for understanding the world. But we should also be aware of the weaknesses embedded in many of these models because many of these models are simplified to the point that they are misleading. And ***this stems from another big problem revolving around the way many economists obsess over mathematics***.

**Regression blindness**

Frances Woolley at

[Worthwhile Canadian Initiative](http://worthwhile.typepad.com/worthwhile_canadian_initi/2014/03/why-do-people-get-so-worked-about-linear-probability-models.html)

complained about the same kind of blindness from her students. They focus too much on technique, rather than what they are trying to explain, in light of the problems with the data:

> People make elementary errors when they run a regression for the first time. They inadvertently drop large numbers of observations by including a variable, such as spouse's hours of work, which is missing for over half their sample. They include every single observation in their data set, even when it makes no sense to do so. For example, individuals who are below the legal driving age might be included in a regression that is trying to predict who talks on the cell phone while driving. People create specification bias by failing to control for variables which are almost certainly going to matter in their analysis, like the presence of children or marital status.
> 
> But it is rare that I will have someone come to my office hours and ask "have I chosen my sample appropriately?" Instead, year after year, students are obsessed about learning how to use probit or logit models, as if their computer would explode, or the god of econometrics would smite them down, if they were to try to explain a 0-1 dependent variable by running an ordinary least squares regression.
> 
> I try to explain "look, it doesn't matter. It doesn't make much difference to your results. It's hard to come up with an intuitive interpretation of what logit and probit coefficients mean, and it's a hassle to calculate the marginal effects. You can run logit or probit if you want, but run a linear probability model as well, so I can tell whether or not anything weird is going on with the regression."
> 
> But they just don't believe me.

In essence, students just want to know the "formula" and spend less time thinking and understanding the problem that they are trying to address:

> Once students know how to appropriately define a sample, deal with missing values, spot an obviously endogenous regressor, and figure out which explanatory variables to include in their model, then it might be worth having a conversation about the relative merits of probit and linear probability models. Until then, I'm telling my students to use the regress command and, if it makes them feel better, stick "robust" at the end of it.

That`s because their training emphasizes technique over analysis, which is a complaint similar to the one Cullen Roche voiced:

> It all comes down to the way that they have been taught econometrics. Most - not all - econometrics classes emphasize statistical theory. Students might run regressions, but often these are canned, ready-made examples, with the parameters of the analysis clearly defined, or straightforward replication exercises.
> 
> Econometrics is taught that way for a simple, practical reason: it's easy. When every student downloads his own data, works on his own unique problem, and specifies a novel and original model, each student will need a lot of individual help and attention. The marking cannot be delegated to a TA, because each research question, and each data set, is different, so it is impossible to write down a simple answer key. But spending hours upon hours reading students' first struggling steps at regression analysis is a huge amount of work. It's so much easier to mark a final exam consisting of calculations, short answer questions, and replication of theorems.

**Can I just plug in my numbers and get the answer?**

Here is another example. A few years ago I wrote a post about the

[limitations of Altman Z](http://humblestudentofthemarkets.blogspot.com/2008/05/limitations-of-altman-z.html)

. I wrote that Altman Z score was a useful first cut at solvency analysis for operating companies, but had many industry specific problems:

> The main problem with this formulation of solvency risk is that the formula is not suited for many industries. As an example, when I first tried to apply Altman Z I found that many regulated utilities showed up as having high bankruptcy risk.
> 
> I found that Altman Z was not industry specific enough to my liking. For instance, low or negative working capital doesn’t score well on Altman Z but some industries can operate with zero or negative working capital. For example, a restaurant gets paid in cash, but their suppliers will generally give them net 30 on their payables and the inventory (food) turns over very quickly.
> 
> Another sector that the Altman Z doesn’t analyze is the financial sector. What does “sales” mean for a bank? Financials tend to be highly levered and their operating risks and exposures are not well disclosed.

That post still gets read once in a while because it serves as a useful reference on the Altman Z score. Then, the other day, I get a

[question](http://humblestudentofthemarkets.blogspot.ca/2008/05/limitations-of-altman-z.html?showComment=1395574728915#c3348566714827220951)

asking if "we (can) use Altman Z score to predict (the) banking industry?"

Think about that for a minute, the original Altman Z score assigned weights to different measures of solvency, such as working capital adequacy, EBIT margin, turnover, etc. The weights appeared to have been optimized for operating companies in manufacturing or distribution. Do those weights make sense for a bank? If an analyst had spent just a few minutes thinking about the underlying assumptions of Altman Z; how it relates to the business model of a typical manufacturer and then thought about the business model of a bank; he would instantly have the answer.

These episodes are important lessons to young quantitative analysts and could be inspiration for a MasterCard ad (all figures are approximations):

*   An undergrad degree (at $30K a year for 4 years): $120K
*   A graduate degree: $80K
*   Being forced to think for yourself....priceless

*Cam Hui is a portfolio manager at [Qwest Investment Fund Management Ltd.](http://www.qwestfunds.com/) (“Qwest”). The opinions and any recommendations expressed in the blog are those of the author and do not reflect the opinions and recommendations of Qwest. Qwest reviews Mr. Hui’s blog to ensure it is connected with Mr. Hui’s obligation to deal fairly, honestly and in good faith with the blog’s readers.”

None of the information or opinions expressed in this blog constitutes a solicitation for the purchase or sale of any security or other instrument. Nothing in this blog constitutes investment advice and any recommendations that may be contained herein have not been based upon a consideration of the investment objectives, financial situation or particular needs of any specific recipient. Any purchase or sale activity in any securities or other instrument should be based upon your own analysis and conclusions. Past performance is not indicative of future results. Either Qwest or I may hold or control long or short positions in the securities or instruments mentioned.*