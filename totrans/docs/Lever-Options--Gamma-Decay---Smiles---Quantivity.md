<!--yml
category: 未分类
date: 2024-05-18 13:55:41
-->

# Lever Options: Gamma Decay & Smiles | Quantivity

> 来源：[https://quantivity.wordpress.com/2009/08/11/lever-options-gamma-decay/#0001-01-01](https://quantivity.wordpress.com/2009/08/11/lever-options-gamma-decay/#0001-01-01)

Levered ETFs are fascinating financial instruments. Derivatives on levered ETFs, termed *lever options* here (or, *levers* for shorthand), are even more interesting. As lever options are likely to be the first [exotic](http://en.wikipedia.org/wiki/Exotic_option) to gain substantial exchange-traded volume, volatility traders should be salivating!

One of the most interesting aspects of levers is *gamma decay* (liberally inventing terminology, borrowing from the classic [greek](http://en.wikipedia.org/wiki/Greeks_(finance)) gamma):

> Gamma decay is the decay in option value due to the leverage decay of the underlying levered instrument.

In other words, leverage decay in the underlying results in a direct effect on the derivative captured by gamma decay. Gamma decay is a non-trivial departure from the standard [BSM](http://en.wikipedia.org/wiki/Black%E2%80%93Scholes) assumption of a [Weiner process](http://en.wikipedia.org/wiki/Wiener_process) underlying. Note gamma decay differs, although is similarly derived, from the linear scaling of the drift and volatility.

Most fundamentally, gamma decay should cause pause to evaluate the classic BSM gamma-theta tradeoff, now that both gamma and theta decay: ![(\frac{1}{2} \sigma^2S^2\Gamma + \theta)](img/7516945d09d848b80cd5f15b9d9c0fb7.png).

Quick scan of the smiles for August expiry [SSO](http://finance.yahoo.com/q?s=SSO) and [UPRO](http://finance.yahoo.com/q?s=UPRO) indicate [MMs](http://en.wikipedia.org/wiki/Market_maker) may still be pricing using classic BSM. Multi-order polynomial smile for SSO (fitted in blue, unfitted in gray), assuming 1.24% cont yield and 0% risk-free:

![sso-vol-surface-expiry-aug-2009](img/1efbbd765f520ed6f07a5239725d7215.png "sso-vol-surface-expiry-aug-2009")

Similar smile for UPRO, assuming 0% cont yield and risk-free:

![upro-vol-surface-expiry-aug-2009](img/4d7676fe850411b17b981858f5fdd82d.png "upro-vol-surface-expiry-aug-2009")

Subsequent posts will continue analysis of levers given they are such a rich vein.