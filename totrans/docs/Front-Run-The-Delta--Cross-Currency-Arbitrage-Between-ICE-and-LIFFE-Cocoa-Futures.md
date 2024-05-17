<!--yml
category: 未分类
date: 2024-05-12 23:33:40
-->

# Front-Run The Delta: Cross-Currency Arbitrage Between ICE and LIFFE Cocoa Futures

> 来源：[https://frontrunthedelta.blogspot.com/2011/09/cross-currency-arbitrage-between-ice.html#0001-01-01](https://frontrunthedelta.blogspot.com/2011/09/cross-currency-arbitrage-between-ice.html#0001-01-01)

This is the spread built utilizing three futures contracts and one cash transaction.  The base spread comes from the ICE-listed Cocoa contract (

[CC](https://www.theice.com/publicdocs/ICE_Cocoa_Brochure.pdf)

) [pdf] and the LIFFE-listed Cocoa contract (

[C](http://www.euronext.com/trader/contractspecifications/derivative/wide/contractspecifications-2864-EN.html?euronextCode=C-LON-FUT)

).  The contracts are for identical quantities and listed in USD and GBP, respectively.  The GBP/USD rate is the key to theoretical price discovery.  Prices were recorded August 26, 2011\.

From CC's prospectus, page 3:

> "Cocoa is unique among soft commodities in its relationship to currencies. Because of Britain’s historical domination of the [West African](http://www.maketradefair.com/assets/english/CocoaStudy.pdf) [pdf] cocoa industry and a British pound-denominated futures contract traded on the London International Financial Futures (LIFFE) exchange, cocoa’s currency correlation is stronger with the British pound (GBP) than with the ICE U.S. Dollar Index® (USDX®)..."

> "While the long-term relationship is shown, experienced traders see the effect intraday when the British pound has a large movement during the period when New York and London trading overlaps."

Implied & Real Prices. 

This structure utilizes both the

[interbank forex market](http://frontrunthedelta.blogspot.com/2011/06/triangular-arbitrage-using-usdhkd.html)

 (Cash) and the CME-listed

[GBP/USD futures](http://frontrunthedelta.blogspot.com/2011/07/etf-futures-arbitrage-fxb-and-gbp.html)

contract (

[6B](http://www.cmegroup.com/trading/fx/g10/british-pound_contract_specifications.html)

) (Fut) to capture the "large movements" of the Pound.  Because both cash and futures GBP are included in the study, two currency-adjusted values for the GBP-denominated C are shown here (above) with the USD-denominated CC contract.

The Spreads.

Because the

[ETF and Futures](http://frontrunthedelta.blogspot.com/2011/07/etf-futures-arbitrage-fxb-and-gbp.html)

markets mirror the

[cash](http://frontrunthedelta.blogspot.com/2011/06/triangular-arbitrage-using-usdhkd.html)

prices, there is very little deviation between the futures and cash spreads shown here (above).  The negative spread implies the GBP Cocoa contract currently trades at a premium to the USD Cocoa contract, as evidenced by the chart of the implied values.

The width of ICE's bid/ask spread relative to that of LIFFE's eliminates the potential for intraday entry and exit (at least with the volatility level of the period studied), and makes it counter productive and disadvantageous to trade.  This relationship is in the black book of

[macro](http://www.bloomberg.com/news/2011-08-26/brevan-howard-macro-fund-said-to-rise-6-amid-august-market-rout.html) [managers](http://www.armajarotrading.com/)

requiring longer holding times and more fundamental, regional supply/demand analysis.