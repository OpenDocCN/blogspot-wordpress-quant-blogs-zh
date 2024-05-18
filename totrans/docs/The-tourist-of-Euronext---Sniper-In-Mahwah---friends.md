<!--yml
category: 未分类
date: 2024-05-18 14:13:08
-->

# The tourist of Euronext – Sniper In Mahwah & friends

> 来源：[https://sniperinmahwah.wordpress.com/2015/12/10/the-tourist-of-euronext/#0001-01-01](https://sniperinmahwah.wordpress.com/2015/12/10/the-tourist-of-euronext/#0001-01-01)

For once, something is happening in France about high-frequency trading (HFT). The French market regulator Autorité des Marchés Financiers (AMF) recently fined both a trading firm, Virtu, and an exchange, Euronext. The full report/sanction published by the AMF, in French, is [here](http://www.amf-france.org/Sanctions-et-transactions/Decisions-de-la-commission/Chronologique/Liste-Chronologique/Sanction.html?year=2015&docId=workspace%3A%2F%2FSpacesStore%2F079a99f9-ae7d-4786-ad5a-ef55ad788145). Here is a very quick summary of the case, with a few numbers.

###### **CONTEXT**

Madison Tyler Europe (MTE) was created on April 2008 as a subsidiary of New-York based Madison Tyler Holdings LLC,  who merged with Virtu Financial in 2011\. In 2009, Madison Tyler Europe had offices in London and a dozen of employees were working for the proprietary trading division of the firm. Back in June 2008, MTE became a member of Euronext, and in January 2009 MTE started to colocate their servers close to the Euronext matching engine in Aubervilliers, in the suburbs of Paris (later, in 2010, Euronext moved to Basildon, England, where the exchange had built a new data centre).

According to the AMF, Euronext did not initially charge firms who sent orders to the exchange but given the new electronic (“HFT”) ecosystem, the Euronext platform was not able to manage the flow of orders anymore and decided to set a daily order-to-trade ratio (OTR) for each member (and penalties were imposed for each new order). AMF says that the Euronext OTR was 10(orders)/1(transaction) in January 2008, changed to 100/1 in March 2009 (the ratio remained unchanged thereafter). Euronext had a special program for the firms who “provided liquidity” in less liquid stocks (in return, the market makers received rebates on fees) but in 2009 there was no such program proposed to the firms who trade the first 100 very liquid stocks (“Euronext 100”).

###### **INVESTIGATION**

In 2010, the AMF started an investigation on the supposed “layering” activities of MTE (layering  is considered as a manipulative scheme when a firm sends orders to an exchange but cancel those orders as if they had never been intended to be executed). Given the huge volume of data involved, the AMF investigated MTE activities on 27 different (and liquid) stocks only (mostly French companies like France Telecom, Peugeot, EDF and even a bank, Crédit Agricole); and given the impossible synchronization of data coming from other exchanges where MTE traded the same stocks (BATS, Chi-X, Nasdaq Europe and Turquoise), the investigation focused on 32 trading days, from July 21 to September 2, 2009 (particular attention was paid on one day, August 28, and on one stock, EDF).

###### FINDINGS

First, that’s interesting to read in the report that MTE received message acknowledgements (transaction/cancelation confirmations, etc.) ± 5 millisecond before these messages were sent to the other members of Euronext; such a policy, allowing a firm to “see the market” before other participants, has been much debated by market microstructure specialists and some exchanges don’t have the same policy – on Eurex, as far as I know, messages are sent to all the participants *at the same time*. That’s important to note because, according to the AMF, between July and September 2009, 5 000 000 orders sent by MTE on Euronext were canceled/modified in less than 2 milliseconds, meaning that when other members received the messages, those orders had already disappeared.

The AMF mainly focused on a MTE algorithm named “Soap” (two other similar algos, “Tourist” and “Schwamm” [“Sponge” in German], were also involved). In short, Soap 1) detected the best price for a stock on *one* of the five exchanges (Euronext, BATS, Chi-X, Turquoise or Nasdaq Europe) 2) sent passive orders to the *four* other platforms, 3) checked if one of these four orders were executed, 4) if so, then Soap canceled orders on the other platforms; 5) Go to 1). On average orders were for ± 100-400 shares; 80 percent of trades were executed in less than 1 second (66 percent in less than 10 milliseconds); and MTE made money on 90% of trades.

Besides, the special investigation on August 28, 2009 (on EDF stocks) showed that
– MTE sent 576 237 messages to the five exchanges (206 133 to Euronext)
– 1 506 orders were filled (605 on Euronext)
– the order-to-trade ratio was 341/1 on Euronext, 2 358/1 on BATS, 120/1 on Chi-X, 495/1 on Turquoise and 1 249/1 on Nasdaq Europe
– MTE accounted for 81% of messages on Euronext but 2,8% of volume; 93,6% of the messages on BATS (17,6% of volume); 58% of the messages on Turquoise (11,2% of volume) 

######  **FINES**

In short, Euronext is fined because the exchange allowed MTE to have an order-to-trade ratio greater than 100/1 without mentioning that *in a clear and intelligible manner* to the other participants (even if the AMF concedes that three other Euronext members, not named, also had an OTR greater than 100/1). During the 32 days analyzed by the AMF, the MTE order-to-trade ratio was 253/1 (MTE contested the ratio and says the OTR was 146/1), compared to 11,7/1 on average for the other members. The AMF estimates the non-public exemption granted  by Euronext to MTE resulted in a €19M loss for the exchange (the amount of penalties MTE should have paid given their OTR). The AMF fined Euronext €5M because the exchange did not respect “*its duty of neutrality and impartiality*”.

MTE (now Virtu) is also fined €5M for “*market manipulation*” – the AMF estimated MTE profit during the 32 days, thanks to Soap, Tourist and Schwamm, was €782 000. Virtu responded the algos were doing “*arbitrage*” between different exchanges (“*the arbitrageur buys under-evaluated stocks on a platform and sells them where the stocks are over-evaluated*”) and argued this “*transfer of liquidity*” allowed other participants to save €2,5M. But the AMF does not agree. Given that a lot of trading firms (market makers or not) use the same kind of algorithms, I’m just wondering how the AMF will manage the supposedly “layering” manipulations. Both Virtu and Euronext are appealing the AMF decision. The case will continue for years. Let’s hope it will help to understand more how market making works.