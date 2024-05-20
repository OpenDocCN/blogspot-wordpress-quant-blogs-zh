<!--yml
category: 未分类
date: 2024-05-18 15:41:35
-->

# Applying Genetic Algorithms | Tr8dr

> 来源：[https://tr8dr.wordpress.com/2007/10/27/applying-genetic-algorithms/#0001-01-01](https://tr8dr.wordpress.com/2007/10/27/applying-genetic-algorithms/#0001-01-01)

October 27, 2007 · 8:49 pm

I have done some experimentation with genetic algorithms in the past, but am now looking to incorporate as an optimization tool into my rules-based strategy framework.

The behavior of our strategies are often parameterized. There can be so many combinations of parameters, that to arrive at a sucessful or best performing set can be a matter of guesswork, testing and retesting.

Enter Genetic Algorithms (GA). GA allows us to efficiently arrive at a (nearly) best fit set of parameters based on a fitness function. For those not familiar with genetic algorithms (GA), GA is a biology-inspired gene/generational means of evolving a solution based on fitness criteria. A population of genes is produced on each generation, the fittest of which are chosen and recombined with other genes. Successive generations will tend to be more and more fit, arriving at a fitness maximum.

In truth GA, as exotic as it sounds, is just one of many optimization techniques where one is trying to minimize, maximize, or find a zero for a complex function. GA is easy to set up and can work with black-box functions, so is a good candidate.

I need to set up an environment to run the optimization in parallel given the computation required. For each day we evaluate a strategy will be looking at 200K – 500K ticks or more. So to evaluate over, say, 3 months of data is 30 million ticks. Multiply this by 1000 or more fitness evaluations, and one is looking to evaluate billions of ticks and rules.

Given that we have datasynapse available on hundreds of blades, may adapt JGAP and the strategy engine for this infrastructure.