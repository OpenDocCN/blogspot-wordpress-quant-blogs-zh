<!--yml
category: 未分类
date: 2024-05-18 08:07:19
-->

# Passing a pandas.DataFrame on to Javascript within Ipython/Jupyter Notebook | Quant Corner

> 来源：[https://quantcorner.wordpress.com/2014/10/13/from-a-python-dataframe-to-javascript-within-ipython-notebook/#0001-01-01](https://quantcorner.wordpress.com/2014/10/13/from-a-python-dataframe-to-javascript-within-ipython-notebook/#0001-01-01)

***Updated on Jan 3rd. 2016 – See at the bottom the code for Jupyter notebook 4.0.1***

I was willing to pass on data contained in a quite big dataframe  — specifically a **pandas.DataFrame** object to **Javascript** within **IPython Notebook 3.2.1** .

Some say it is not straightforward due to security reasons, other argue it requires a template engine such as **Jinja2**.

After some time (banging my head against the wall), I finally came up with the following solution (see code below). Yeah .. it was  simple actually: use a built-in **IPython** **widget**.

Just write these few lines of **Python** in a cell of the notebook:# Required library

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

And, that’s it!

One can check that the data originally produced in **Python** are available to **Javascript**, eg:

```
var jsString = $('div.dataframe').text();

```

One can then eg convert it (back) to **json** which makes the data easy to manipulate with **Javascript**:

```
var obj = jQuery.parseJSON(jsString);

```

***/* Update Jan 3rd. 2016 – code for Jupyter notebook 4.0.1 */***

The code above just doesn’t work with the newest version of the **IPython notebook** aka **Jupyter**. Instead, use the snippet below:

```
# Header from IPython.html import widgets

# Your pandas.DataFrame 
# It is converted to json 
# Create a Ipython widget
widgets.HTML(value = ''' < div  class='dataframe' > ''' + jsonDf + ' < / div > ' )
```