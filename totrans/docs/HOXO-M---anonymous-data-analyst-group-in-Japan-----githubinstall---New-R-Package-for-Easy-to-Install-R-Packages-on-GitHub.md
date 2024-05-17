<!--yml
category: 未分类
date: 2024-05-18 06:47:41
-->

# HOXO-M - anonymous data analyst group in Japan - : githubinstall - New R Package for Easy to Install R Packages on GitHub

> 来源：[http://mockquant.blogspot.com/2016/06/githubinstall-new-r-package-for-easy-to.html#0001-01-01](http://mockquant.blogspot.com/2016/06/githubinstall-new-r-package-for-easy-to.html#0001-01-01)

## 1\. Overview

A growing number of R packages are created by various people in the world. A part of the cause of it is the **devtools** package that makes it easy to develop R packages [[1]](https://www.rstudio.com/products/rpackages/devtools/). The **devtools** package not only facilitates the process to develop R packages but also provides an another way to distribute R packages.

When developers publish R packages, the CRAN [[2]](https://cran.r-project.org) is commonly used. You can install the packages that are available on CRAN using `install.package()`. For example, you can install **dplyr** package as follows:

```
install.packages("dplyr")
```

The **devtools** package provides `install_github()` that enables installing packages from GitHub.

```
library(devtools)
install_github("hadley/dplyr")
```

Therefore, developers can distribute R packages that is developing on GitHub. Moreover, there are some developers that they have no intention to submit to CRAN. For instance, Twitter, Inc. provides **AnomalyDetection** package on GitHub but it will not be available on CRAN [[3]](https://blog.twitter.com/2015/introducing-practical-and-robust-anomaly-detection-in-a-time-series). You can install such packages easily using **devtools**.

```
library(devtools)
install_github("twitter/AnomalyDetection")
```

There is a difference between `install.packages()` and `install_github()` in the required argument. `install.packages()` takes package names, while `install_github()` needs repository names. It means that when you want to install a package on GitHub you must remember its repository name correctly.

The trouble is that the usernames of GitHub are often hard to remember. Developers consider the package names so that users can understand the functionalities intuitively. However, they often decide username incautiously. For instance, **ggfortify** is a great package on GitHub, but who created it? What is the username? The answer is *sinhrks* [[4]](https://github.com/sinhrks/ggfortify). It seems to be difficult to remember it.

The **githubinstall** package provides a way to install packages on GitHub by only the package names just like `install.packages()`.

```
library(githubinstall)
githubinstall("AnomalyDetection")
```

```
Suggetion:
 - twitter/AnomalyDetection
Do you install the package? 

1: Yes (Install)
2: No (Cancel)
```

`githubinstall()` suggests the GitHub repository from package names, and asks whether you want to execute the installation.

Furthermore, you may succeed in installing packages from a faint memory because our package automatically correct its spelling by fuzzy string search.

```
githubinstall("AnomaryDetection")
githubinstall("AnomalyDetect")
githubinstall("anomaly-detection")
```

## 2\. Installation

You can install the **githubinstall** package from CRAN.

```
install.packages("githubinstall")
```

The source code for **githubinstall** package is available on GitHub at

## 3\. Details

The **githubinstall** package provides several useful functions.

*   `githubinstall()` or `gh_install_packages()`
*   `gh_suggest()`
*   `gh_suggest_username()`
*   `gh_list_packages()`
*   `gh_search_packages()`
*   `gh_show_source()`
*   `gh_update_package_list()`

The functions have common prefix `gh`. `githubinstall()` is an alias of `gh_install_packages()`.

To use these functions, first, you should load the package as follows.

### 3.1\. Install Packages from GitHub

`githubinstall()` enables to install packages on GitHub by only package names.

```
githubinstall("AnomalyDetection")
```

```
Suggestion:
 - twitter/AnomalyDetection
Do you install the package? 

1: Yes (Install)
2: No (Cancel)

Selection: 
```

The function suggests GitHub repositories. If you type ‘1’ and ‘enter’, then installation of the package will begin. The suggestion is made of looking for the list of R packages on GitHub. The list is provided by [Gepuro Task Views](http://rpkg.gepuro.net).

If multiple candidates are found, you can select one of them.

```
Select one repository or, hit 0 to cancel. 

1: amurali2/cats      cats
2: danielwilhelm/cats No description or website provided.
3: hilaryparker/cats  An R package for cat-related functions #rcatladies
4: lolibear/cats      No description or website provided.
5: rafalszota/cats    No description or website provided.
6: tahir275/cats      ff

Selection: 
```

`githubinstall()` is an alias of `gh_install_packages()`.

```
gh_install_packages("AnomalyDetection")
```

### 3.2\. Suggest Repositories

`githubinstall()` prompts you to install the suggested packages. But you may just want to know what will be suggestions.

`gh_suggest()` returns the suggested repository names as a vector.

```
gh_suggest("AnomalyDetection")
```

```
## [1] "twitter/AnomalyDetection"
```

```
## [1] "amurali2/cats"       "danielwilhelm/cats"  "davidluizrusso/cats"
## [4] "hilaryparker/cats"   "lolibear/cats"       "rafalszota/cats"    
## [7] "tahir275/cats"
```

In addition, `gh_suggest_username()` is useful if you want to know usernames from a faint memory.

```
gh_suggest_username("hadly")
```

```
## [1] "hadley"
```

```
gh_suggest_username("yuhui")
```

```
## [1] "yihui"
```

### 3.3\. List the Packages

`gh_list_packages()` returns the list of R package repositories on GitHub as `data.frame`.

For example, if you want to get the repositories that have been created by *hadley*, run the following.

```
hadleyverse <-  gh_list_packages(username = "hadley")
head(hadleyverse)
```

```
##   username package_name                                              title
## 1   hadley   assertthat                     User friendly assertions for R
## 2   hadley    babynames An R package contain all baby names data from the 
## 3   hadley    bigrquery          An interface to Google's bigquery from R.
## 4   hadley     bookdown                                              Watch
## 5   hadley   clusterfly An R package for visualising high-dimensional clus
## 6   hadley      decumar                           An alternative to sweave
```

By using the result, you can install all packages created by hadley.

```
repos <-  with(hadleyverse, paste(username, package_name, sep="/"))
githubinstall(repos) # I have not tried it
```

### 3.4\. Search Packages by a Keyword

`gh_search_packages()` returns the list of R package repositories on GitHub that the titles contains a given keyword.

For example, if you want to search packages that are relevant to *lasso*, run the following.

```
gh_search_packages("lasso")
```

```
##           username     package_name                                  title
## 1  ChingChuan-Chen             milr  multiple-instance logistic regressi..
## 2       YaohuiZeng         biglasso  Big Lasso: Extending Lasso Model Fi..
## 3      huayingfang          CCLasso  CCLasso: Correlation Inference for ..
## 4         mlampros FeatureSelection  Feature Selection in R using glmnet..
## 5             pnnl        glmnetLRC  Lasso and Elastic-Net Logistic Regr..
## 6       statsmaths         genlasso  Path algorithm for generalized lass..
## 7       vincent-dk         logitsgl  Fit Logistic Regression with Multi-..
## 8       vincent-dk             lsgl  Linear Multiple Output Using Sparse..
## 9       vincent-dk             msgl  High Dimensional Multiclass Classif..
## 10      vstanislas             GGEE  R Package for the Group Lasso Gene-..
## 11          zdk123       BatchStARS  R package for Stability Approach to..
## 12          zdk123           pulsar  R package for Stability Approach to..
```

### 3.5\. Show the Source Code of Functions on GitHub

`gh_show_source()` looks for the source code of a given function on GitHub, and tries to open the place on Web browser.

```
gh_show_source("mutate", "dplyr")
```

If you have loaded the package that the function belongs to, you can input the function directly.

```
library(dplyr)
gh_show_source(mutate)
```

This function may do not work well with Safari.

### 3.6\. Update the List of R Packages

The **githubinstall** package uses [Gepuro Task Views](http://rpkg.gepuro.net) for getting the list of R packages on GitHub. Gepuro Task Views is crawling the GitHub and updates information every day. The package downloads the list of R packages from Gepuro Task Views each time it was loaded. Thus, you can always use the newest list of packages on a new R session.

However, you may use an R session for a long time. In such case, `gh_update_package_list()` is useful.

`gh_update_package_list()` updates the downloaded list of the R packages explicitly.