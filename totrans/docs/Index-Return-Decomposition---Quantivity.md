<!--yml
category: 未分类
date: 2024-05-18 13:46:43
-->

# Index Return Decomposition | Quantivity

> 来源：[https://quantivity.wordpress.com/2011/12/14/index-return-decomposition/#0001-01-01](https://quantivity.wordpress.com/2011/12/14/index-return-decomposition/#0001-01-01)

Unmasking a phenomenon ![f](img/f6f5c905b764a946a65bee80b6736fe6.png) into its constituent parts ![\textbf{g}](img/dd36de08983666821bd2eac7513fb63a.png), via *functional decomposition* ![\phi](img/2091dd12efe62f5560f0e90f96ef4889.png), is one of the great beauties of mathematics:

   ![f(\textbf{x}) = \phi(g_1(\textbf{x}), g_2(\textbf{x}), \dots, g_n(\textbf{x})) ](img/937ce0003616227e8e5a15e180ae901a.png)

This technique finds surprisingly often use in quant models.

Ongoing analysis and trading based on proxy hedging, exemplified by series beginning with [Proxy / Cross Hedging](https://quantivity.wordpress.com/2011/10/02/proxy-cross-hedging/), suggests potential for an equity decomposition model based on the relationship between returns of a stock ![r_t](img/81847f8e748a72d127acffb74b21e309.png) and its corresponding index ![i_t](img/d1ba04e50950b99d9eabd6f208278285.png):

   ![r_t = s_t \left[ \alpha_t | z_t | + (1 - \alpha_t) \beta | i_t | \right] + \epsilon_t ](img/031d799b8df5320f04bc3fef04370113.png)

To explain this model, let’s build it up from intuition.

To begin, consider a trading observation: interday returns of individual stocks have a subtle relationship with their corresponding index. On some days, return for a given stock follows its index; other days, returns of stock and index diverge strongly. This distinction in behavior is commonly attributed to stock-specific “news”, interpreted broadly—whether known publicly or only privately.

This intuition can be formalized into two-state regime:

*   **Uninformed regime**: stock return ![r_t](img/81847f8e748a72d127acffb74b21e309.png) follows an index ![i_t](img/d1ba04e50950b99d9eabd6f208278285.png), scaled by a proportional factor ![\beta](img/e59dd600f7eb22f952e355797bceba2e.png)
*   **Informed regime**: stock return ![r_t](img/81847f8e748a72d127acffb74b21e309.png) follows an idiosyncratic path ![z_t](img/74d890ac7e079882a239837ea3afdf8c.png), conditionally independent of its index

Relationship between regimes can be modeled in two ways via ![\alpha](img/9a53e012ad26523af8c1a6778d340c3f.png). A switching model arises when regimes are binary: ![\alpha \in \{ 0, 1 \}](img/d4b72d2b7819d4db2110c87f652f0556.png). An ensemble model arises when regimes are smooth: ![\alpha \in [ 0, 1 ]](img/36b28f10b2458c68b27ddc0dba545e36.png). For the latter, ![\alpha](img/9a53e012ad26523af8c1a6778d340c3f.png) can be understood as proportional decomposition weighting of the respective return series, and thus can provide smooth mixing between the regimes. Finally, sign of returns are explicitly decomposed as ![s_t \in \{ -1, 1 \}](img/81d33b065045ea524c0e70f77e8b012a.png), acknowledging greater regularity of absolute-valued return series.

Worth noting is the following are *latent* variables: idiosyncratic path ![z_t](img/74d890ac7e079882a239837ea3afdf8c.png) from the informed regime, proportional factor ![\beta](img/e59dd600f7eb22f952e355797bceba2e.png), and regime parameter ![\alpha](img/9a53e012ad26523af8c1a6778d340c3f.png). Obviously, challenge of this model lies in their estimation. One potential trick is to exploit triangular relationships, as described below.

One stylized fact *not* explicitly accommodated by this model is well-known *asymmetry of uninformed regimes*, arising from analysis of market breadth: stocks uniformly go down together (think big down days), but much less often uniformly go up together (majority of rallies). Unclear whether this fact naturally arises via ![\alpha](img/9a53e012ad26523af8c1a6778d340c3f.png) or needs to be explicitly modeled.

Readers familiar with machine learning (ML) may recognize how to reformulate this as an *additive model*:

   ![r(\textbf{x}) = \sum\limits_{i=1}^2 w_i f_i(\textbf{x}) ](img/e08d6dab2b35925f5ca475316add0354.png)

Where ![\textbf{x} \equiv \{ z, i, \alpha, \beta \}](img/41c8b5f4ce625c80770706f459b5e3ed.png).

This model can be interpreted in numerous ML ways, depending on the desired objective. For example, ![z](img/7d74f7d8fdd6545e22c6dd9de0af53b3.png) and ![i](img/6aed483d693a0743f647c27ec4372c2a.png) can be interpreted as basis functions. Alternatively, boosting can be applied by interpreting them as weak classifiers. Graphical models can be applied by introducing conditional dependence between ![r](img/77c7edfa0ca5ff951f4f75b75deb7f01.png), ![z](img/7d74f7d8fdd6545e22c6dd9de0af53b3.png), and ![i](img/6aed483d693a0743f647c27ec4372c2a.png). Hierarchical models and decision trees naturally arise when ![z](img/7d74f7d8fdd6545e22c6dd9de0af53b3.png) and ![i](img/6aed483d693a0743f647c27ec4372c2a.png) are further functionally decomposed.

Given this model, an interesting question is how to use it *predicatively*—whether directional or not. For example, combining models for two stocks which share a common index to introduce the notion of equity triangle arbitrage on the joint ![z](img/7d74f7d8fdd6545e22c6dd9de0af53b3.png).