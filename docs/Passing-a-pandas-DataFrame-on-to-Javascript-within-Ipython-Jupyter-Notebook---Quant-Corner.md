<!--yml

分类：未分类

日期：2024 年 05 月 18 日 08:07:19

-->

# 通过 Ipython/Jupyter Notebook 在 Javascript 中传递 pandas.DataFrame | 量化角落

> 来源：[`quantcorner.wordpress.com/2014/10/13/from-a-python-dataframe-to-javascript-within-ipython-notebook/#0001-01-01`](https://quantcorner.wordpress.com/2014/10/13/from-a-python-dataframe-to-javascript-within-ipython-notebook/#0001-01-01)

***更新于 2016 年 1 月 3 日 - 在底部查看适用于 Jupyter notebook 4.0.1 的代码***

我想要将一个相当大的数据帧（特别是一个 **pandas.DataFrame** 对象）中的数据传递给 **IPython Notebook 3.2.1** 中的 **Javascript**。

有人说由于安全原因这并不直接，其他人则认为这需要像 **Jinja2** 这样的模板引擎。

经过一段时间（撞墙）后，我终于想出了以下解决方案（见下面的代码）。是的...其实很简单：使用内置的 **IPython** **小部件**。

只需在笔记本的一个单元格中写入这几行 **Python** 代码：# 必需的库

```
import pandas as pd
from IPython.html import widgets

# Create an example pandas DataFrame object
df = pd.DataFrame([{'a': 1, 'b': 2}, {'a': 5, 'b': 10, 'c': 20}], index=['first', 'second'])

# Convert df to json
jsonDf = df.to_json(orient='records')

# Create a Ipython widget
widgets.HTMLWidget(
    value = ''' < div  class='dataframe' > ''' + jsonDf + ' < / div > '
)  # Use hidden argument if required
```

就是这样！

可以检查 **Python** 中最初生成的数据是否可用于 **Javascript**，例如：

```
var jsString = $('div.dataframe').text();

```

然后可以将其转换（回）为 **json**，这样可以方便使用 **Javascript** 进行数据操作：

```
var obj = jQuery.parseJSON(jsString);

```

***/* 2016 年 1 月 3 日更新 - 适用于 Jupyter notebook 4.0.1 的代码 */***

上述代码在最新版本的 **IPython notebook**（即 **Jupyter**）中不起作用。相反，请使用下面的片段：

```
# Header from IPython.html import widgets

# Your pandas.DataFrame 
# It is converted to json 
# Create a Ipython widget
widgets.HTML(value = ''' < div  class='dataframe' > ''' + jsonDf + ' < / div > ' )
```
