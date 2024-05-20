<!--yml
category: 未分类
date: 2024-05-18 14:00:08
-->

# Give me good data, or give me death – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2016/01/10/give-me-good-data-or-give-me-death/#0001-01-01](https://quantumfinancier.wordpress.com/2016/01/10/give-me-good-data-or-give-me-death/#0001-01-01)

Based on that quick and dirty analysis HDF seems to do better. Read performance is much more important to me as the data should only be written once but will definitely be read more than that. Please not that I did not intend portray this test a end-all discussion proof. But simply to look at what the options were and to evaluate their relative performance.Based on my preliminary results including but not limited to this analysis, I elected to store the data using the HDF format as it meets all my requirements and looks to be fairly fast, at least for medium size data. It should also enable the R homies to use it through the excellent rhdf5 library.

So at this point I have decided on a format. The question that remains to be answered is how to organize it. I was thinking of something like this:

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

Personally not too sure how to best do this. It would seem to me that it would be rather difficult to design a clean polymorphic API to access the data with such a structure but I can’t seem to find a better way.

I would like to hear what readers have come up with to address those problems. In addition to how you store and organize your data, I am very keen to hear how you would handle automating the creation of perpetual contracts without having to manually write a rule for the roll of each product. This has proven to be a tricky task for me and since I use those contracts a lot in my analysis I am looking for a good solution.

Hopefully this discussion will be of interest to readers that manage their own data in-house.