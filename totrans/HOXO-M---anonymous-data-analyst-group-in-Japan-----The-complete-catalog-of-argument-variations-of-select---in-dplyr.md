<!--yml
category: 未分类
date: 2024-05-18 06:47:57
-->

# HOXO-M - anonymous data analyst group in Japan - : The complete catalog of argument variations of select() in dplyr

> 来源：[http://mockquant.blogspot.com/2015/07/the-complete-catalog-of-argument.html#0001-01-01](http://mockquant.blogspot.com/2015/07/the-complete-catalog-of-argument.html#0001-01-01)

When I read the [dplyr vignette](https://cran.rstudio.com/web/packages/dplyr/vignettes/introduction.html), I found a convenient way to select sequential columns such as `select(data, year:day)`.
Because I had inputted only column names to `select()` function, I was deeply affected by the convenient way.

On closer inspection, I found that the `select()` function accepts many types of input.
Here, I will enumerate the variety of acceptable inputs for `select()` function.

By the way, these column selection methods also can use in the `summarise_each()`, `mutate_each()` and some functions in **tidyr** package(e.g. `gather()`).

## 1\. Whole codes.

At first, whole codes were shown for perspicuity.
In the sections below, the details of each command were shown.

```
# Data preparation ------------------------------------------------------------------
library(dplyr)
library(nycflights13)
set.seed(123)
data 
```

## 2\. Data preparation.

To follow the [dplyr vignette](https://cran.rstudio.com/web/packages/dplyr/vignettes/introduction.html), `flights` data set in **nycflights13** package were used as an example.

```
library(dplyr)
library(nycflights13)

set.seed(123)
data 
```

```
Variables:
$ year      (int) 2013, 2013, 2013
$ month     (int) 12, 7, 3
$ day       (int) 15, 17, 2
$ dep_time  (int) 2124, 651, 1636
$ dep_delay (dbl) -4, -9, 1
$ arr_time  (int) 2322, 936, 1800
$ arr_delay (dbl) 1, -28, 0
$ carrier   (chr) "UA", "DL", "WN"
$ tailnum   (chr) "N801UA", "N194DN", "N475WN"
$ flight    (int) 289, 763, 1501
$ origin    (chr) "EWR", "JFK", "LGA"
$ dest      (chr) "DTW", "LAX", "MKE"
$ air_time  (dbl) 88, 306, 103
$ distance  (dbl) 488, 2475, 738
$ hour      (dbl) 21, 6, 16
$ minute    (dbl) 24, 51, 36

```

This data set includes the 16 columns shown above.

## 3\. Basic method of use select().

At first, the ways of using `select()` were shown.

```
select(data, year) 
```

```
  year
1 2013
2 2013
3 2013

```

This process shows the way to take the `year` column out of data. To pick multiple columns, you can write the following.

```
select(data, year, month, day) 
```

```
  year month day
1 2013    12  15
2 2013     7  17
3 2013     3   2

```

If columns were sequential in the dataset, you could write the following to pick sequential columns.

```
select(data, year:day) 
```

```
  year month day
1 2013    12  15
2 2013     7  17
3 2013     3   2

```

If you want to remove a specific column, add `-` in the head of the column name as follows.

```
select(data, -year, -month, -day) 
```

```
  dep_time dep_delay arr_time arr_delay carrier tailnum flight origin dest air_time distance hour minute
1     2124        -4     2322         1      UA  N801UA    289    EWR  DTW       88      488   21     24
2      651        -9      936       -28      DL  N194DN    763    JFK  LAX      306     2475    6     51
3     1636         1     1800         0      WN  N475WN   1501    LGA  MKE      103      738   16     36

```

To remove sequential columns, put sequential columns in brackets `()` connected with a colon.

```
select(data, -(year:day)) 
```

```
  dep_time dep_delay arr_time arr_delay carrier tailnum flight origin dest air_time distance hour minute
1     2124        -4     2322         1      UA  N801UA    289    EWR  DTW       88      488   21     24
2      651        -9      936       -28      DL  N194DN    763    JFK  LAX      306     2475    6     51
3     1636         1     1800         0      WN  N475WN   1501    LGA  MKE      103      738   16     36

```

It is also possible to pick columns by choosing the column number.

```
select(data, 1, 2, 3)
select(data, 1:3) 
```

```
  year month day
1 2013    12  15
2 2013     7  17
3 2013     3   2

```

Next topics are slightly advanced.

It is possible to pick sequential columns temporarily and remove some of these.

```
select(data, year:day, -month) 
```

```
  year day
1 2013  15
2 2013  17
3 2013   2

```

It is also possible to remove sequential columns and keep a part of these.

```
select(data, -(year:day), month) 
```

```
  dep_time dep_delay arr_time arr_delay carrier tailnum flight origin dest air_time distance hour minute month
1     2124        -4     2322         1      UA  N801UA    289    EWR  DTW       88      488   21     24    12
2      651        -9      936       -28      DL  N194DN    763    JFK  LAX      306     2475    6     51     7
3     1636         1     1800         0      WN  N475WN   1501    LGA  MKE      103      738   16     36     3

```

Even using a column number can give the same result with the column name. (The results are omitted.)

```
select(data, 1:3, -2)
select(data, -(1:3), 2) 
```

## 4\. Utility functions of select().

Utility functions existing in `select()`, `summarise_each()` and `mutate_each()` in **dplyr** as well as some functions in the **tidyr** package.

Seven functions existed in the utility functions of `select()`.

*   `starts_with(match, ignore.case = TRUE)`
*   `ends_with(match, ignore.case = TRUE)`
*   `contains(match, ignore.case = TRUE)`
*   `matches(match, ignore.case = TRUE)`
*   `num_range(prefix, range, width = NULL)`
*   `one_of(...)`
*   `everything()`

We now check the respective commands and how to use them.

First, `starts_with()` picks columns whose name starts with the specified string.

```
select(data, starts_with("arr")) 
```

```
  arr_time arr_delay
1     2322         1
2      936       -28
3     1800         0

```

The argument `ignore.case` specifies whether the lowercase is classified as a capital letter(default is `TRUE`).

The `ends_with()` picks columns whose name ends with the specified string .

```
select(data, ends_with("time")) 
```

```
  dep_time arr_time air_time
1     2124     2322       88
2      651      936      306
3     1636     1800      103

```

The `contains()` picks columns whose name contains the specified string.

```
select(data, contains("_")) 
```

```
  dep_time dep_delay arr_time arr_delay air_time
1     2124        -4     2322         1       88
2      651        -9      936       -28      306
3     1636         1     1800         0      103

```

The `matches()` picks columns based on a regular expression matching string.

```
select(data, contains("_")) 
```

```
  dep_time dep_delay arr_time arr_delay air_time
1     2124        -4     2322         1       88
2      651        -9      936       -28      306
3     1636         1     1800         0      103

```

When the numbers were included in column names, `num_range()` might be useful.
In this example, we change the column names to be `x1`-`x16` and execute `num_range()` command for the data set.

```
data2 
```

```
  x8     x9  x10 x11
1 UA N801UA  289 EWR
2 DL N194DN  763 JFK
3 WN N475WN 1501 LGA

```

By specifying as `num_range("x", 8:11)`, columns `x8` to `x11` can be identified.
Numbers in the column name are not necessarily sequential.

```
select(data2, num_range("x", c(9, 11))) 
```

```
      x9 x11
1 N801UA EWR
2 N194DN JFK
3 N475WN LGA

```

When column names were padded, the column name was shown as `x01`.
Here, the argument `width` in `num_range()` might be useful.
We now try this process for a data that changes the column names as `x01`-`x16`.

```
data3 
```

```
  x08    x09  x10 x11
1  UA N801UA  289 EWR
2  DL N194DN  763 JFK
3  WN N475WN 1501 LGA

```

By specifying as `width=2`, the zero filled columns can be picked out.

When a column is named as a vector or character string, `one_of()` might be useful.
An error occurs in the following case with `select()`.

```
col_vector 
```

```
Error: All select() inputs must resolve to integer column positions.
The following do not:
*  col_vector

```

However, an intended process occurs in the case of `one_of()`.

```
select(data, one_of(col_vector)) 
```

```
  year month day
1 2013    12  15
2 2013     7  17
3 2013     3   2

```

The `everything()` selects all columns. (Result was omitted.)

```
select(data, everything()) 
```

If add `-` is in the head of a utility function name, we can pick out all except for the area specified in the utility function.

```
select(data, -starts_with("arr")) 
```

```
  year month day dep_time dep_delay carrier tailnum flight origin dest air_time distance hour minute
1 2013    12  15     2124        -4      UA  N801UA    289    EWR  DTW       88      488   21     24
2 2013     7  17      651        -9      DL  N194DN    763    JFK  LAX      306     2475    6     51
3 2013     3   2     1636         1      WN  N475WN   1501    LGA  MKE      103      738   16     36

```

## 5\. Standard evaluation.

Thus far, we explained the normal `select()` function; however, the normal `select()` function cannot handle character strings as arguments.
This might become a problem when column names are given as a string vector for example.
To solve this problem, the `select_()` function was equipped in **dplyr**. (Caution: An underscore was added in the function name.)
The use of the `select_()` function is the same as the `select()` except specifying columns by string; however, attention is needed when specifying a column name by a vector.

```
select_(data, "year", "month", "day") 
```

```
  year month day
1 2013    12  15
2 2013     7  17
3 2013     3   2

```

When specifying column names by a vector, the vector should be given the `.dot` argument.

```
col_vector 
```

```
  year month day
1 2013    12  15
2 2013     7  17
3 2013     3   2

```

All arguments that can use the `select()` function are also possible candidates for the `select_()` function.

```
select_(data, 'year:day')
select_(data, 'year:day', '-month')
select_(data, '-(year:day)')
select_(data, 'starts_with("arr")')
select_(data, '-ends_with("time")') 
```

Furthermore, also in this case, the argument vector should be given the `.dot` argument in the `select_()` function.

```
select_(data, .dots = c('starts_with("arr")', '-ends_with("time")')) 
```

## 6\. References.

Introduction to dplyr
[https://cran.rstudio.com/web/packages/dplyr/vignettes/introduction.html](https://cran.rstudio.com/web/packages/dplyr/vignettes/introduction.html)

Help page for `select()` function
`> help("select", package = "dplyr")`

Original entry in Japanese by hoxo_m
[https://qiita.com/hoxo_m/items/f2f1793c6f086d381340](https://qiita.com/hoxo_m/items/f2f1793c6f086d381340)

Translated by siero