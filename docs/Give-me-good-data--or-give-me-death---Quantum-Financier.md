<!--yml

类别：未分类

日期：2024 年 05 月 18 日 14:00:08

-->

# 给我好的数据，或者让我死去 – 量化金融家

> 来源：[`quantumfinancier.wordpress.com/2016/01/10/give-me-good-data-or-give-me-death/#0001-01-01`](https://quantumfinancier.wordpress.com/2016/01/10/give-me-good-data-or-give-me-death/#0001-01-01)

基于快速而粗糙的分析，HDF 似乎表现更好。读取性能对我来说更重要，因为数据只需要写入一次，但肯定会被读取多次。请注意，我并不打算把这个测试描绘成最终的讨论证据。而只是看看有什么选择，并评估它们的相对性能。基于我初步的结果，包括但不限于此分析，我选择使用 HDF 格式存储数据，因为它符合我的所有要求，并且对于中等规模数据来说看起来相当快。这也应该使得 R 同伴们可以通过出色的 rhdf5 库来使用它。

到这个时候，我已经决定了一个格式。剩下要回答的问题是如何组织它。我在想类似于这样的东西：

```
/data
|-- Equities
    |-- Stock (e.g. SPY, AAPL etc.)
        |-- Metadata
|-- Forex
    |-- Cross (e.g. USDCAD, USDJPY etc.)
        |-- Metadata
        |-- Aggregated data
        |-- Exchanges (e.g. IdealPRO etc.)
|-- Futures
    |-- Exchange (e.g. CME, ICE, etc.)
        |-- Contract (e.g. ES, CL etc.)
            |-- Metadata
            |-- Continuously rolled contract
            |-- Expiry (e.g. F6, G6, H6 etc.)
```

对于如何最好地做这一点，我个人也不太确定。对我来说，设计一个干净的多态 API 来访问这样的结构化数据似乎相当困难，但我似乎找不到更好的方法。

我想听听读者是如何解决这些问题的。除了如何存储和组织数据之外，我非常想知道你们如何处理自动创建永久合同，而不必手动编写每种产品的规则。对我来说，这已经被证明是一项棘手的任务，因为我在分析中经常使用这些合同，我正在寻找一个好的解决方案。

希望这个讨论会引起那些在内部管理他们自己数据的读者的兴趣。
