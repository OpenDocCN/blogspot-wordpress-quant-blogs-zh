<!--yml
category: 未分类
date: 2024-05-18 05:47:48
-->

# Big Data – Getting Over The Hype | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/08/04/big-data-getting-over-the-hype/#0001-01-01](https://mdavey.wordpress.com/2014/08/04/big-data-getting-over-the-hype/#0001-01-01)

Big Data is one of those buzz words that unless applied to specific business solutions is often in the stratosphere on detail.  In the financial arena there has always been a large around of data in the house.  Lets start with a few real-world data insight solutions which hopefully the usual suspect sell-side organisations are working too.

# Straight Through [Processing](http://www.wallstreetandtech.com/data-management/is-big-data-a-problem-or-an-opportunity--/a/d-id/1297613) (STP) Efficiency

Architecting an STP solution usually comes about due to the need to resolve numerous manual steps in a workflow that is traversed frequently within an organisation.  An example maybe RFQ pricing.  Manually pricing an RFQ might be acceptable for a low throughput of requests, but as the request rate rises, the hiring of sales people all at some point no scale, coupled with the head count cost, and the possible human mis-keying issues.  Thus at some point RFQ’s need to be automated.  Although automation of the RFQ fixes one problem, unless an understanding of how the trade flows through post-trade, correlated with the steps that a support team had to undertake manually , and the latency implications of the flow depending on volume, it would be hard to identify what areas should have budget allocated to improve processing, or reduce/remote manual interaction.  Big data processing of the trade cycle could provide insight to the business to direct development budget

# Helping Salesperson Improve the Client Experience

Salespeople want clients to increase their trading frequency and volume – obviously.  Salespeople can help to increase a clients trading by understanding the client better, and thus providing the client with better direction and opportunity.  If you think about a clients interaction from a trading perspective, its either via voice, or through an electronic trading platform.  Further, there is client pre-trading interaction based on what a client readings that influences the clients decision process.

If the sell-side organisation could bring together everything about all clients, from their past trading activity, what research and trade ideas the client has read, married to the voice discussions had with the bank, it should be possible to begin to better understand the client, direct the client down paths that the client hadn’t possibly considered e.g. trading new products because of the type of reading material they had read over the last month, or improving the pricing to entice the client to accept an RFQ rather than consistently see the client reject an RFQ or allow it to time out, even though the client had attempted to trade consistently over the last n hours/days/weeks.

This brings us to the concept of a sales persons insight dashboard.  Such a dashboard would deliver alerts in real-time to direct sales in how to interact with the client – either through suggested reading maternal, telephone calls to interact and better understand the client, or simply to tune the electronic trading application (think Single Bank Platform (SBP)) in real-time enhance the users experience with the sell-side, delivering a stickier connection.

Apache Spark, Databricks and other such platforms can aid in delivering the big data components to empower your existing application.  Specifically by delivering a stream of data that leverages machine learning capabilities

# Transactional Cost [Analysis](http://www.wallstreetandtech.com/trading-technology/real-time-tca-for-decision-support-and-transparency/a/d-id/1297743) (TCA)

ITG has recently disclosed the work its doing around TCA and big data.  Equities offers the ability to aggregate centralised quote data feeds or actionable quote feeds which can form the basis of TCA and offering insight around trading costs.   Equiduct MarketViewer is one such visualisation from an equities perspective that offers TCA features though data aggregation.

In the case of FX and institutional orders ITG has leveraged dealers and new electronic communications networks to aid in constructing an order book, which I suspect would offer a similar view to the Equiduct MarketViewer.  Leveraging both historical and real-time data ingestion, big data should be able to deliver appropriate answer to questions of where an order should be submitted, and the cost implications – pre-trade analysis.

All of the above lead to a need to identify the data sources within an organisation, which then leads to a question of data quality prior to ingestion into the big data plant.  Identification is probably the easier of the two.  Data quality may mean that legal applications need to be improved to resolve data generation issues, or pre-processing of data to validate quality needs to occur before ingestion. There is also the issues of data holes, some of which might be able to be filled in inferring, whilst other holes may just need to be filled using classic software engineering.

~ by mdavey on August 4, 2014.

Posted in [Data](https://mdavey.wordpress.com/category/data/)