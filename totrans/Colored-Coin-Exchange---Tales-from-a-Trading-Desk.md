<!--yml
category: 未分类
date: 2024-05-18 05:39:34
-->

# Colored Coin Exchange | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/09/20/colored-coin-exchange/#0001-01-01](https://mdavey.wordpress.com/2015/09/20/colored-coin-exchange/#0001-01-01)

## Colored Coin Exchange

Lykke appears to be taking a different blockchain path to [startup](https://bitcoinmagazine.com/articles/blythe-masters-wall-street-opt-permissioned-non-bitcoin-blockchains-1441227797) Digital Asset Holdings – Lykke is going for [colored](http://coloredcoins.org/) coins, and the public blockchain that exists today.  Lykke has a nice [white](https://wiki.lykkex.com/colored_coin_exchange_white_paper) paper on its reasoning for colored coins, and presents a high level [architecture](https://wiki.lykkex.com/colored_coin_exchange_software_architecture) highlighting the exchange usage:

> Traders create an order by creating and signing a transaction to send x coins to the exchange, whereas x is the amount and type of coins they intend to sell. Unlike usual transactions, this transaction is not sent to the Bitcoin network, but to the exchange instead, along with additional information about the order (type, asset to buy, limit, etc.). As soon as the exchange receives a matching order containing a second transaction, the exchange creates a third transaction that sends the exchanged amounts to the two traders. These three transactions together form a trade and are sent to the Bitcoin network for execution. The third transaction is also sent to the two traders, so they can immediately reuse the proceeds for subsequent transactions. Unfilled or cancelled orders are simply discarded.

In some ways the exchange is similar to the Ripple [Gateways](https://ripple.com/trade/ripple-for-market-makers/).

~ by mdavey on September 20, 2015.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [blockchain](https://mdavey.wordpress.com/tag/blockchain/)