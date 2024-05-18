<!--yml
category: 未分类
date: 2024-05-18 15:36:27
-->

# Mean in the context of Mean-Reversion | Tr8dr

> 来源：[https://tr8dr.wordpress.com/2009/12/02/mean-in-the-context-of-mean-reversion-take-3/#0001-01-01](https://tr8dr.wordpress.com/2009/12/02/mean-in-the-context-of-mean-reversion-take-3/#0001-01-01)

December 2, 2009 · 7:45 pm

I want a running mean estimator that acts as a mode through mean reversion cycles of target amplitude or frequency.   The key characteristics should be:

*   **adaptation to local volatility**
    *   determination of diffusion related squared return
    *   determination of jump related squared return
    *   determination as to how much of the jump should be absorbed into the mean
*   **model of mean reversion**
    *   calibrated to a desired long-run rate of reversion
    *   allowance for changes in reversion constant and reversion to long run
*   **model of mean**
    *   autoregressive
    *   innovations scaled by sigma term (with MR component and jumps removed)
*   **recursive backward estimation of ML**
    *   implicitly decide how innovation is distributed amongst mean, mean-reversion, and noise

**A SDE-based Approach**
The model is an expanded variant of the familiar *Ornstein*–*Uhlenbeck* process, with specialized mean-reversion, mean, and volatility processes.   It also attempts to correct for jumps.    Let’s start with the following SDEs (in continuous time):

[![](img/9907860d771ceb5db1955ddc0504f201.png "Picture 5")](https://tr8dr.wordpress.com/wp-content/uploads/2009/12/picture-5.png)

**Variance**
![](img/b00f73655502dcb9de9b6ec20bcfb769.png)There are many approaches to modeling volatility (all with issues).   Initially I had though to use a predictive model based on:

*   **intensity process** (based on “first exit” duration)
    This is a very complex process.  First approximations have been to use ACD, a family of AR models for duration.   ACD models perform very poorly on HF data however.    It seems that a markov chain model recognizing the patterns will be most appropriate.
*   **amplitude process**
    The amplitudes of squared returns seem to follow a largely AR process.   This seems fairly well behaved.

Before fully committing to a complex volatility model thought its makes sense to first try with a non-predictive measure of realized variance.  I will use:

[![](img/1d5bd43b41c946b3b1ade923efd84773.png "Picture 7")](https://tr8dr.wordpress.com/wp-content/uploads/2009/12/picture-7.png)

The choice of α determines the degree of smoothing with previous values based on how local (and noisy) we want this function to be.   For example, here is the estimate with a smoothing factor of 60 and a threshold of 3e-5:

[![](img/1c603e5c48c096ccff4f43863946cab8.png "Picture 3")](https://tr8dr.wordpress.com/wp-content/uploads/2009/12/picture-3.png)

**Discretising**
Using Ito’s lemma we discretise the processes as follows:

[![](img/a80eba0c5d660e1d156ed14c8529d7fd.png "Picture 8")](https://tr8dr.wordpress.com/wp-content/uploads/2009/12/picture-8.png)

Simplifying the volatility term in S(t), we first determine the variance of the SDE:

[![](img/88eca04b14c1bd1b11423fa4ab821041.png "Picture 2")](https://tr8dr.wordpress.com/wp-content/uploads/2009/12/picture-2.png)

We reorganize as follows:

[![](img/78094f037da4c59e22548924e4af890e.png "Picture 3")](https://tr8dr.wordpress.com/wp-content/uploads/2009/12/picture-31.png)

**Putting it together**
We can now model this discretely as a state-space based filter, searching for parameters that fit a-posteriori idealized view on the mode and mean-reversion process.   Post-parameterization, the process can be used in real-time to provide an estimate of the mode.

**Final Notes**
As you may have seen I took a (useful) 2-3 week diversion before coming back to the SDE based approach.   This is not a final model by any means, but I think a a solid starting point.    The purpose of the above is as a one of a number of factors in a multi-factor  strategy that want to optimize further.