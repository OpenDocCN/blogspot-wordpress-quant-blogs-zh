<!--yml
category: 未分类
date: 2024-05-12 21:34:29
-->

# Falkenblog: How to Make BBB Securities AAA

> 来源：[http://falkenblog.blogspot.com/2010/04/how-to-make-bbb-securities-aaa.html#0001-01-01](http://falkenblog.blogspot.com/2010/04/how-to-make-bbb-securities-aaa.html#0001-01-01)

In today's

[senate hearing](http://www.marketwatch.com/story/fabulous-fabs-almost-fabulous-testimony-2010-04-27?dist=countdown)

, there was a question how a portfolio of BBB rated securities can generate a AAA rated security. Ex-Goldman exec Dan Sparks basically said it was due to diversification. This is an incomplete answer. Diversification alone is insufficient. You also need to add an equity tranche, a first-loss position that is breached only in specified probabilities. This is modeled based on historical loss rates for the rated collateral, and the minimum amount of equity needed to imply the Senior securities have expected loss rates consistent with AAA ratings (expected loss is the expected default rate times the loss in event of default). This is modeled using Monte Carlo methods because these structures have waterfalls where reserves build-up and are paid down, so they don't assume 'gaussian' distributions.

So, turning B rated bonds into AAA rated bonds, involves both diversification and equity. You can't turn $100 worth of BBB bonds into $100 worth of AAA bonds. You turn it into $95 worth of AAA bonds (or something, depending on the time horizon).

And this was all farked because the ratings on the collateral were wrong, but that's a separate issue.