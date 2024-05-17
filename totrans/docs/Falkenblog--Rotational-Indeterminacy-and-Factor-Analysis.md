<!--yml
category: 未分类
date: 2024-05-12 20:51:00
-->

# Falkenblog: Rotational Indeterminacy and Factor Analysis

> 来源：[http://falkenblog.blogspot.com/2011/07/rotational-indeterminacy-and-factor.html#0001-01-01](http://falkenblog.blogspot.com/2011/07/rotational-indeterminacy-and-factor.html#0001-01-01)

A recent Bloggingheads has

[highlighted](http://bloggingheads.tv/diavlogs/37155?in=53:51&out=61:13)

the 'Factor indeterminacy' problem remains a conspicuous if rarely highlighted item among IQ critics due to Stephen Jay Gould's Mismeasure of Man, which remains required reading for many college freshman. Gould set out to demolish all research relating to racial differences in IQ, arguing that neither concept exist, and noting that slave owners and Nazis also believed in these things (Hitler was a vegetarian too, but no one sees the obvious connection there). His main argument against IQ is the following (taken from

[his critique](http://www.dartmouth.edu/~chance/course/topics/curveball.html)

of The Bell Curve):

> Spearman used factor analysis to find a single dimension—which he called g—that best identifies the common factor behind positive correlations among the tests. But Thurstone later showed that g could be made to disappear by simply rotating the dimensions to different positions...In any case, you can't grasp the issue at all without a clear exposition of factor analysis—and The Bell Curve cops out on this central concept.

Basically Gould argued that 'if you can't grasp the issue' you shouldn't have an opinion, as if there's some big math error at the bottom of IQ and if you can't do factor analysis you can't understand IQ. Meanwhile, IQs are remarkable stable over people's lives, belying the assertion they are arbitrary.

[Arbitrage Pricing Theory](http://en.wikipedia.org/wiki/Arbitrage_pricing_theory)

(APT) proposed by Stephen Ross in 1976 generate a flurry of research in the eighties and 1990s, because it extended the basic single factor CAPM to include multiple factors. Such generalizations are popular among academics because they invite a lot of rigorous extensions, perfect for creating publications. These factors could include 'the market', but also something for 'oil', currency risk, and just about any bugaboo you can imagine. The basic idea is to estimate the equation

r=a+bf+e

where r is an nx1 vector of returns over n stocks, and then use factor analysis to extract the factors (f) and the factor loadings (aka 'betas', b). In the CAPM, the factor is the excess market return, Rm-Rf, but this could be instead the vector of {Rm-Rf, Oil price Change}, etc.

Interestingly, there has never been a big worry about factor indeterminacy among finance professors who studied it so carefully. That is, say you multiply b by L, and f by L

^(-1)

. This creates

r=a+bLL

^(-1)

f+e

Now, this simplifies to

r=a+bf+e

So, you can do this with any nonzero L you want and the data are observationally equivalent. That is, you can say everyone had a low factor loading and the factor was really volatile, or the factor loadings were really large and the factor was rather quiet; these are observationally equivalent. Generally, you solve the problem by arbitrarily stipulating that E(ff')=I (the identity matrix), and then everyone knows what you are talking about.

There are ways to test for multiple factors, basically, by estimating k factors and their loadings in sample A, and show that the loadings from sample A explains more of the sample B variance! You can use likelihood ratio tests on k and k+1 factors models, but these I find much less convincing than the out-of sample performance. If you can identify an additional 'music' or 'verbal' IQ, or a 'non-market risk factor', together with their loadings, and then find this also explains subsequent performance on different samples, the world will beat a path to your door. Indeed, in finance people have left the latent factor approach, and chosen instead factor proxies such as 'value' or 'size'. Interestingly, the 'you can't measure the true market factor' issue-- a logical possibility just as possible as that g is unmeasurable--hasn't been a practical problem because either one discusses factors that others can also measure and thus have relatively unambiguous meaning, or you are irrelevant. There is no factor indeterminacy problem because people don't get bogged down on problems that have reasonable solutions (the

[Roll critique](http://en.wikipedia.org/wiki/Roll's_critique)

has been no cause for nihilism).

I found this

*contretemps*

interesting because it's an example of Euler's famous '

[(a + bn)/n = x, hence God exists](http://leonhard-euler.tripod.com/id4.html)

' argument, a statement that seems technical and profound, but is pure squid ink, indicative of bad faith, especially in the context of Gould's assertion that the IQ research bullies people into believing results via abstruse technical arguments (ironic because that is exactly what he did here).

This came up because Jon Horgan was discussing his support for Stephen Jay Gould in light of

[criticism](http://www.plosbiology.org/article/info:doi/10.1371/journal.pbio.1001071)

of his

*Mismeasure of Man*

, where one chapter focused on the work of a 19th-century physician, Samuel George Morton, who amassed a collection of almost 1000 skulls from around the world. Morton estimated the brain size of different racial groups by pouring seed and lead shot into the skulls. He concluded that whites have larger brains on average than blacks.

Gould argued that Morton applied an unconscious bias into his work by selectively including and excluding various skulls in his measurement.

[Recent researchers](http://www.plosbiology.org/article/info:doi/10.1371/journal.pbio.1001071)

revisited the data, and found the reverse: Gould had a biased view of the data, not Morton. The issue centers on which of the 1000 skulls one includes in the sample. Read the paper, it's easy enough for a high school kid to follow. It is hard to see how Gould's selective sampling as opposed to the updated approach is more accurate.

Yet Horgan

[states](http://www.scientificamerican.com/blog/post.cfm?id=defending-stephen-jay-goulds-crusad-2011-06-24)

that:

> their analysis, far from being "straightforward," was highly technical and based on many judgment calls, as were those of Gould and Morton. The divergent results depend in part on whether to include or exclude certain skulls that could unduly skew estimates of brain sizes.

Now, I agree its not easy to put their critique of Gould into a single picture that leaves  room for no other interpretation, but if Horgan is going to state that the judgement calls in their analysis allows him to remain unconvinced then virtually no one can be convinced of anything, because the judgement calls were about as simple as could be (eg, include all skulls labeled 'American Indian' as American Indians and take the average).

Indeed, why Horgan

[defends Gould](http://bloggingheads.tv/diavlogs/37155#A4J2S9F7)

is mainly because he hates biological determinism (as stated, who is for that?), but also as he is now pushing the

[argumentative theory](http://en.wikipedia.org/wiki/Argumentation_theory)

, that brains have evolved to persuade others rather than find truth. While I too think we all are more hard-wired to try and win arguments as opposed to find truths, I would add that the truth is still a good goal. It's simply more productive to have better theories underlying your observations than false theories, otherwise you end up arguing in circles trying to convince people that, say, 'the Hegelian dialectic' is the best way to explain history, which is possible but difficult because it's a crappy theory. Horgan has taken argumentative theory to rationalize his unwillingness to engage in analysis of the data simply because so many researchers are merely rationalizing their biases. He seems to have spent a life studying science and concluded that it's all a game, and he's going to play it as such.

The refutation of Gould is important because it highlights that those who are most strenuously against bias are often the most biased, just as those who say 'it's not about the money' really mean it's all about the money. For Gould this was just the tip of the tendentious iceberg, as he ignored all the contrary and more sophisticated data since Morton on brain size, race, and IQ, that really makes Morton irrelevant (see

[here](http://www.sciencedirect.com/science/article/pii/S1053811904002332)

,

[here](http://psycnet.apa.org/psycinfo/2002-10756-001)

,

[here](http://www.sciencedirect.com/science/article/pii/S0160289604001357)

,

[here](http://brain.oxfordjournals.org/content/129/2/386.short)

,

[here](http://onlinelibrary.wiley.com/doi/10.1002/ajpa.1330400314/abstract)

,

[here](http://ajp.psychiatryonline.org/cgi/content/abstract/150/1/130)

, and

[here](http://www.sciencedirect.com/science/article/pii/0160289694900027)

for some more updated analyses with references), and such errors of omission are most disingenuous because they reflect a strategy of avoiding the opposite's best arguments and instead attacking straw men. He ignored the fact that the higher the g loading a subtest the higher is its heritability, the higher its relation to elementary cognitive tasks like reaction time, and a lot of other such data.

It's possible to maintain a belief as long as the evidence is not common knowledge--something outsiders know you know they know that you know they know etc--because as long as it's not common knowledge, there's a chance you could be

reasonably

wrong. I understand that my prejudices are the most important determinant of how I see the world, but instead of simply accepting that, I try to tackle my adversary's best arguments as opposed to avoid them via the "it's complicated" dodge.

What we see is very theory-laden, we see what we believe. It's not only good to have priors, to have prejudices and beliefs, it's impossible not to. To have strong opinions, weakly held, is a good strategy in such an environment. Moderation in all things. I expect people to be biased, to tell lies, to occasionally betray friends with minor slights, but that doesn't mean I should do it unabashedly. Principles are what keep us from being totally uninteresting shills, in spite of the fact they are also unrealistic ideals.