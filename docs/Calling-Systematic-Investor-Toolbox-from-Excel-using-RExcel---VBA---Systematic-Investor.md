<!--yml

类别：未分类

日期：2024-05-18 14:37:14

-->

# 从 Excel 使用 RExcel & VBA 调用 Systematic Investor Toolbox | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/04/10/calling-systematic-investor-toolbox-from-excel-using-rexcel-vba/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/04/10/calling-systematic-investor-toolbox-from-excel-using-rexcel-vba/#0001-01-01)

[RExcel](http://rcom.univie.ac.at/download.html)是一个连接 R 和 Microsoft Excel 的强大工具。只需按下按钮，我就可以轻松执行我的 R 脚本，并在 Excel 中交互式地呈现输出。这种简单的集成允许非 R 用户探索 R 语言的强大功能。作为这种方法的一个示例，我想展示如何使用[Systematic Investor Toolbox](https://systematicinvestor.wordpress.com/systematic-investor-toolbox/)创建一个有效前沿并在 Excel 中显示。

首先，您需要从[`rcom.univie.ac.at/download.html`](http://rcom.univie.ac.at/download.html)安装[RExcel](http://rcom.univie.ac.at/download.html)。我使用了以下指南来帮助我安装：[`homepage.univie.ac.at/erich.neuwirth/php/rcomwiki/doku.php?id=wiki:how_to_install`](http://homepage.univie.ac.at/erich.neuwirth/php/rcomwiki/doku.php?id=wiki:how_to_install)

接下来，请检查[RExcel](http://rcom.univie.ac.at/download.html)是否正常工作，尝试一些来自

[`homepage.univie.ac.at/erich.neuwirth/php/rcomwiki/doku.php?id=wiki:excel_worksheet_functions_using_r`](http://homepage.univie.ac.at/erich.neuwirth/php/rcomwiki/doku.php?id=wiki:excel_worksheet_functions_using_r)

现在，我们准备好设计工作簿以运行均值-方差优化以创建有效前沿。以下是完整界面的截图：

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/snapshot.png)

你可以在继续阅读的同时下载[AssetAllocation.xls](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/assetallocation.xls)工作簿并进行实验。

让我们把我们的输入假设放入 Excel 中：在 1:12 行中的回报、风险和相关矩阵。让我们在第 14 行制作一个按钮来构建有效前沿，并将其与我们的**“create_efficient_frontier”** VBA 宏关联起来。

**“create_efficient_frontier”** VBA 宏将从 Excel 收集我们的输入假设，并将它们发送到 R 环境。它将接下来执行 R 脚本以构建有效前沿，最后将收集风险、回报和位于有效前沿上的投资组合的权重的 R 计算结果，并将它们传输回 Excel。

这是构建有效前沿的 R 脚本。我创建了一个名为**“create_rcode”**的 VBA 函数来自动创建此文件以供本示例使用。在实践中，这可以是一个包含算法所有逻辑的静态文件。

```

###############################################################################
# Load Systematic Investor Toolbox (SIT)                                       
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/         
###############################################################################
if(!exists('portopt')) {                                                       
   con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))         
       source(con)                                                             
   close(con)                                                                  
}                                                                              

   #--------------------------------------------------------------------------
   # Create Efficient Frontier                                                
   #--------------------------------------------------------------------------
     ia = list()                                                              
       ia$symbols = ia.name                                                   
       ia$n = len(ia$symbols)                                                 
       ia$expected.return = ia.return                                         
       ia$risk = ia.risk                                                      
       ia$correlation = ia.correlation                                        
   n = ia$n                                                                   

   # 0 <= x.i <= 1                                                            
   constraints = new.constraints(n, lb = 0, ub = 1)                           

   # SUM x.i = 1                                                              
   constraints = add.constraints(rep(1, n), 1, type = '=', constraints)       

   # create efficient frontier                                                
   ef.risk = portopt(ia, constraints, 50)                                     

```

**“create_efficient_frontier”** VBA 宏将收集输入假设并将其发送到 R 环境，然后执行 R 脚本以构建有效边界，最后收集有效边界上的投资组合的风险、收益和权重，并将其传输回 Excel。

下面是自动化所有功能的**“create_efficient_frontier”** VBA 宏：

```

' Create Efficient Frontier
Sub create_efficient_frontier()
    ' Start R connection
    RInterface.StartRServer

    ' Write R code to file
    create_rcode

    ' Clean Output Area
    Sheets("AssetAllocation").Range("A17:IV10000").ClearContents

    ' Put Input Assumptions into R
    RInterface.PutArray "ia.name", Range("AssetAllocation!A4:A12")
    RInterface.PutArray "ia.return", Range("AssetAllocation!B4:B12")
    RInterface.PutArray "ia.risk", Range("AssetAllocation!C4:C12")
    RInterface.PutArray "ia.correlation", Range("AssetAllocation!F4:N12")

    ' Executes the commands in R script
    RInterface.RunRFile r_filename

    ' Get Efficient Frontier into Excel
    RInterface.GetArray "ef.risk$return", Range("AssetAllocation!B17")
    RInterface.GetArray "ef.risk$risk", Range("AssetAllocation!C17")
    RInterface.GetArray "ef.risk$weight", Range("AssetAllocation!E17")     
End Sub

```

这里有一个完整的[AssetAllocation.xls](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/assetallocation.xls)工作簿，可以根据用户指定的输入假设创建一个有效边界。只要安装了[RExcel](http://rcom.univie.ac.at/download.html)，非 R 用户就可以使用这个工作簿来探索 R 语言的强大功能。

请确保将 RExcel 库添加到引用中。首先，点击工具->引用（从 VBA IDE 菜单）

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/rexcel-ref1-small.png)

接下来选择 RExcelVBAlib 并按下确定

![](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/04/rexcel-ref2-small.png)
