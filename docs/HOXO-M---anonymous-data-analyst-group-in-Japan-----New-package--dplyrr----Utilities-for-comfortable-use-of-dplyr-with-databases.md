<!--yml

category: 未分类

date: 2024-05-18 06:47:53

-->

# HOXO-M - anonymous data analyst group in Japan - : New package "dplyrr" - Utilities for comfortable use of dplyr with databases

> 来源：[`mockquant.blogspot.com/2015/08/new-package-dplyrr-utilities-for.html#0001-01-01`](http://mockquant.blogspot.com/2015/08/new-package-dplyrr-utilities-for.html#0001-01-01)

## 1\. Overview

`dplyr package `

is the most powerful package for data handling in R, and it has also the ability of working with databases(

[See Vignette](https://cran.rstudio.com/web/packages/dplyr/vignettes/databases.html)

).

But the functionalities of dealing with databases in

`dplyr`

is begin developped even now.

Now, I'm trying to make

`dplyr`

with databases more comfortable by some functions.

For that purpose, I've created

`dplyrr`

package.

`dplyrr`

has below functions:

+   `load_tbls()` : Easy to load table objects for all tables in a database.

+   `cut()` in `mutate()` : Easy to create a case statement by using the grammar like the `base::cut()`.

+   `count_if()` and `n_if()` in `summarise()` : Shortcut to count rows that a condition is satisfied.

+   `filter()` : Improved `filter()` for `tbl_sql` which adds parentheses appropriately.

+   `moving_mean()` in `mutate()` : Compute moving average for PostgreSQL.

+   `moving_max()` in `mutate()` : Compute moving max for PostgreSQL.

+   `moving_min()` in `mutate()` : Compute moving min for PostgreSQL.

+   `moving_sum()` in `mutate()` : Compute moving sum for PostgreSQL.

+   `first_value()` in `mutate()` : Compute first value for PostgreSQL.

## 2\. How to install

The source code for

`dplyrr`

package is available on GitHub at

You can install the pakage from there.

```
install.packages("devtools") # if you have not installed "devtools" package
devtools::install_github("hoxo-m/dplyrr") 
```

## 3\. Common functions for all databases

For illustration, we use a database file: "my_db.sqlite3".

If you want to trace the codes below, you should create the databese file at first.

```
library(dplyrr)
library(nycflights13)

db 
```

### 3-1\. load_tbls()

Usually, when we use a database with

`dplyr`

, we first create database object, and we can see the tables in the databese by

`show()`

.

```
library(dplyrr)
# Create database object
db 
```

```
## src:  sqlite 3.8.6 [my_db.sqlite3]
## tbls: airlines, airports, flights, planes, sqlite_stat1, weather

```

Next, we create table objects for pulling data in some tables in the database.

```
airlines_tbl 
```

Typing this code is really a bore!

If you want to create table objects for

**all tables in the database**

, you can use

`load_tbls()`

.

```
load_tbls(db) 
```

```
## Loading: airlines_tbl
## Loading: airports_tbl
## Loading: flights_tbl
## Loading: planes_tbl
## Loading: sqlite_stat1_tbl
## Loading: weather_tbl

```

Check the created table objects.

```
ls(pattern = "_tbl$") 
```

```
## [1] "airlines_tbl"     "airports_tbl"     "flights_tbl"     
## [4] "planes_tbl"       "sqlite_stat1_tbl" "weather_tbl"

```

```
glimpse(airlines_tbl) 
```

```
## Observations: 16
## Variables:
## $ carrier (chr) "9E", "AA", "AS", "B6", "DL", "EV", "F9", "FL", "HA", ...
## $ name    (chr) "Endeavor Air Inc.", "American Airlines Inc.", "Alaska...

```

### 3-2\. cut() in mutate()

If you want to write case statement with like

`base::cut()`

, you can use

`cut()`

function in

`mutate()`

.

For example, there is

`air_time`

column in the database.

```
db % select(air_time)
air_time % collect
head(air_time, 3) 
```

```
## Source: local data frame [3 x 1]
## 
##   air_time
## 1      227
## 2      227
## 3      160

```

If you want to group the

`air_time`

by break points

`c(0, 80, 120, 190, 900)`

, you think you must write the next code.

```
q % 
  select(air_time) %>%
  mutate(air_time_cut = if(air_time > 0 && air_time <= 80) "(0,80]"
         else if(air_time > 80 && air_time <= 120) "(80,120]"
         else if(air_time > 120 && air_time <= 190) "(120,190]"
         else if(air_time > 190 && air_time <= 900) "(190,900]")
air_time_with_cut % collect
head(air_time_with_cut, 3) 
```

```
## Source: local data frame [3 x 2]
## 
##   air_time air_time_cut
## 1      227    (190,900]
## 2      227    (190,900]
## 3      160    (120,190]

```

When the break points increase, you are going to be tired to write more lines.

By using

`cut()`

function in

`mutate()`

, it can become easy.

```
q % 
  select(air_time) %>%
  mutate(air_time_cut = cut(air_time, breaks=c(0, 80, 120, 190, 900)))
air_time_with_cut % collect
head(air_time_with_cut, 3) 
```

```
## Source: local data frame [3 x 2]
## 
##   air_time air_time_cut
## 1      227    (190,900]
## 2      227    (190,900]
## 3      160    (120,190]

```

The

`cut()`

in

`mutate()`

has more arguments such as labels coming from

`base::cut()`

.

+   `cut(variable, breaks, labels, include.lowest, right, dig.lab)`

For integer break points, specially you can indicate

`labels="-"`

.

```
q % 
  select(air_time) %>%
  mutate(air_time_cut = cut(air_time, breaks=c(0, 80, 120, 190, 900), labels="-"))
air_time_with_cut % collect
head(air_time_with_cut, 3) 
```

```
## Source: local data frame [3 x 2]
## 
##   air_time air_time_cut
## 1      227      191-900
## 2      227      191-900
## 3      160      121-190

```

### 3-3\. count_if() and n_if() in summarise()

当我们想要计数满足条件的行时，我们可能会写成这样。

```
q % 
  select(air_time) %>%
  summarise(odd_airtime_rows = sum(if(air_time %% 2 == 1) 1L else 0L), 
            even_airtime_rows = sum(if(air_time %% 2 == 0) 1L else 0L), 
            total_rows=n())
q %>% collect 
```

```
## Source: local data frame [1 x 3]
## 
##   odd_airtime_rows even_airtime_rows total_rows
## 1           164150            163196     336776

```

The

`count_if()`

并且

`n_if()`

函数仅仅是它的一个快捷方式。

+   `count_if(condition)`

+   `n_if(condition)`

```
q % 
  select(air_time) %>%
  summarise(odd_airtime_rows = count_if(air_time %% 2 == 1), 
            even_airtime_rows = n_if(air_time %% 2 == 0), 
            total_rows=n())
q %>% collect 
```

```
## Source: local data frame [1 x 3]
## 
##   odd_airtime_rows even_airtime_rows total_rows
## 1           164150            163196     336776

```

两个函数完全做同样的事情。

### 3-4. 改进 filter()

如果你用

`dplyr`

纯净的思维中使用数据库的时候，你可能会碰到下面不期而遇的情形。

```
library(dplyr)

db %
  select(month, air_time) %>%
  filter(month == 1) %>%
  filter(air_time > 200 || air_time < 100)
q$query 
```

```
## <Query> SELECT "month" AS "month", "air_time" AS "air_time"
## FROM "flights"
## WHERE "month" = 1.0 AND "air_time" > 200.0 OR "air_time" < 100.0
## <SQLiteConnection>

```

你预期 WHERE 子句是这样的吗？

如果你使用

`dplyrr`

，加括号就自然了。

```
library(dplyrr)

db %
  select(month, air_time) %>%
  filter(month == 1) %>%
  filter(air_time > 200 || air_time < 100)
q$query 
```

```
## <Query> SELECT "month" AS "month", "air_time" AS "air_time"
## FROM "flights"
## WHERE ("month" = 1.0) AND ("air_time" > 200.0 OR "air_time" < 100.0)
## <SQLiteConnection>

```

## 4. PostgreSQL 的函数

### 4-1. mutate() 中的 moving_**()

`dplyrr`

有四个

`moving_**()`

可以在函数中使用的函数

`mutate()`

。

+   `moving_mean(variable, preceding, following)`

+   `moving_max(variable, preceding, following)`

+   `moving_min(variable, preceding, following)`

+   `moving_sum(variable, preceding, following)`

当你想设置相同的

`preceding`

并且

`following`

，你可以省略

`following`

。

为了说明，我们使用的测试数据库是 PostgreSQL。

```
srcs 
```

```
##   x
## 1 1
## 2 2
## 3 3
## 4 4
## 5 5

```

计算前 1 个和后 1 个数据的移动均值。

```
q %
  mutate(y = moving_mean(x, 1))
q %>% collect 
```

```
## Source: local data frame [5 x 2]
## 
##   x   y
## 1 1 1.5
## 2 2 2.0
## 3 3 3.0
## 4 4 4.0
## 5 5 4.5

```

确认查询。

```
q$query 
```

```
## <Query> SELECT "x", "y"
## FROM (SELECT "x", avg("x") OVER (ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING) AS "y"
## FROM "tlsqbjsuou") AS "_W1"
## <PostgreSQLConnection:(10316,0)>

```

计算前 1 个和后 2 个数据的移动平均值。

```
q %
  mutate(y = moving_mean(x, 1, 2))
q %>% collect 
```

```
## Source: local data frame [5 x 2]
## 
##   x   y
## 1 1 2.0
## 2 2 2.5
## 3 3 3.5
## 4 4 4.0
## 5 5 4.5

```

确认查询。

```
q$query 
```

```
## <Query> SELECT "x", "y"
## FROM (SELECT "x", avg("x") OVER (ROWS BETWEEN 1 PRECEDING AND 2 FOLLOWING) AS "y"
## FROM "tlsqbjsuou") AS "_W2"
## PostgreSQLConnection:(10316,0)>

```

同理，你可以使用其他的

`moving_**()`

函数。

### 4-2. mutate() 中的 first_value()

`dplyrr`

有

`first_value()`

你可以在其中使用的函数

`mutate()`

。

+   `first_value(value, order_by)`

当你想设置相同的

`value`

以及

`order_by`

，你可以省略

`order_by`

。

为了说明，我们使用的测试数据库是 PostgreSQL。

```
srcs 
```

```
##   class x y
## 1     A 1 6
## 2     A 2 5
## 3     B 3 4
## 4     B 4 3
## 5     C 5 2
## 6     C 6 1

```

根据类别对 x 的第一个值进行排序。

```
q %
  group_by(class) %>%
  mutate(z = first_value(x))
q %>% collect 
```

```
## Source: local data frame [6 x 4]
## Groups: class
## 
##   class x y z
## 1     A 1 6 1
## 2     A 2 5 1
## 3     B 3 4 3
## 4     B 4 3 3
## 5     C 5 2 5
## 6     C 6 1 5

```

看查询。

```
q$query 
```

```
## <Query> SELECT "class", "x", "y", "z"
## FROM (SELECT "class", "x", "y", first_value("x") OVER (PARTITION BY "class" ORDER BY "x") AS "z"
## FROM "slrhxfdvrt") AS "_W3"
## <PostgreSQLConnection:(10316,0)>

```

根据 y 对 x 的第一个值进行排序。

```
q %
  group_by(class) %>%
  mutate(z = first_value(x, y))
q %>% collect 
```

```
## Source: local data frame [6 x 4]
## Groups: class
## 
##   class x y z
## 1     A 2 5 2
## 2     A 1 6 2
## 3     B 4 3 4
## 4     B 3 4 4
## 5     C 6 1 6
## 6     C 5 2 6

```

看查询。

```
q$query 
```

```
## <Query> SELECT "class", "x", "y", "z"
## FROM (SELECT "class", "x", "y", first_value("x") OVER (PARTITION BY "class" ORDER BY "y") AS "z"
## FROM "slrhxfdvrt") AS "_W4"
## <PostgreSQLConnection:(10316,0)>

```

根据 y 的降序对 x 的第一个值进行排序。

```
q %
  group_by(class) %>%
  mutate(z = first_value(x, desc(y)))
q %>% collect 
```

```
## Source: local data frame [6 x 4]
## Groups: class
## 
##   class x y z
## 1     A 1 6 1
## 2     A 2 5 1
## 3     B 3 4 3
## 4     B 4 3 3
## 5     C 5 2 5
## 6     C 6 1 5

```

看查询。

```
q$query 
```

```
## <Query> SELECT "class", "x", "y", "z"
## FROM (SELECT "class", "x", "y", first_value("x") OVER (PARTITION BY "class" ORDER BY "y" DESC) AS "z"
## FROM "slrhxfdvrt") AS "_W5"
## <PostgreSQLConnection:(10316,0)>

```

## 5. 其他

### update_dplyrr()

`update_dplyrr()`

是

```
devtools::install_github("hoxo-m/dplyrr") 
```

### unload_dplyrr()

`unload_dplyrr()`

是

```
detach("package:dplyrr", unload = TRUE)
detach("package:dplyr", unload = TRUE) 
```

## 6. Bug 报告
