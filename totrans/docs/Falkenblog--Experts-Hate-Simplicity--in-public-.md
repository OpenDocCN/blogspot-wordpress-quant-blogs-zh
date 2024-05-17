<!--yml
category: 未分类
date: 2024-05-12 22:05:11
-->

# Falkenblog: Experts Hate Simplicity (in public)

> 来源：[http://falkenblog.blogspot.com/2009/05/experts-hate-simple-rules-in-public.html#0001-01-01](http://falkenblog.blogspot.com/2009/05/experts-hate-simple-rules-in-public.html#0001-01-01)

The risk management group Moodys/KMV has a proprietary default model of public companies with several tricky refinements that it

[swears](http://www.moodyskmv.com/research/files/wp/EDF_Validation_All_2007.pdf)

is significantly more powerful than simple applications of the

[Merton model](http://ideas.repec.org/p/uts/rpaper/112.html)

. I have a model,

[Defprob](http://www.defprob.com/)

, that I think does as well as the Moody's model, as it basically uses a Merton model in conjunction with a handful of obvious supplementary inputs. But in any case, I was reacquainted with this strange elevation of useless nuance via the following observation in Geoffrey Miller's new evolutionary biology book,

[Spent](http://www.amazon.com/Spent-Sex-Evolution-Consumer-Behavior/dp/0670020621/vdare)

:

> Is it an accident that researchers at the most expensive, elite, IQ-screening universities tend to be most skeptical of IQ tests? I think not. Universities offer a costly, slow, unreliable intelligence-indicating product that competes directly with cheap, fast, more-reliable IQ tests. They are now in the business of educational credentialism. Harvard and Yale sell nicely printed sheets of paper called degrees that cost about $160,000 ($40,000 for tuition, room, board, and books per year for four years). To obtain the degree, one must demonstrate a decent level of conscientiousness, emotional stability, and openness in one’s coursework, but above all, one must have the intelligence to get admitted, based on SAT scores and high school grades. Thus, the Harvard degree is basically an IQ guarantee.

So basically, those selling costly substitutes for a simple rule are the most vociferous in blasting the simple rule. You could have a simple 'seal of approval' based on some

[g-loaded](http://en.wikipedia.org/wiki/General_intelligence_factor)

test (eg, the SAT> 1300), and some objective extracurricular accompishments to show you aren't a socially obtuse nerd. Throw in passing some on-line courses in physics, computing, English, and statistics, and boom: everyone can be confident you are a great bet as a new hire.

An honest expert admits when a simple alternative does as well as a sophisticated model or analysis. Alas, most experts are not honest, at least not publicly. They aren't evil, they just convince themselves that their years of expertise imply the entire gestalt is necessary to capture the situation, as if the fourth and seventh elements of a power series are essential in a

[power series approximation](http://en.wikipedia.org/wiki/Power_series)

, and naive approaches merely look at the first two terms. The cognitive dissonance needed to believe these self-serving confabulations is something most experts accept as life in the real world, like a politician talking about the public at large while merely handing out jobs and contracts to his voting base--everyone has their axe to grind. As

[Holden Caulfield](http://en.wikipedia.org/wiki/Holden_Caulfield)

noted, most adults are phonies in some way, you just have to learn to deal with it.

Anyone currently in a good position due to more convoluted signalling will pooh-pooh simple solutions, no matter how near-optimal. I remember monitoring our traders as a risk manager, and invariably a market maker would present himself as a savvy speculator, with great insights as to short term movements and longer term trends (these always are in opposite direction, so that way whatever happens falls to plan). Thus, if you said, 'all you do is buy stuff from retail goobs below the bid and sell above the ask, and make riskless profit', you would never be in the circle of trust. Some things on the trade floor, known by everyone, are never stated openly, because phone clerks don't get paid $200k+, while 'traders' do. But it was similar in the Asset and Liability Committee (ALCO) meetings, where you have a bunch of people picking a point in duration space, and smoothing earnings by selectively buying or selling something in the 'banking book' which generates an immediate hit to the pnl even though its value was known for many moons. Such a task could be automated, but then the naked interest rate bets, earning manipulation, would be too transparent. So the ALCO's purpose was to manage earnings, and take interest rate bets, in the most convoluted way possible using all the latest financial jargon: "we are seeking greater liability sensitivity in the current uncertain environment that suggests we synergistically position ourselves to maximize the risk sensitivity..."

Back to credit models, in KMV's case,

[Shumway and Bharath](http://w4.stern.nyu.edu/salomon/docs/Credit2006/shumway_kmvmerton1.pdf)

show that one can simplify the Merton model further, and approximate the Merton approach fairly well. I too find their rule works relatively well.

KMV can always point to their proprietary default database, and as it is proprietary, you can't prove them wrong, though such a database is not nearly as special as they think (these are public firms, after all). I'm 97% sure their model does not significantly outperform a naive Merton Model, and that adding their liability adjustment, or their adjustment to historical volatility by looking at how the liability structure has changed, doesn't add up to anything significant. There is value to having a popular risk measure, however flawed, because it makes communication easier across parochial domains--there are economies of scale in validation and transparency--but that's not a very compelling sales pitch because then you don't have barriers to entry that would protect intangible assets. So the equilibrium tendency is to complicate things more than they should be, and highlight irrelevant nuances and vague principles, because then no one can copy you.

This is all unfortunate because it takes something relatively simple--the default modeling problem has a 'flat maximum'--and makes it seem much more complicated than it really is. It would be nice if valuable analytics or signals were knife-edged and involved subtle nuance, because that implies knowledge is not just 'good', but valuable. For instance, what if

[dynamic programming](http://www.faqs.org/abstracts/Economics/Dynamic-programming-with-homogenous-functions-Tax-distortions-in-a-neoclassical-monetary-economy.html)

generated clearly superior fiscal policy? Or if

[2-stage least squares](http://economics.about.com/od/economicsglossary/g/twostage.htm)

was really more useful than ordinary least squares? The

[Wald, Likelihood ratio, and Lagrange Multiplier](http://www.ats.ucla.edu/stat/mult_pkg/faq/general/nested_tests.htm)

statastical tests all necessary and complimentary? Then, all that hard work, that extensive, difficult to emulate knowledge would be worth quite a bit.

Truly good ideas are pretty robust and involve a handful of parochial, but straightforward adjustments. It helps to know the fancy math extensions to be sure of this, and often it takes an advanced knowledge to apply simple principles well, but the bottom line is an optimal solution that is not very 'sophisticated'. No one wants to hear this, because if you educate yourself sufficiently to understand the problem well enough to actually know if this is true in any specific case you have a vested interest in having a complicated solution.