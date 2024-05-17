<!--yml
category: 未分类
date: 2024-05-12 19:33:00
-->

# Python DAGs | Coding the markets

> 来源：[https://etrading.wordpress.com/2014/05/05/python-dags/#0001-01-01](https://etrading.wordpress.com/2014/05/05/python-dags/#0001-01-01)

## Python DAGs

### May 5, 2014

[Tales flags](http://mdavey.wordpress.com/2014/04/30/the-python-angle/) some interesting developments in the [Python](www.python.org) world. The demand for [Python developers in finance](http://www.thepythonquants.com/ "Python quants") does seem to be building. Both [Man](http://www.man.com) and [Getco](http://en.wikipedia.org/wiki/Global_Electronic_Trading_Company) are big users, and as Tales points out, [JP Morgan](www.jpmorgan.com) and [BAML](https://www.bankofamerica.com/) both use Python as the primary programming languages in their [Athena](http://techcareers.jpmorgan.com/cm/BlobServer/athena_jpmc.pdf "Athena") and [Quartz](http://thegatewayonline.com/technology/technology-at-a-bank/bank-of-america-merrill-lynch-become-part-of-the-quartz-community) systems, both of which are inspired by Goldman’s [SecDB/Slang](http://www.businessinsider.com/former-goldmanite-this-might-get-me-sued-but-im-going-to-lift-the-veil-on-goldmans-trading-2010-8#!IKI63). Tales wonders if [Washington Square Tech](http://www.washingtonsquaretech.com/) will the fourth implementation of this paradigm; I believe it may be the fifth, as [Morgan Stanley](http://www.morganstanley.com) had an Athena like project called Pioneer during [Jay Dweck’s ill fated tenure](https://www.quantnet.com/threads/jay-dweck-global-head-of-strats-and-tech-left-morgan-stanley.5397/). Apparently that project is now defunct. The Athena paradigm is technically a very powerful solution for trading businesses that have run on ad hoc solutions using Excel for pricing and risk. Partly because they seek to replace Excel based pricing and risk, and partly because it’s compute efficient, all implementations of the Athena SecDB/Slang paradigm implement Directed Acyclic Graphs. I’m guessing that Washington Square Tech will think this could be very appealing for buy side firms that don’t have big in house tech stacks, together with incumbent tech teams defending them against replacements.

[Directed Acyclic Graphs](http://en.wikipedia.org/wiki/Directed_acyclic_graph) (DAGs) are a powerful implementation technique for minimising the load of compute intensive tasks like pricing and risk, and this is one good reason why Excel has been so successful in this area, as [Ben Lerner of DataNitro](http://howtowriteabusinessplan.com/2013/05/datanitro/) [explains persuasively here](https://datanitro.com/Python_Meetup_1_16_14.pdf). So it should be no surprise to see that Man Groups own [open source Python codebases](https://github.com/ahlmss) include a DAG implementation, [MDF](https://github.com/ahlmss/mdf). The MDF docs include a very good illustration of the power of the DAG approach.