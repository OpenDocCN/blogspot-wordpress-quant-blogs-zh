<!--yml
category: 未分类
date: 2024-05-12 21:09:17
-->

# Falkenblog: Can a Computer do Your Job?

> 来源：[http://falkenblog.blogspot.com/2011/01/can-computer-do-your-job.html#0001-01-01](http://falkenblog.blogspot.com/2011/01/can-computer-do-your-job.html#0001-01-01)

Physicist Steven Hsu has

[several interesting observations](http://infoproc.blogspot.com/2011/01/credentialism-and-elite-performance.html)

on the selection process of colleges and elite firms. One little aside on college admissions I found very amusing:

> When I was on the faculty at Yale I knew people in admissions and it's not clear to me that they were the best able to spot potential in 18 year olds. In studies of expert performance admissions people are less good at predicting UG[undergrad] GPA than a simple algorithm. (The "algorithm" is simply a weighted sum of SAT and HS GPA!)

When I worked at a bank, I remember we had a bunch of 'underwriters', and their job was to evaluate the creditworthiness of loan applicants. Coming out of grad school, I had no experience with this, and they had this very complex, holistic methodology. Later, when I became head of capital allocations and we started quantifying their portfolios, I invariably found they could be replicated via some pretty simple rules. This got me excited about going to Moody's to help develop their new RiskCalc Private firm model, which today dominates private firm underwriting worldwide. Anyway, the simple trick was always the same:

1) identify the key indicators

2) transform them appropriately (eg, turn 'profits' into percentile for profit/assets, or some sigmoidal transformation like exp(x)/(1+exp(x))

3) weight or crosstab the indicators

4) add 'em up, and transform output into meaningful buckets used for pricing (200 bps) or risk classification (eg BBB)

Risk is invariably on a log scale, so usually the ordinal rankings correspond to exponential increases in expected default rates.

Anyway, with hindsight, I found most of the facade put forth by various departments (eg, auto lending, health care lending), was very misleading. Everyone made the simple complicated. I think deep down, no one likes to think a computer can do their job, and there are many instances where exceptions matter, so a great deal is made out of these special cases. Yet the false positives made them great anecdotes, but horrible for generalizations. Thus, simple rules dominate their much more costly, confusing, and non-quantitative product created by teams of analysts.

These jobs seem rather common. For example, In the nineties many 'traders' I knew would simply buy from a customer at the bid, and then sell to another customer at the ask, and go home 'making' $10k a day. They would then get a $500k annual bonus. A college admissions director probably interviews people all day, and writes pages of material supplementing their decisions, but all to trail a simple linear rule. I also worked in an econ department, where we created tons of forecasts with lots of commentary, all dominated by vector autoregressions. Our asset/liability committees would often have a lot of commentary about where various interest rates are going, as if these forecasts were any better than what could be lifted from forward prices.

People in these situations are rather quite pathetic. Many are really good people, and would take a big pay cut if they started over, so its not as simple as just choosing a new career.