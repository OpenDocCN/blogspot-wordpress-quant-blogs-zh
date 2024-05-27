<!--yml

类别：未分类

日期：2024-05-12 17:55:07

-->

# 概率动量电子表格修正 | CSSA

> 来源：[`cssanalytics.wordpress.com/2014/02/12/spreadsheet-correction-probabilistic-momentum/#0001-01-01`](https://cssanalytics.wordpress.com/2014/02/12/spreadsheet-correction-probabilistic-momentum/#0001-01-01)

下面的电子表格中在红色高亮显示的公式中缺少一个负号。公式应该在 F3 单元格中读作：

=IF(E7>0,1-TDIST(E7,COUNT(C2:C61),1),TDIST(**–**E7,COUNT(C2:C61),1))

这个错误并非是我们代码中固有的，而是被错误地复制到了 Excel 中。修正后的表格可以在以下链接找到：
