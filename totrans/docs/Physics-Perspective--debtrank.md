<!--yml
category: 未分类
date: 2024-05-18 07:00:42
-->

# Physics Perspective: debtrank

> 来源：[http://physicsoffinance.blogspot.com/2012/08/debtrank.html#0001-01-01](http://physicsoffinance.blogspot.com/2012/08/debtrank.html#0001-01-01)

My latest Bloomberg column can be read

[here](http://www.bloomberg.com/news/2012-08-06/how-google-might-help-us-avert-a-financial-crisis.html)

. The title sounds rather weird, I think, because the research I've written about has nothing to do with Google helping anyone. The hazards of writing and the production process. But ignore that -- I think the subject matter is important, and I wanted to offer some further information on what I wrote about there, and a link to the original research.

The basic topic is a new measure of systemic risk known as DebtRank, which was just introduced a few days ago in

[this new paper](http://www.nature.com/srep/2012/120802/srep00541/full/srep00541.html)

in

*Nature Scientific Reports*

. This is the work of physicist Stefano Battiston and a team of other physicists and economists, and takes its inspiration from the famous

[PageRank algorithm](http://en.wikipedia.org/wiki/PageRank)

invented by Google founders Sergey Brin and Larry Page. DebtRank could do for the analysis of global financial risks what Google did for web search -- make it really possible to determine which elements in the network matter most.

The essential insight of the PageRank algorithm is that in any network of things that make references to each other -- web pages through hypertext links, or scientific papers through citations, for example -- each element effectively votes for other importance of other elements by linking to them. Hence, the most important web pages, Page and Brin reasoned, should be those drawing links from many other pages, especially from other really important pages. The best scientific papers should be those that get those most references, especially from other profoundly important scientific papers (rather than from papers no one ever reads).

To calculate the PageRank of a web page (or a scientific paper), you have to look at all the web pages that link to it. The page gets a higher PageRank in so far as many other pages link to it, especially if those other pages are important, i.e. are pages that have many other web pages linking to them, especially other important web pages. The definition is obviously circular -- you have to know which pages are important in order to be able to calculate which pages are important. That may seem useless, but this problem is easy to sort out mathematically (it's just some linear algebra).  That's what Google algorithm does, and it can be done with lots of computing power, which makes Google so powerful (this is of course only part of the recipe of the search engine). 

Now, what about finance? The analogy for DebtRank is quite direct -- those institutions that present the greatest risks to the financial system are those that, if they fail, would cause the widest spread of economic distress. Naturally, you would tend to have a high DebtRank if you are linked by loans and other financial ties to other firms with high DebtRank -- the same circularity again.

I won't go into more detail except to say that an algorithm can calculate the DebtRank using real data (a partial network of financial ties between institutions based on public information). This is what Battiston and colleagues have done, and it shows some surprises. At the peak of the financial crisis, for example, DebtRank measures for the largest 20 or so banks show that simple bank size just isn't as important as we've come to think. Institutions such as Barclays, Bank of America, JP Morgan and Royal Bank of Scotland presented more systemic risk than did Citigroup or Deutsche Bank, despite being significantly smaller in total assets. Wells Fargo stands out even more: It presented as much systemic risk as Citigroup, despite having only a quarter of the assets. 

This is really only a proof of principle, as the network used is indeed very incomplete. But it shows quite clearly how the phrase "too big to fail" is slightly misleading. We need to worry about which institutions are too central to fail, or really a mixture of too big and too central, and this is what something like DebtRank lets you get at.

Most importantly, the study shows how any assessment of global financial risks will require much more public knowledge of the links between institutions, most of which are currently not public. For more information, I suggest looking at the web site of the European project FOC (Forecasting Financial Crises), in which this research took place. In particular, you may want to have a look at the

[widget](http://ethz.focproject.net:8080/widget)

produced by the researchers that shows some of the key institutions and reflects their systemic risks at the height of the crisis as estimated by DebtRank.