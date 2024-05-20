<!--yml
category: 未分类
date: 2024-05-18 03:29:40
-->

# Humble Student of the Markets: Can a quant make a fruit salad?

> 来源：[https://humblestudentofthemarkets.blogspot.com/2014/11/can-quant-make-fruit-salad.html#0001-01-01](https://humblestudentofthemarkets.blogspot.com/2014/11/can-quant-make-fruit-salad.html#0001-01-01)

I describe myself in my LinkedIn profile as a "left and right brained modeler of quantitative investment systems". While the left and right brained metaphor may not be entirely technically correct, people generally get the idea.

**Watch out for black boxes!**

It is with that theme that I reiterate my point that good quantitative analysts need both book smarts and street smarts. John Chisholm, who is the CIO of the quantitatively oriented asset manager Acadian Asset Management, described the challenges this way in an

[Institutional Investor](http://www.institutionalinvestor.com/blogarticle/3392374/blog/the-fundamental-challenge-of-fundamental-investing.html#.VGFWs7l0zPZ)

article:

> Black box data-crunching quant is not the answer. I believe it is possible to design a quantitative approach that replicates many of the best features of fundamental management individual company insight, depth, conviction, forward focus, responsiveness and adaptability.
> 
> Modern quantitative investing is creative. With the right tools, the data explosion can become a trove of resources to help identify the kinds of fundamental company and market characteristics that may lead to future outperformance. Managers need to apply these insights consistently, to the largest possible universe of opportunity, and be disciplined even or especially  when decisions are counterintuitive.

I believe that Chisholm is has the correct approach but he may be overly optimistic. If I am reading him correctly, Chisholm is advocating the implementation a form of AI, or Artificial Intelligence, for quantitative investing.

**The failure of Big Data** [Michael L Jordan](http://www.cs.berkeley.edu/~jordan/)

, who is the Pehong Chen Distinguished Professor at the University of California, Berkeley and a leading authority on machine learning, disagrees about the use of so-called "Big Data" and AI. In an interview with

[IEEE Spectrum](http://spectrum.ieee.org/robotics/artificial-intelligence/machinelearning-maestro-michael-jordan-on-the-delusions-of-big-data-and-other-huge-engineering-efforts)

, Jordan stated that we have little sense of how human intelligence really works, so the task of modeling human intelligence is overly ambitious at this point:

> I wouldn’t want to put labels on people and say that all computer scientists work one way, or all neuroscientists work another way. But it’s true that with neuroscience, it’s going to require decades or even hundreds of years to understand the deep principles. There is progress at the very lowest levels of neuroscience. But for issues of higher cognition—how we perceive, how we remember, how we act—we have no idea how neurons are storing information, how they are computing, what the rules are, what the algorithms are, what the representations are, and the like. So we are not yet in an era in which we can be using an understanding of the brain to guide us in the construction of intelligent systems.

The current applications of big data is bound to see some spectacular failure because of dumb machine intelligence:

> In a classical database, you have maybe a few thousand people in them. You can think of those as the rows of the database. And the columns would be the features of those people: their age, height, weight, income, et cetera.
> 
> Now, the number of combinations of these columns grows exponentially with the number of columns. So if you have many, many columns—and we do in modern databases—you’ll get up into millions and millions of attributes for each person.
> 
> Now, if I start allowing myself to look at all of the combinations of these features—if you live in Beijing, and you ride bike to work, and you work in a certain job, and are a certain age—what’s the probability you will have a certain disease or you will like my advertisement? Now I’m getting combinations of millions of attributes, and the number of such combinations is exponential; it gets to be the size of the number of atoms in the universe.
> 
> Those are the hypotheses that I’m willing to consider. And for any particular database, I will find some combination of columns that will predict perfectly any outcome, just by chance alone. If I just look at all the people who have a heart attack and compare them to all the people that don’t have a heart attack, and I’m looking for combinations of the columns that predict heart attacks, I will find all kinds of spurious combinations of columns, because there are huge numbers of them.
> 
> So it’s like having billions of monkeys typing. One of them will write Shakespeare.

In other words, Big Data can be very book smart, but it has no street smarts.

**Making the wrong assumptions**

Here is what I mean by street smarts. The typical quantitative financial analyst will tend to implement models without understanding the underlying assumptions.

Consider the example of the difficulties of investing in Russia. This

[Time](http://time.com/3547935/putin-pugachev-oligarchs/)

magazine article of an interview with Sergei Pugachev, an out-of-favor Russian who was formerly known as “Kremlin’s banker”. Pugachev describes Putin's behavior as the new Tsar of Russia (my words, not his):

> Over the past 15 years, Putin has weakened most institutions in Russia that could act as blocks to his power: political parties, the media, the courts, the civil service, regulators and police. Putin gradually side-lined all the individuals he inherited from Yeltsin’s Kremlin. He is now surrounded by close friends, mostly from St. Petersburg and the security services, such as Vladimir Yakunin (head of Russian Railways) and Igor Sechin (head of the Rosneft oil company), who have reportedly become wealthy during his time in office.
> 
> If they want something, they get it, Pugachev said: from a Russian shipyard to a Ukrainian province.
> 
> “If Putin says he wants to buy something, you cannot say that you do not want to sell. If he says ‘I want to buy something’ then you say, ‘Thanks for saying you want to buy it, and not just taking it,’” Pugachev says.
> 
> The authorities’ light-fingered approach to private property has been one of many reasons why investors have been reluctant to leave their money in Russia. Capital flight is due to hit $85.3 billion this year this year, partly as a result of Western sanctions on Russian business. The rouble has lost around a fifth of its value against the dollar since the summer.

[![](img/3618ef2a7a4c72a1ec8e43a7c13bd29f.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiK7bw5hw4PxBQlr1cR5jnWOeeBphopkpBMXG2XJwfzbH7xO8O9CpeRHydNoL9-bjAw45UFnAelauQn5sTQg4-rMNtTXMQE_bOpiq1CrnF8pYmOsIbTnuS4F9w5L1Tx5okq41rDUwFRGq0/s1600/putin.jpg)

In the old Tsarist Russia, everything belonged to the Tsar. You made money by getting a license from the Tsar for a certain activity, such as fishing for herring in the Baltic. The license could be taken away at any time at the Tsar's pleasure. Such a framework for doing business creates certain incentives and disincentives. First of all, you have no property rights. Since the license could be taken away at any time, you behaved in a highly political manner, and you have no incentive to undertake capital investments. The correct approach under such circumstances would be to engage in a harvesting strategy - to take as much as you could and suck the resource dry. That's the sort of Russia that Putin seems to be encouraging.

How many quants will have those kinds of assumptions in their spreadsheets?

**Assuming similarity of culture**

The mistake that rookie quants make is that he assumes that everyone thinks the same way as westerners. Consider this example of a talk by Paul Smith about the difficulties that private banks are having with achieving the kind of profitability that they would like to have in Asian markets (emphasis added):

> Asia Pacific has nearly as many high-net-worth individuals as the United States, the region with the highest number of HNWI in the world, according to the 2014 World Wealth Report. And their numbers are growing fast.
> 
> So why have some private banks in the region grumbled about profit?
> 
> Paul Smith, CFA, managing director, Asia Pacific global head, institutional partnerships, at CFA Institute, says it’s because private wealth business models in the region are not connecting with the needs of local clients.
> 
> Speaking at the recent [Wealth Think](http://wealth-think.com/) conference in Singapore, Smith said: “***I would argue that the business models in this region are struggling, and one of the reasons for that is the business models that are most current here are European or North American business models that are being imposed upon a client base that is, today, predisposed against those models.***” He noted, for example, that many firms talk about running an advisory business model in a market that’s resistant to the idea of paying for investment advice.

There is a relatively short video at this

[link](http://blogs.cfainstitute.org/investor/2014/11/04/whats-wrong-with-the-asian-wealth-management-industry/)

that`s well worth watching. In effect, Smith explained that Asians are highly resistant to the western model of paying for financial advice. They prefer direct investments that they can touch and feel, such as real estate and private equity. They loathe co-mingled vehicles such as funds. Instead, western private banks try to push equity investments in the form of pooled funds. Is there any wonder why bankers are not successful?

Is the behavior of Asian investor modeled differently in spreadsheets?

**Book smart vs. street smart**

The moral of these stories are: Be book smart, but learn to be street smart as well.

I once read terrific definitions of the two terms. Being book smart means that you know a tomato is a fruit, as that knowledge can be profitability on its own. Being street smart is knowing not to put a tomato in a fruit salad.

If you're just book smart, you will one day go down the Big Data road and end up investing based on

[spurious correlations](http://tylervigen.com/view_correlation?id=1597)

like this:

**US spending on science, space, and technology ****vs.**

**Suicides by hanging, strangulation and suffocation**

Make sure you know how to properly make a fruit salad.