<!--yml
category: 未分类
date: 2024-05-18 06:38:01
-->

# Some Questions for Crypto-Exchanges | Mechanical Markets

> 来源：[https://mechanicalmarkets.wordpress.com/2017/12/07/compliance-questions-for-crypto-exchanges/#0001-01-01](https://mechanicalmarkets.wordpress.com/2017/12/07/compliance-questions-for-crypto-exchanges/#0001-01-01)

**1.** Does your exchange engage in proprietary trading? [[1](#bottom1btcexch)]

**A)** If so, what is the nature of the prop-trading? Does it occur on your own exchange, other exchanges, or both?
**B)** Are there information barriers between client data and prop-trading decisions? Are customers ever front-run?
**C)** Does prop-trading have the same access to the exchange as other customers?
**D)** Are exchange operational decisions, like pausing (or not pausing) matching due to IT issues, ever influenced by profit or loss by your prop-trading?
**E)** Who oversees exchange prop-trading and ensures it is non-manipulative? Is oversight segregated from the rest of exchange operations?

**2.** Does your exchange offer securities trading functionality?

**A)** If so, is the exchange registered and approved by the appropriate regulators? For example, if the exchange is in the US and matches Ether (likely a security in the US [[2](#bottom2btcexch)]), is it registered as an ATS, National Securities Exchange, OTC market, Broker-Dealer, or otherwise?
**B)** Are the securities classified as penny stocks, NMS stocks, Regulation A stocks, or another type of stock?
**C)** What standards determine the securities that the exchange matches?
**D)** Does margin trading of securities comply with applicable regulation? [[3](#bottom3btcexch)]
**E)** Does the exchange report suspected insider trading to the appropriate regulators? Are exchange [employees](https://www.cryptocoinsnews.com/traders-accused-insider-trading-zcash-price-surges-bithumb-integration/) monitored to prevent them from insider trading?

**3.** For exchanges offering execution services such as Coinbase, how is the execution price determined?

**A)** Is the customer executed at the worst price over a lookback period? What is the lookback period, and can it vary?
**B)** Do you reject orders via last look? Is it symmetric? Does it comply with market norms? [[4](#bottom4btcexch)]
**C)** Are details like the above, and any additional spreads, fully disclosed to customers?
**D)** If you offer execution services for securities such as Ether, do they comply with best-execution requirements? Are you registered as a broker? Do your retail customers understand any risks of using your services?

**4.** Do clients have equal access to the exchange?

**A)** Can every client access the same market data feeds and order entry gateways? At similar latencies?
**B)** Do any clients receive different fees than the public fee schedule?
**C)** When the exchange has IT issues, do any clients get preferential access? E.g., when the exchange is offline for some clients, does it ever make efforts to stay online for favored clients?
**D)** What safeguards are in place to ensure client information isn’t leaked to other clients?
**E)** If there is a margin deficiency, theft, or other shortfall, how are losses distributed and who oversees the process?

**5.** What mechanisms are in place to prevent and police manipulation?

**A)** Such as: momentum ignition, denial-of-service attacks, triggering margin liquidations, collusion, spoofing, and settlement-price/benchmark manipulation.
**B)** Are margin levels set such that manipulative traders or hackers (outside developed market jurisdictions) can’t force liquidations?
**C)** What are the penalties and enforcement mechanisms? Are instances of manipulation disclosed to clients?
**D)** If the exchange lists derivatives that depend on other exchanges’ pricing, do you communicate with those exchanges about potential manipulation and their own prop-trading? Do you have confidence in their capacity to give you reliable and complete information? [[5](#bottom5btcexch)]

**6.** Does the exchange disclose and investigate security breaches?

**A)** E.g. if the exchange suffers a suspected DOS attack, when and how is that disclosed to customers?

**7.** Does the exchange guarantee that its customers are not buying stolen or laundered coins? If stolen coins were bought on the exchange by an innocent customer, and [reclaimed](https://mechanicalmarkets.wordpress.com/2017/11/05/bitcoin-nemo-dat/), will the customer be compensated?

[[1](#1btcexch)] It is somewhat reassuring that the [Administrator](http://www.cmegroup.com/education/bitcoin-pricing-products-practice-standards.html) of the CME’s Bitcoin settlement price, Crypto Facilities, says it does not engage in (at least some forms of) proprietary trading. In an [interview](http://www.bitcoinfuturesguide.com/bitcoin-blog/qa-with-dr-timo-schlaefer-ceo-of-crypto-facilities-up-and-coming-bitcoin-futures-exchange) with Bitcoin Futures Guide, the CEO said:

> It [the Turbo 50x leverage product] also does not change the risk profile of Crypto Facilities as we are not a counterparty in the trades on our platform.

[[2](#2btcexch)] The [SEC](https://www.sec.gov/litigation/investreport/34-81207.pdf) “has determined that DAO Tokens are securities under the Securities Act of 1933.” You can read Ether’s [offering documents](https://github.com/ethereum/www/tree/master-postsale/src/extras/pdfs) and come to your own conclusions. 

[[3](#3btcexch)] I believe Kraken [allows](https://support.kraken.com/hc/en-us/articles/227876608-Which-currency-pairs-can-I-trade-on-margin-) margin trading for retail customers of Ether and [Tether](https://www.bloomberg.com/news/articles/2017-12-05/mystery-shrouds-tether-and-its-links-to-biggest-bitcoin-exchange) at levels of [up to 5x](https://support.kraken.com/hc/en-us/articles/205605288-What-levels-of-leverage-are-offered-).

[[4](#4btcexch)] I have heard anecdotally that, when the price moves in the customer’s favor, Coinbase may reject executions with error messages like “the exchange rate updated while you were waiting” — but may not always do such rejections when the price moves against the customer.

[[5](#5btcexch)] The CME’s settlement price mechanism may be modified in “[unusual and extreme circumstances](http://www.cmegroup.com/education/bitcoin-pricing-products-practice-standards.html#8-unusual-and-extreme-circumstances).” The Administrator (Crypto Facilities) is responsible for making recommendations in such circumstances, and requires the approval of the CF Member of the [Oversight Committee](http://www.cmegroup.com/trading/cf-bitcoin-reference-rate.html) (who I think is currently the CEO of Crypto Facilities), and one of the CME’s representatives on the committee.

In the Bitcoin market, I’m not sure how unusual “unusual and extreme circumstances” are.