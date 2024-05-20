<!--yml
category: 未分类
date: 2024-05-12 22:20:47
-->

# Falkenblog: Statistical Errors Play into Popular Demand

> 来源：[http://falkenblog.blogspot.com/2009/02/statistical-errors-play-into-popular.html#0001-01-01](http://falkenblog.blogspot.com/2009/02/statistical-errors-play-into-popular.html#0001-01-01)

From

[A case for Due Diligence in Policy Formation:](http://www.fraserinstitute.org/commerce.web/product_files/CaseforDueDiligence_Cda.pdf)

> In 1993, a team of researchers led by D.W. Dockery and C.A. Pope published a study in he New England Journal of Medicine supposedly showing a statistically significant correlation between atmospheric fine particulate levels and premature mortality in six US cities.
> 
> The audit of the HSC data reported no material problems in replicating the original results, though there were a few coding errors. However, their sensitivity analysis showed the risk originally attributed to articles became insignificant when sulphur dioxide was included in the model, and the estimated health effects differed by educational attainment and region, weakening the plausibility of the original findings. The HEI also found that there were simultaneous effects of different pollutants that needed to be included in the analysis to obtain more accurate results.

This is always the case, as empirical errors are mainly parochial issues involved the data, as opposed to whether one used 2 or 3-stage least squares. The authors go over several high-impact studies that were initially well-received and now seen as impossibly flawed: The Boston Fed discrimination study, the Global Warming Hockey stick graph, the Freakonomics Abortion and Crime study, the Bellesiles documentation that early Americans rarely owned guns, and others.

Doing complex problem sets with nuances that are really abstract helps you know the basics, yet at the end of it all the useful tools of analysis are all covered in undergraduate statistics. It takes years of study to really understand it, as I remember not really understanding basic probability and statistics until I TA'd the course three times in graduate school. They key is controlling for relevant omitted variables, knowing whether the relevant variability is over time or within a time period, how the errors are distributed, and other prosaic issues.

Academics are really good at proofs, refinements of cutting edge applications, but these are generally pretty irrelevant to any practical issue. The important insights in data come from understanding the data. In every case, the problem studies had one key commonality:

they were results people wanted to believe

. When people publish results consistent with intuition, especially when it is done in an academic way by making abstruse second order adjustments to coefficients and standard errors, this gives any piece sufficient superficial rigor so that you can then say to your critics: "if you do not understand instrumental variables (say), then you cannot criticize this study!" People love using these kinds of papers to buttress their pet policies, and thus they become popular.

Consider the

[study](http://research.chicagogsb.edu/IGM/docs/ZingalesCulturGenderMath.pdf)

put out by four economists led by Paola Sapienza and Luigi Zingales in economics that supposedly proved the sex gap in mathematical abilities disappears when everyone embraces women's emancipation. In other words, The Man is at fault, as usual, for observed human biodiversity, a prized academic result (the Dean may show up at your seminar!). An anonymous blogger,

[La Grifffe du Lion](http://www.lagriffedulion.f2s.com/math2.htm)

, demolishes this and related studies by adjusting for the following facts:

2.  the math gap mainly occurs only after the onset of puberty

4.  simple proficiency tests do not measure ability relevant to explaining the proportion of engineers and top scientists, who are all highly proficient at mathematics

6.  the means are not as important as the relative variances of the distributions when comparing the proportion of groups in extremums

8.  higher IQ countries implies the level of 'proficiency' is less of an extreme tail cutoff, which lower group differences.

These corrections are not purely statistical, rather, they come from understanding the issue (eg, that gender differences appear only after hormones start diverging). It comes from understanding the phenomenon in question, as opposed to some abstract second-order statistical tweak.

The best way to succeed in academics is to assess what the zeitgeist currently wants documented, and give it to them in a long article with lots of abstruse mathematics. By the time someone says, "you assumed unobserved credit scores of the applications is uncorrelated with race", well, by then you have tenure and can call such criticisms hair splitting (though, conspicuously, you never publish on that subject again). Indeed, Liebowitz's rebuttal of Munnell's Boston Fed study is not great econometrics, and so Munnell was published in the AER, Liebowitz in the Journal of Obscure Economics, yet Liebowitz was right and Munnel wrong. But the result of Munnell was something many people, including academics, wanted to be true, so they read the conclusion (we can costlessly help poor people!), focused on second-order statistical adjustments but ignored bigger issues like omitted variables, noisy data, and the fact that default rates were, if anything, higher on the group than supposedly is held to a higher credit standard. While some might have noticed the increase in housing prices post 2000, no one was on the warpath saying we need to make current lending criteria more stringent prior to 2007\. The cause of this mortgage bubble was something very few people wanted to tackle.

Thus, the problem in the mortgage debacle is not some specific statistical test, an obscure Value-at-Risk assumption buried in a footnote of Jorion's text, but merely an assumption anyone could understand (housing prices do go down, no money down is a very dangerous 'innovation'), yet no one cared about. Investment banks, academics, and regulators considered this scenario irrelevant for a variety of reasons, but most importantly because it was intellectually defensible (mortgage loss rates had not increased since underwriting standards started deteriorating in the early 1990's due to regulatory pressure), and it was something they wanted to believe (if true, it was generated a lot of money and votes for everyone involved). We can now go back and find all the technical errors by Moody's or the Boston Fed study, but anyone who thinks that moving from a 10-day VaR to an annual horizon is missing the deeper point, that the assumptions most dangerous are the one's that are changing due to some new big trend--tax shelter REIT's in the 1980's, new economy companies in the late 1990's--and people applying the old standard find themselves marginalized in the boom, and they become powerless if not jobless at the peak.