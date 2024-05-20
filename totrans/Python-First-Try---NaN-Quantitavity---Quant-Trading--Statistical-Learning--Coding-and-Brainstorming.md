<!--yml
category: 未分类
date: 2024-05-18 13:57:22
-->

# Python First Try | NaN Quantitavity - Quant Trading, Statistical Learning, Coding and Brainstorming

> 来源：[https://quantlife.wordpress.com/2013/03/16/python-first-try/#0001-01-01](https://quantlife.wordpress.com/2013/03/16/python-first-try/#0001-01-01)

### Python First Try

import pandas as pd
import pandas.io.sql as pd_sql
import sqlite3 as sql
import os

path = “C:\\test”
os.chdir(path)

DF = pd.read_csv(‘spy2011.csv’)
DF.head(10)
con = sql.connect(‘data.db’)
pd_sql.write_frame(DF, “tbl”, con)
con.commit()

df = pd.DataFrame({‘label’: [‘A’, ‘B’, ‘C’] + [‘B’] * 2 + [‘A’] * 3, ‘value’: [4, 3, 6, 3, 1, 2, 4, 4]})
df2 = df.sort([‘label’, ‘value’])
df3 = df2.drop_duplicates([‘label’])

No comments yet.