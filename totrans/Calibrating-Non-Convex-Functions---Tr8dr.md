<!--yml
category: 未分类
date: 2024-05-18 15:37:19
-->

# Calibrating Non-Convex Functions | Tr8dr

> 来源：[https://tr8dr.wordpress.com/2009/11/19/calibrating-functions-with-multiple-local-optima/#0001-01-01](https://tr8dr.wordpress.com/2009/11/19/calibrating-functions-with-multiple-local-optima/#0001-01-01)

Many of the calibrations I perform are on non-convex functions, functions with multiple local minima/maxima.    Solving a min(max)imization for this class of function precludes a wide range of algorithms based on gradient descent (such as BFGS).    There are a number of “metaheuristic” approaches to solving non-convex problems, such as: *simulated annealing*, *genetic algorithms*, *differential evolution*, *particle swarm*, and brute force *grid search*, amongst others.

For the last couple of years I have been using [JGAP](http://jgap.sourceforge.net/), a library for optimization via genetic algorithm.    For some time was under the impression that most GA libraries were similar in terms of core algorithm and just different at the API level.   I ran into some problems with the new variance model I am working on, where JGAP was not converging in the expected manner.

I recently began using a package in R for ad-hoc calibrations ([genoud](http://sekhon.berkeley.edu/rgenoud/)) and found that it converges quickly, whereas JGAP did very poorly in comparison.   [DEoptim](http://cran.r-project.org/web/packages/DEoptim/DEoptim.pdf) is a very similar package (a straight implementation of *differential evolution).* Differential Evolution  a cousin of GA, but with a different approach to population evolution.

**Differential Evolution**
Differential Evolution is very similar to standard GA approaches in that both involve working towards the optimum via a randomly generated population of “trial vectors” (θ) and a directed evolution of those vectors towards the optimum.   Differential evolution is implemented as follows:

```
generate Population = { θ1, θ2, θ3, ... } where θ in domain of function
determine θbest ← maxarg [θ : fitness(θ)] forall θ
repeat
   foreach θi in Population
      draw { θa, θb, θc } randomly from P (without duplication)
      θd ← θa + F(θb - θc)
      θnew ← crossover (θd, θi) 

      # adjust ith vector if fitness of generated superior
      if fitness(θnew) > fitness(θi) then
         θi ← θnew

      # adjust best vector if new optimum seen
      if fitness(θnew) > fitness(θbest) then
         θbest ← θnew
   end
until fitness(θbest) approaches target
```

One of the key innovations is that the variance of the innovations (mutations) is dependent on the dispersion of the vectors.  At the outset the dispersion will be large, and as the optimization progresses, the dispersion will reduce and hence mutations will be more focused.   The choice of the function F(), operating on the difference of vectors, has various effects on the speed of convergence and exploration of the domain.  I will not go into it here.

**Improvements with Hybrid Approach**
Provided one has a continuous function with derivatives within the neighborhood of a trial vector, the algorithm can be improved with the use of gradient descent (such as the BFGS algorithm) to locate the true optimum within a neighborhood.    Care must be taken not to optimize too early such that the diversity of trials is lost.

**Some Tests**
Here are some results on the two R packages mentioned above.  Ultimately I need to get an implementation into Java, but wanted to do a comparison with existing implementations first.   I ran optimizations on a particularly pathological gaussian mixture (taken from the examples in the genoud package):

[![](img/9a28649d8472eca3bf328fbd13bb8f4d.png "Picture 10")](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-102.png)

Which looks like:

[![](img/2ddc8e3ce35114d663ef237c0d4e5c4d.png "Picture 11")](https://tr8dr.wordpress.com/wp-content/uploads/2009/11/picture-112.png)

It is clear that gradient descent (ascent) solvers will gravitate to one of the local maxima with the above function.   Testing DEoptim with a population of 100 and similar parameters, both arrived within 1e-4 of the answer within 10 generations (without any BFGS optimization) and 5e-6 within 60 generations.

With BFGS optimization on, genoud arrived within 1e-10 within 2 generations!   Unfortunately genoud arrived at the wrong maximum with some other (more complex) mixture function, whereas the pure DE approach arrived at the proper one.    With appropriate parameterisation can be avoided, however.