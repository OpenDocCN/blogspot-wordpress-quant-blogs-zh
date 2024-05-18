<!--yml
category: 未分类
date: 2024-05-18 06:58:51
-->

# Physics Perspective: Let there be light

> 来源：[http://physicsoffinance.blogspot.com/2013/02/let-there-be-light.html#0001-01-01](http://physicsoffinance.blogspot.com/2013/02/let-there-be-light.html#0001-01-01)

*** UPDATE BELOW***

My Bloomberg column this month looks at an idea for improving the function of the interbank lending market. The idea is radical, yet also conceptually very simple. It's radical because it proposes a complete transformation of banking transparency. It shows how transparency may be the best route to achieving overall banking stability and efficiency. It will be interesting to see what free-market ideologues think of the idea, as it doesn't fit into any standard ideological narrative such as "get government out of the way" or "unregulated markets work best." It offers a means to improve market function -- something one would expect free-market cheerleaders to favor -- but does so in a way that threatens banking secrecy and also involves some central coordination.

My column was necessarily vague on detail given its length, so let me give some more discussion here. The paper presenting the ideas is

[this one](http://arxiv.org/abs/1301.6115)

by Stefan Thurner and Sebastian Poledna. It is first important to recognize that they consider here not all markets, but specifically the interbank market, in which banks loan funds to one another to manage demands for liquidity. This is the market that famously froze up following the collapse of Lehman Brothers, as banks suddenly realized they had no understanding at all of the risks facing potential counterparties. The solution proposed by Thurner and Poledna strikes directly at such uncertainty, by offering a mechanism to calculate those risks and make them available to everyone.

Here's the basic logic of their argument. They start with the point that standard theories of finance operate on the basis of wholly unrealistic assumptions about the ability of financial institutions to assess their risks rationally. Even if the individuals at these institutions were rational, the overwhelming complexity of today's market makes it impossible to judge systemic risks because of a lack of information:

> Since the beginning of banking the possibility of a lender to assess the riskiness of a potential borrower has been essential. In a rational world, the result of this assessment determines the terms of a lender-borrower relationship (risk-premium), including the possibility that no deal would be established in case the borrower appears to be too risky. When a potential borrower is a node in a lending-borrowing network, the node’s riskiness (or creditworthiness) not only depends on its financial conditions, but also on those who have lending-borrowing relations with that node. The riskiness of these neighboring nodes depends on the conditions of their neighbors, and so on. In this way the concept of risk loses its local character between a borrower and a lender, and becomes systemic.
> 
> The assessment of the riskiness of a node turns into an assessment of the entire financial network [1]. Such an exercise can only carried out with information on the asset-liablilty network. This information is, up to now, not available to individual nodes in that network. In this sense, financial networks – the interbank market in particular – are opaque. This intransparency makes it impossible for individual banks to make rational decisions on lending terms in a financial network, which leads to a fundamental principle: Opacity in financial networks rules out the possibility of rational risk assessment, and consequently, transparency, i.e. access to system-wide information is a necessary condition for any systemic risk management.

In this connection, recall Alan Greenspan's famous admission that he had trusted in the ability of rational bankers to keep markets working by controlling their counterparty risk. As he exclaimed in 2006,

> "Those of us who have looked to the self-interest of lending institutions to protect shareholder's equity -- myself especially -- are in a state of shocked disbelief."

The trouble, at least partially, is that no matter how self-interested those lending institutions were, they couldn't possibly have made the staggeringly complex calculations required to assess those risks accurately. The system is too complex. They lacked necessary information. Hence, as Thurner and Poledna point out, we might help things by making this information more transparent.

The question then becomes: is it possible to do this? Well, here's one idea. As the authors point out, much of the information that would be required to compute the systemic risks associated with any one bank is already reported to central banks, at least in developed nations. No private party has this information. No single investment bank has this information. Perhaps even no single central bank has this information. But central banks together do have it, and they could use it to perform a calculation of considerably value (again, in the context of the interbank market):

> In most developed countries interbank loans are recorded in the ‘central credit register’ of Central Banks, that reflects the asset-liability network of a country [5]. The capital structure of banks is available through standard reporting to Central Banks. Payment systems record financial flows with a time resolution of one second, see e.g. [6]. Several studies have been carried out on historical data of asset-liability networks [7–12], including overnight markets [13], and financial flows [14].
> 
> Given this data, it is possible (for Central Banks) to compute network metrics of the asset-liability matrix in real-time, which in combination with the capital structure of banks, allows to define a systemic risk-rating of banks. A systemically risky bank in the following is a bank that – should it default – will have a substantial impact (losses due to failed credits) on other nodes in the network. The idea of network metrics is to systematically capture the fact, that by borrowing from a systemically risky bank, the borrower also becomes systemically more risky since its default might tip the lender into default. These metrics are inspired by PageRank, where a webpage, that is linked to a famous page, gets a share of the ‘fame’. A metric similar to PageRank, the so-called DebtRank, has been recently used to capture systemic risk levels in financial networks [15].

I wrote a little about this DebtRank idea

[here](http://physicsoffinance.blogspot.co.uk/2012/08/debtrank.html)

. It's a computational algorithm applied to a financial network which offers a means to assess systemic risks in a coherent, self-consistent way; it brings network effects into view. The technical details aren't so important, but the original paper proposing the notion is

[here](http://www.nature.com/srep/2012/120802/srep00541/full/srep00541.html)

. The important thing is that the DebtRank algorithm, along with the data provided to central banks, makes it possible in principle to calculate a good estimate of the overall systemic risk presented by any bank in the network. 

So imagine this: central banks around the world get together tomorrow, and within a month or so manage to coordinate their information flows (ok, maybe that's optimistic). They set up some computers to run the calculations, and a server to host the results, which would be updated every day, perhaps even hourly. Soon you or I or any banker in the world could go to some web site and in a few seconds read out the DebtRank score for any bank in the developed world, and also to see the listing of banks ranked by the systemic risks they present. Wouldn't that be wonderful? Even if central banks took no further steps, this alone would be a valuable project, using global information to produce a globally valuable information resource for everyone. (Notice also that publishing DebtRank scores isn't the same as publishing all the data that banks supply to their central banks. That level of detail could be kept secret, with only the single measure of overall systemic risk being published.)

I would hope that almost everyone would be in favor of such a project or something like it. Of course, one group would be dead set against it -- those banks who have the highest DebtRank scores because they are systemically the most risky. But their private concerns shouldn't trump the public interest in reducing such risks. Measuring and making such numbers public is the first step in making any such reduction.

But Thurner and Poledna do go further in making a specific proposal for using this information in a sensible way to reduce systemic risks. Here's how that works. Banks in the interbank market borrow funds for varying amounts of time from other banks. Typically, there's a standard interbank interest rate prevailing for all banks (as far as I understand). Hence, a bank looking to borrow doesn't really have much preference as to which bank it finds as a lender; the interest paid will be the same. But if the choice of lender doesn't matter to the borrowing bank, it does matter a lot to the rest of us, as borrowing from a systemically risky bank threatens the financial system. If the borrower can't pay back, that risky bank could be put into distress and cause trouble for the system at large. So, we really should have banks in the interbank market looking to borrow first from the least systemically risky banks, i.e. from those with low values of DebtRank.

This is what Thurner and Poledna propose. Let central banks regulate that borrowers in the interbank market do just that -- seek out the least risky banks first as lenders. In this way, banks acting to take on lots of systemic risk would thereby be marked as too dangerous to make further loans. Further borrowing would instead be undertaken by less risky banks, thereby improving the spread of risks across the system. Don't trust in the miracle of the free market to make this happen -- it won't -- but step in and provide a mechanism for it to happen. As the authors describe it:

> The idea is to reduce systemic risk in the IB network by not allowing borrowers to borrow from risky nodes. In this way systemically risky nodes are punished, and an incentive for nodes is established to be low in systemic riskiness. Note, that lending to a systemically dangerous node does not increase the systemic riskiness of the lender. We implement this scheme by making the DebtRank of all banks visible to those banks that want to borrow. The borrower sees the DebtRank of all its potential lenders, and is required (that is the regulation part) to ask the lenders for IB loans in the order of their inverse DebtRank. In other words, it has to ask the least risky bank first, then the second risky one, etc. In this way the most risky banks are refrained from (profitable) lending opportunities, until they reduce their liabilities over time, which makes them less risky. Only then will they find lending possibilities again. This mechanism has the effect of distributing risk homogeneously through the network.

The overall effect in the interbank market would be -- in an idealized model, at least -- to make systemic banking collapses much less likely. Thurner and Poledna ran a number of agent-based simulations to test out the dynamics of such a market, with encouraging results. The model involves banks, firms and households and their interactions; details in the paper for those interested. Bottom line, as illustrated in the figure below, is that cascading defaults through the banking system become much less likely. Here the red shows the statistical likelihood over many runs of banking cascades of varying size (number of banks involved) when borrowing banks choose their counterparties at random; this is the "business as usual" situation, akin to the market today. In contrast, the green and blue show the same distribution if borrowers instead sought counterparties so as to avoid those with high values of DebtRank (green and blue for slightly different conditions). Clearly, system wide problems become much less likely.

![](img/468729d922dd2a37ff38b37ed271c1de.png)

Another way to put it is this: banks currently have no incentive whatsoever, when seeking to borrow, to avoid borrowing from banks that play systemically important roles in the financial system. They don't care who they borrow from. But we do care, and we could easily force them -- using information that is already collected -- to borrow in a more responsible, safer way. Can there be any argument against that?

What are the chances for such a sensible idea to be put into practice? I have no idea. But I certainly hope these ideas make it quickly onto the radar of people at the new

[Office for Financial Research](http://www.treasury.gov/initiatives/ofr/Pages/default.aspx)

.

**UPDATE**

A reader emailed to alert me to

[this blog](http://www.tyillc.blogspot.co.uk/p/fdr-framework.html)

he runs which champions the idea of "ultra transparency" as a means for ensuring greater stability in finance. At face value, it makes a lot of sense and I think that the work I wrote about today fits into this perspective very well. The idea is simply that governments can provide information resources to the markets which would support better decisions by everyone in reckoning risks and rewards. Of course, we need independent people and firms gathering information in a decentralized way. But that isn't enough. In today's hypercomplex markets, some of the risks are simply invisible to anyone lacking vast quantities of data and the means to analyze them. Only governments currently have the requisite access to such information.