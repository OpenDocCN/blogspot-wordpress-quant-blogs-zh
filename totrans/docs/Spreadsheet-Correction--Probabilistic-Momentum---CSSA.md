<!--yml
category: 未分类
date: 2024-05-12 17:55:07
-->

# Spreadsheet Correction- Probabilistic Momentum | CSSA

> 来源：[https://cssanalytics.wordpress.com/2014/02/12/spreadsheet-correction-probabilistic-momentum/#0001-01-01](https://cssanalytics.wordpress.com/2014/02/12/spreadsheet-correction-probabilistic-momentum/#0001-01-01)

The spreadsheet below is missing a minus sign in the formula which is  highlighted below in red. The formula in cell F3 should read:

=IF(E7>0,1-TDIST(E7,COUNT(C2:C61),1),TDIST(**–**E7,COUNT(C2:C61),1))

This error was not built into our code, it was copied incorrectly into excel. The corrected sheet can be found here: