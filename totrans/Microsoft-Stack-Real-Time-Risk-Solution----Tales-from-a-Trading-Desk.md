<!--yml
category: 未分类
date: 2024-05-18 06:19:10
-->

# Microsoft Stack Real-Time Risk Solution? | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2009/11/29/microsoft-stack-real-time-risk-solution/#0001-01-01](https://mdavey.wordpress.com/2009/11/29/microsoft-stack-real-time-risk-solution/#0001-01-01)

## Microsoft Stack Real-Time Risk Solution?

There appears to be a lot of opportunity in the real-time risk space. For a company like Microsoft who would probably like a large share of the financial vertical pie, it’s unclear if they understand the problem or have a solution. If you look at the various real-time risk product companies I’ve blogged about recently, there are numerous contenders who may or may not be used in the solutions banks are building or will build over the coming year or so. Unfortunately I don’t think this is a clear winner as yet in this product space, there doesn’t seem to be a single product that solves 80% of the problem.

If we look at the problem space, what we do know is that we need to handle a lot of moving data (trades, market, etc), we need to cook curves, calculate risk on trades/positions in real-time, and finally we need to present this data appropriately, and allow drill-down and analysis of the data – [P&L attribution](http://pnlexplained.com/PEP_PnL_Explained_FAQ.html).

So now we turn to Microsoft, and what it can provide to solve this problem. Today it has [Analysis services](http://www.microsoft.com/sqlserver/2005/en/us/Analysis-Services.aspx), which offers OLAP but isn’t a vector database, and I suspect it’s not real-time enough for the desk 😦 However, I suspect there is part of a solution if your prepared to try a bit of a Proof Of Concept (POC): Take StreamInsight, connect to HPC possibly using [Dryad](http://blogs.technet.com/windowshpc/archive/2009/07/15/dryad-and-dryadlinq-on-hpc-server.aspx), stir in Windows Server AppFabric caching for trades/risk data and possible consider building an [in-memory](http://it.toolbox.com/blogs/crm-realms/inmemory-olap-vs-traditional-olap-27467) cube off this distributed data set presented though a Silverlight/WPF application – essentially [StreamCube](http://www.panopticon.com/products/streamcube_olap_data_visualization.htm) over AppFabric Caching.

Torsten’s PDC 2009 session provides some insight into how you might use StreamInsight in a Real-Time Risk (RTR) architecture. Although his Market Mover demo is not aggregating risk, it does show how with a multi-layer StreamInsight architecture you can use – 41mins into the session. I suspect you want to feed a SQL Server 2008 Analysis Services (OLAP) database as well for MDX ad-hoc queries in the green coloured StreamInsight servers, with the 3rd tier handling client application requests to push RTR data based on dynamic queries. 46mins into the session I think provides a good RTR viewpoint.

~ by mdavey on November 29, 2009.

Posted in [Trading](https://mdavey.wordpress.com/category/trading/)
Tags: [Microsoft](https://mdavey.wordpress.com/tag/microsoft/)