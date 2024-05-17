<!--yml
category: 未分类
date: 2024-05-18 00:44:44
-->

# Humble Student of the Markets: Why I am not a bottom-up equity quant

> 来源：[https://humblestudentofthemarkets.blogspot.com/2009/10/why-i-am-not-bottom-up-equity-quant.html#0001-01-01](https://humblestudentofthemarkets.blogspot.com/2009/10/why-i-am-not-bottom-up-equity-quant.html#0001-01-01)

I spent close to two decades of my career building bottom-up equity quantitative models to pick stocks, in Canadian, US and international markets. I was asked why I don’t do that anymore.

My flippant answer was:“Been there, done that.”

My longer answer was that the competitive advantage of doing bottom-up quantitative analysis is being eroded to such an extent that alphas are rapidly diminishing.

Let me explain. Back in the 1970s and 1980s, the task of performing equity quantitative analysis required a large commitment by an investment organization. Sure, there were databases around, but the task of integrating them was a non-trivial task that required investment in staff and infrastructure.

Here are some sample issues. How do you marry an earnings estimate database (e.g. IBES) with a fundamental database (e.g. Compustat) when:

*   The series have different periodicities (annual & quarterly for the fundamental and daily/weekly/monthly for earnings estimates)?
*   The identifier for earnings estimates is for the security (stock specific) but the fundamental database is identified by company (as multiple share classes are not uncommon for non-US companies)?

Add to that the issues of adding data for new listings, deletions, name changes, etc. The investment organization quickly finds itself not in the investment business, but the database maintenance business.

**Falling barriers to entry**
Fast forward a couple of decades, the apperance of system integrators like [Factset Research Systems](http://www.factset.com/) have revolutionized the business and dramatically lowered the barriers to entry to bottom-up equity quantitative analysis. Today, you can build an equity quantitative research capability by subscribing to these services.

**Opera singers don't belt, quants control for factor risk**
Moreover, a generation of quants has been [conditioned by the likes of Barra](http://humblestudentofthemarkets.blogspot.com/2008/04/have-we-quants-been-brainwashed-by.html) to decompose risk as industry plus a Fama-French like common factors such as Market Capitalization and Style (Value/Growth).

The implications of this analysis framework is that just as opera singers are genetically imprinted not to belt when they sing, bottom-up equity analysts are conditioned to believe that you shouldn’t try to forecast the returns to these risk factors. Instead, the appropriate way to forecast alpha is to forecast alpha based on residual risk, or stock pick after controlling for, at the very least, industry and sector risk.

The combination of lower entry barriers and groupthink has led equity quants into a crowded trade. They all uses some form of multi-factor stock selection model, but the data comes from the same databases. The factors all appear to be uncorrelated but we saw [what happened in August 2007](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1288988).

**The low lying fruit is gone**
Even when you succeed, it’s a really tough business.

I recently attended a seminar put on by a risk model vendor and a respected equity quant manager. The equity manager put up an analysis showing various ways of integrating their forecast alphas with the risk models that they use. The most optimal technique for a long only portfolio, with a 2-2.5% forecast tracking error, resulted in an annual alpha of about 1.5% a year.

1.5% sounds pretty good.

However, you have to consider that this is a forecast alpha from a model portfolio with no turnover costs. Once you throw in trading costs, the shortfall between the turnover of the forecast alpha and the actual portfolio, which could vary greatly, and even the fact that good managers with tight investment processes experience portfolio dispersion (difference in returns between accounts with similar mandates) of 2% or more, 1.5% doesn’t sound that good.

As I said before, it’s getting to be a really tough business.

So far my solution has been to do something that is truly queasy and nauseating to many equity quants. I have been using top-down investing and factor rotational approaches to quantitative investing. The approach disturbs quants because it's less disciplined, less risk controlled (according to the way they are trained) and appears to be so, well, ***empircally*** oriented.

My approach is not the only answer but bottom-up equity quants need to find new sources of alpha.