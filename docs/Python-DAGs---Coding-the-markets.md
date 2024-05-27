<!--yml

category: 未分类

date: 2024-05-12 19:33:00

-->

# Python DAGs | 编码市场

> 来源：[`etrading.wordpress.com/2014/05/05/python-dags/#0001-01-01`](https://etrading.wordpress.com/2014/05/05/python-dags/#0001-01-01)

## Python DAGs

### May 5, 2014

[Tales flags](http://mdavey.wordpress.com/2014/04/30/the-python-angle/)在 Python 世界中的一些有趣的发展。金融领域对[Python 开发者](http://www.thepythonquants.com/ "Python 量化")的需求似乎确实在增长。Man 和 Getco 都是大用户，正如 Tales 所指出的，JP Morgan 和[BAML](https://www.bankofamerica.com/)都将 Python 作为其[Athena](http://techcareers.jpmorgan.com/cm/BlobServer/athena_jpmc.pdf "Athena")和[Quartz](http://thegatewayonline.com/technology/technology-at-a-bank/bank-of-america-merrill-lynch-become-part-of-the-quartz-community)系统中的主要编程语言，这两个系统都受到了高盛的[SecDB/Slang](http://www.businessinsider.com/former-goldmanite-this-might-get-me-sued-but-im-going-to-lift-the-veil-on-goldmans-trading-2010-8#!IKI63)的启发。Tales 想知道[Washington Square Tech](http://www.washingtonsquaretech.com/)是否将是这种范式的第四个实现；我相信它可能是第五个，因为[摩根士丹利](http://www.morganstanley.com)在[杰伊·德威克](https://www.quantnet.com/threads/jay-dweck-global-head-of-strats-and-tech-left-morgan-stanley.5397/)任职期间有一个类似 Athena 的项目，名为 Pioneer。显然，那个项目现在已经不存在了。Athena 范式从技术上讲是一种非常强大的解决方案，适用于一直使用 Excel 进行定价和风险的基于 ad hoc 解决方案的交易业务。部分原因是他们寻求取代基于 Excel 的定价和风险，部分原因是它具有计算效率，所有 Athena SecDB/Slang 范式的实现都实现了有向无环图。我猜测 Washington Square Tech 会认为这对于没有大型内部技术堆栈的买方公司来说可能非常有吸引力，同时现有技术团队捍卫他们免受替代。

[有向无环图](http://en.wikipedia.org/wiki/Directed_acyclic_graph)（DAGs）是一种强大的实现技术，用于最小化计算密集型任务（如定价和风险）的负载，这就是 Excel 在这个领域如此成功的一个好理由，正如 DataNitro 的[本·莱纳](http://howtowriteabusinessplan.com/2013/05/datanitro/)在其文章[中](https://datanitro.com/Python_Meetup_1_16_14.pdf)所 persuasively 解释的那样。因此，看到 Man Groups 拥有的[开源 Python 代码库](https://github.com/ahlmss)包括一个 DAG 实现，[MDF](https://github.com/ahlmss/mdf)，并不令人惊讶。MDF 文档包括一个很好地展示了 DAG 方法的强大性的插图。
