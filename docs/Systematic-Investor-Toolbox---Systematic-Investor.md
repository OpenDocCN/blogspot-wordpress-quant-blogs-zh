<!--yml

分类：未分类

日期：2024-05-18 14:43:03

-->

# 系统投资者工具箱 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/systematic-investor-toolbox/#0001-01-01`](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/#0001-01-01)

## 系统投资者工具箱

[系统投资者工具箱 (SIT)](https://github.com/systematicinvestor/SIT)

系统投资者工具箱是我使用的工具集合。

在我的投资研究中。

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/
###############################################################################
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

###############################################################################
# Load Systematic Investor Toolbox (SIT): Windows only
############################################################################### 
# Load Systematic Investor Toolbox (SIT)
setInternet2(TRUE)
con = gzcon(url('https://github.com/systematicinvestor/SIT/raw/master/sit.gz', 'rb'))
	source(con)
close(con)

###############################################################################
# Load Systematic Investor Toolbox (SIT): from file, if for example you saved sit.gz to c:/temp/sit.gz
############################################################################### 
con = gzcon(file('c:/temp/sit.gz', 'rb'))
	source(con)
close(con)

###############################################################################
# Load Systematic Investor Toolbox (SIT): Requires RCurl package
############################################################################### 
require(RCurl)
sit = getURLContent('https://github.com/systematicinvestor/SIT/raw/master/sit.gz', binary=TRUE, followlocation = TRUE, ssl.verifypeer = FALSE)
	con = gzcon(rawConnection(sit, 'rb'))
	source(con)
close(con)

###############################################################################
# Example Usage:
############################################################################### 
# Run plota test
plota.test()

```

更多内容即将推出，

迈克尔·卡普勒

TheSystematicInvestor at gmail
