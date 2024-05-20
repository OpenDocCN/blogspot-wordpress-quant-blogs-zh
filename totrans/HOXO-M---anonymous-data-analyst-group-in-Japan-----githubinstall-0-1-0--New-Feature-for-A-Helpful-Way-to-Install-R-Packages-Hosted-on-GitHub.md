<!--yml
category: 未分类
date: 2024-05-18 06:47:37
-->

# HOXO-M - anonymous data analyst group in Japan - : githubinstall 0.1.0: New Feature for A Helpful Way to Install R Packages Hosted on GitHub

> 来源：[http://mockquant.blogspot.com/2016/08/githubinstall-010-new-feature-for.html#0001-01-01](http://mockquant.blogspot.com/2016/08/githubinstall-010-new-feature-for.html#0001-01-01)

We have updated our **githubinstall** package. It is now on [CRAN](https://cran.rstudio.com/web/packages/githubinstall/).

### Basics

Using the package, you can install R packages hosted on GitHub without usernames.

```
library(githubinstall)
githubinstall("AnomalyDetection")
# It is same as devtools::install_github("twitter/AnomalyDetection")
```

We introduced the package in [the previous entry](http://mockquant.blogspot.jp/2016/06/githubinstall-new-r-package-for-easy-to.html).

You can install or update the package as follows.

```
install.packages("githubinstall")
```

### New Feature

We have added a new feature to the new version of the package.

Now, you can install packages with specifying Git references (branch, tag, commit and pull request).

Developers are divided in policy to manage R packages on GitHub. If a package is going to be developed in "develop" branch, you may want to install the package from the branch.

`gh_install_packages()` has `ref` argument to specify Git references. For instance, you can install **awaptools** from the ["develop" branch](https://github.com/swish-climate-impact-assessment/awaptools/tree/develop) as follows:

```
githubinstall("awaptools", ref = "develop")
```

You may sometimes encounter failing to install packages because its repository HEAD is broken. In such case, you can specify a tag or commit to `ref`. In almost cases, tags are added on an unbroken commit. For instance, you can install **densratio** from the [“v0.0.3” tag](https://github.com/hoxo-m/densratio/releases/tag/v0.0.3) as follows:

```
githubinstall("densratio", ref = "v0.0.3")
```

Even if you cannot find such tags, you can install packages from any commit that is not broken. For instance, you can install **densratio** from the [“e8233e6” commit](https://github.com/hoxo-m/densratio/commit/e8233e651dbef2b34a8c9c2e4432594a13ea8de7) as follows:

```
githubinstall("densratio", ref = "e8233e6")
```

Finally, you may find a patch for fixing bugs as a pull request. In such case, you can specify pull requests to `ref` using `github_pull()`. For instance, you can install **dplyr** from the [pull request #2058](https://github.com/hadley/dplyr/pull/2058) as follows:

```
githubinstall("dplyr", ref = github_pull("2058"))
```

### Bug Fixes

We have fixed some bugs reported on [Issues](https://github.com/hoxo-m/githubinstall/issues). It has detailed on [NEWS](https://github.com/hoxo-m/githubinstall/releases/tag/v0.1.0).

If you find some bugs or need new features, we would appreciate reporting it.