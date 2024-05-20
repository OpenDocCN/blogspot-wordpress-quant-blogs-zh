<!--yml
category: 未分类
date: 2024-05-18 15:33:50
-->

# Impulse Response | Tr8dr

> 来源：[https://tr8dr.wordpress.com/2010/02/20/impulse-response/#0001-01-01](https://tr8dr.wordpress.com/2010/02/20/impulse-response/#0001-01-01)

February 20, 2010 · 12:10 pm

This is just a quick note on deriving an impulse response function for a VECM system.   Basically we want to get the system into a form where we can take the partial derivatives at various lags.   Starting with a simplified VECM:

[![](img/5d63baae20decb58df54fb9502d6f29a.png "VECM")](https://tr8dr.wordpress.com/wp-content/uploads/2010/02/screen-shot-2010-02-20-at-11-40-57-am.png)

Convert this into a form expressing in terms of X instead of ΔX:

[![](img/cc6876cd291727ba33379637191e83b3.png "VECM to VAR form")](https://tr8dr.wordpress.com/wp-content/uploads/2010/02/screen-shot-2010-02-20-at-11-42-10-am.png)

We change variable to simplify the form:

[![](img/14ebe36856c6007a43e4d04c7bd3e634.png "change of variable")](https://tr8dr.wordpress.com/wp-content/uploads/2010/02/screen-shot-2010-02-20-at-11-44-05-am.png)

Via Pesaran and Shin (1996) we transform this into the following recursive expression:

[![](img/121f46d2ca70a9688236817f291a490f.png "Recursive formulation")](https://tr8dr.wordpress.com/wp-content/uploads/2010/02/screen-shot-2010-02-20-at-11-47-18-am.png)

We determine the partial derivative of ∂vj / ∂vk  (i.e. the impact of a change in the kth variable on the ith) after n time periods (t+n) to be:

[![](img/f6d46f1dcd1cb9b46288a987c6929417.png "Screen shot 2010-02-20 at 11.53.29 AM")](https://tr8dr.wordpress.com/wp-content/uploads/2010/02/screen-shot-2010-02-20-at-11-53-29-am.png)

where Si is a selection vector with 1 at the ith position and 0 elsewhere.

Normally the cholesky decomposition is used to orthogonalize the covariance (U U’ = Σ), however other decompositions can be used, providing different measures of  response such as the Bernanke-Sims approach.