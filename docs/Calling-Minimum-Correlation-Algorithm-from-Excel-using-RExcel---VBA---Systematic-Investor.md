<!--yml

category: 未分类

日期：2024-05-18 14:37:22

-->

# 从 Excel 使用 RExcel & VBA 调用最小相关性算法 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/09/27/calling-minimum-correlation-algorithm-from-excel-using-rexcel-vba/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/09/27/calling-minimum-correlation-algorithm-from-excel-using-rexcel-vba/#0001-01-01)

我想展示如何从 Excel 中调用最小相关性算法的示例。我将使用 [RExcel](http://rcom.univie.ac.at/download.html) 来连接 R 和 Excel，并创建一个小的 VBA 单元格数组函数来在 Excel 和 R 之间通信。

我先前在 [“使用 RExcel & VBA 从 Excel 调用 Systematic Investor Toolbox”](https://systematicinvestor.wordpress.com/2012/04/10/calling-systematic-investor-toolbox-from-excel-using-rexcel-vba/) 帖子中讨论了连接 R 和 Excel 的概念。请阅读 [此](https://systematicinvestor.wordpress.com/2012/04/10/calling-systematic-investor-toolbox-from-excel-using-rexcel-vba/) 帖子以获取设置 [RExcel](http://rcom.univie.ac.at/download.html) 的说明。

以下是完整工作簿的屏幕截图：

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/09/snapshot.png)

您可以在阅读的同时下载 [MinimumCorrelation.xls](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/09/minimumcorrelation1.xls) 工作簿并进行实验。

我创建了 VBA 中的“MinimumCorrelation”单元格数组函数。*不要忘记使用 CTRL+SHIFT+ENTER 将“MinimumCorrelation”函数输入到您的工作簿中*。 “MinimumCorrelation”函数将从 Excel 发送历史价格信息到 R 环境。接下来，它将执行 R 脚本，使用最小相关性算法构建权重，最后将收集 R 计算的组合权重并将其传送回 Excel。

这是调用 min.corr.portfolio() 函数的 R 脚本。我创建了一个名为“create_rcode”的 VBA 函数来自动创建此文件作为示例。

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)                                       
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/         
###############################################################################
if(!exists('min.corr.portfolio')) {                                            
   setInternet2(TRUE)                                                          
   con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))         
       source(con)                                                             
   close(con)                                                                  
}                                                                              

   #*****************************************************************          
   # Setup                                                                     
   #*****************************************************************          
   n = ncol(hist_prices)                                                       
   hist = na.omit(hist_prices / mlag(hist_prices) - 1)                         

   # create historical input assumptions                                       
   ia = list()                                                                 
       ia$n = n                                                                
       ia$risk = apply(hist, 2, sd)                                            
       ia$correlation = cor(hist, use='complete.obs', method='pearson')        
       ia$cov = ia$correlation * (ia$risk %*% t(ia$risk))                      

   # portfolio allocation                                                      
   weights = min.corr.portfolio(ia, null)                                      
   dim(weights)=c(1,n)                                                         

```

接下来，VBA 中的“MinimumCorrelation”单元格数组函数调用 R 中的 min.corr.portfolio() 函数：

```

'Minimum Correlation Algorithm
Public Function MinimumCorrelation(ByRef r_values As Range) As Variant
    ' Start R connection
    RInterface.StartRServer

    ' Write R code to file
    create_rcode

    ' Put Historical Asset Prices into R
    RInterface.PutArray "hist_prices", r_values

    ' Executes the commands in filename
    RInterface.RunRFile r_filename

    ' Get Portfolio Allocation determined by the Minimum Correlation Algorithm into Excel
    MinimumCorrelation = RInterface.GetArrayToVBA("weights")
End Function

```

[MinimumCorrelation.xls](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/09/minimumcorrelation1.xls) 工作簿的完整工作副本。

*请不要忘记使用 CTRL+SHIFT+ENTER 将“MinimumCorrelation”函数输入到您的工作簿中*。
