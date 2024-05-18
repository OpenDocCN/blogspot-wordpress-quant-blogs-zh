<!--yml
category: 未分类
date: 2024-05-18 15:40:38
-->

# GP for option pricing | Tr8dr

> 来源：[https://tr8dr.wordpress.com/2008/01/20/gp-for-option-pricing/#0001-01-01](https://tr8dr.wordpress.com/2008/01/20/gp-for-option-pricing/#0001-01-01)

January 20, 2008 · 8:19 am

As you probably know GP (Genetic Programming) is an extension of GA which rearranges algebraic or functional instruction trees to fit to a solution.

[![](img/655f47e5320abf7fc31d37da37b3a146.png)](http://upload.wikimedia.org/wikipedia/en/7/77/Genetic_Program_Tree.png)
I had not thought of it previously, but could use such an approach with the right set of functional constructors to converge on an option pricing GP. Now if all we were trying to do was to replicate the Black / Scholes, CEV, or other gaussian distribution based model, would not be very interesting.

We know that the actual distribution are often non-gaussian. Could we produce a more accurate approximation of the hedging cost against a non-gaussian distribution (implying the true risk free price of the option) with GP?

Interestingly, Neural Networks are just special cases of a GP tree, so in the end GP is the most general approach to non-linear regression.