<!--yml
category: 未分类
date: 2024-05-18 05:23:04
-->

# Magmasystems Blog: Index and Bespoken Tranches

> 来源：[http://magmasystems.blogspot.com/2005/11/index-and-bespoken-tranches.html#0001-01-01](http://magmasystems.blogspot.com/2005/11/index-and-bespoken-tranches.html#0001-01-01)

In the credit derivatives trading system we are building, we need to add support for various structured products. Two of the products are index and bespoken tranches. Other instruments that we will eventually have to implement are NTDs, CDOs, and CDO

2.

We all know what a Credit Default Swap (CDS) is, right? It's a form of insurance that someone takes out on a company. One party (the buyer of the insurance) pays a periodic premium to a counterparty (seller of the insurance) for insurance on an underlying instrument (bond or other credit instrument). If there is a "credit event" on the underlying (ie: a company goes bust, misses an interest payment, or the CEO runs away to Bermuda with his secretary), the seller of the insurance must pay the buyer a certain sum of money, known as the "recovery rate". The CDS has some parameters, such as the

**seniority**

(who is first in line to get paid in case the company goes belly up), the

**tenor**

(how long the buyer has to pay the premiums for), and the

**notional**

(the value of the underlying instrument).

There are Indexes on CDS's. We can create our own index, such as the bonds of all of the American auto manufacturers. Or, we can use an exchange-manufactured index.

CDS indices are so popular that there is a

[CDS index](http://djindexes.com/mdsidx/index.cfm?event=cdx)

on the Dow. The most widely-traded CDS index is the one for

[North American Investment Grade](http://finance.yahoo.com/q?s=%5EDJCDXNI)

instruments. It accounts for over 80% of the CDX volume that is traded.

So, now we know what a CDS Index is. On to Tranches....

A

**Tranche**

is a certain level of risk. According to Investopedia:

*Tranche is a term often used to describe a specific class of* [*bonds*](http://www.investopedia.com/terms/t/tranches.asp#) *within an offering wherein each tranche offers varying degrees of risk to the* [*investor*](http://www.investopedia.com/terms/t/tranches.asp#)*. For example, a CMO offering a partitioned MBS portfolio might have mortgages (tranches) that have one-year, two- year, five-year and 20-year maturities.*

For the above-mentioned index, there are 5 tranches. The

***Equity***

tranche covers the first 3% of losses on the credit instruments. The

***Mezzanine***

tranche covers from 3-7%. The two

***Senior***

tranches cover 7-10% and 10-15% respectively. The

***Super Senior***

tranche covers the last 15-30% of losses.

**Index Tranches**

are for active traders. A

**Bespoken Tranche**

is one that is put together on the wishes of an investor. It is usually created for long-term investment.

©2005 Marc Adler - All Rights Reserved