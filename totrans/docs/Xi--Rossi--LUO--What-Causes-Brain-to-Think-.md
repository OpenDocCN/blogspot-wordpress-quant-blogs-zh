<!--yml
category: 未分类
date: 2024-05-18 14:06:02
-->

# Xi (Rossi) LUO: What Causes Brain to Think?

> 来源：[http://rossiluo.blogspot.com/2012/04/what-cause-brain-to-think.html#0001-01-01](http://rossiluo.blogspot.com/2012/04/what-cause-brain-to-think.html#0001-01-01)

Brain causes us to behave as who we are, but what causes brain to think (activate)?  Indirect measures of brain activities are usually preferred, such as fMRI, but the resulting statistics usually cannot resolve the causality issue.  The simple box plots (image below, left) show no significant differences of the brain activity under two experimental conditions.  Without modeling what the indirect response function looks like (e.g.

[HRF](http://en.wikipedia.org/wiki/Functional_magnetic_resonance_imaging#BOLD_hemodynamic_response)

), our

[paper](http://arxiv.org/abs/1110.6560)

 (to appear in Journal of the American Statistical Association) provides a way to resolve the causality question: what causes brain to think?(image below, right)

This method is specifically designed to provide causal interpretation under interference, and is robust against any shape of the response function.  The R package is

[CIN](http://cran.r-project.org/web/packages/cin/index.html)

.