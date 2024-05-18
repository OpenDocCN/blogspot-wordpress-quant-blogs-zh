<!--yml
category: 未分类
date: 2024-05-18 14:02:21
-->

# Basic Introduction to GARCH and EGARCH (part 3) – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2010/09/23/basic-introduction-to-garch-and-egarch-part-3/#0001-01-01](https://quantumfinancier.wordpress.com/2010/09/23/basic-introduction-to-garch-and-egarch-part-3/#0001-01-01)

Here is the final part of the series of posts on the volatility modelling where I will briefly talk about one of the many variant of the GARCH model: the exponential GARCH (abbreviated EGARCH). I chose this variant because it improves the GARCH model and better model some market mechanics.

In the GARCH post, I didn’t mention any of the limitation of the model as I kept them for today’s post. First of all, the GARCH model assume that only the magnitude of unanticipated excess returns determines ![\sigma^2_t](img/21fd744994e2f41e326d17da24f7f33a.png). Intuitively, we can question this assumption; I, for one, would argue that not only the magnitude but also the direction of the returns affects volatility. In plain English: negative shocks (events/news, etc.) tend to impact volatility more than positive shocks. Think about the asymmetric nature of the VIX (see [Bill Luby’s Vix and More](http://vixandmore.blogspot.com/)).

Another limitation that may concern the quant savvy investor is the persistence of volatility shock. How long does a shock linger in the volatility estimate? Some may persist for a finite period of time while other might linger *ad vidam, aeternam*; effectively changing the market volatility structure. In the GARCH (1,1) model, shocks can be persistent or not, which might be undesirable depending on the situation.

These two limitations are the mains drivers behind the EGARCH model which meets these objections. Without further ado here is the EGARCH formulation:

![log(\sigma_t^2) = \omega + \sum_{k=1}^{p} \beta_kg(Z_{t-k}) + \sum_{k=1}^{q} \alpha_k log \sigma_{t-k}^2](img/0badc89ccc58a655b1116b613bae1ab6.png)

and

![g(Z_t) = \theta Z_t + \lambda(|Z_t| - E(|Z_t|))](img/1ffeee7f876277cd951dde1e37e6d51d.png)

Where ![\omega, \beta, \alpha, \theta,](img/e51b7ea1a016b77f090ea97ae198ffc6.png) and ![\lambda](img/d0f09b12e316b3dd6e46b9398b808747.png) are coefficients, and ![Z_t](img/f0de939d8d82d2be19922f82106576c8.png) comes from a generalized error distribution.

Using this model, we can expect a better estimate the volatility for asset returns due to how the EGARCH counteracts the limitations on the classic GARCH model. In terms of implementation, as always, I recommend using statistical software to perform the analysis.

As a side note, I have to cite my sources for this post series since I mostly followed other academic papers, and I took some part textual, trying to only focus on what I thought was important for an introduction. Please refer to them if you want more information.

Nelson, D.B. (1991). Conditional heteroskedasticity in asset returns: a new approach. Econometrica,, 59(2), 347-370.

Engel, R. (2001). Garch 101: the use of arch/garch models in applied econometrics. Journal of Economic Perspectives, 15(4), 157-168.

QF