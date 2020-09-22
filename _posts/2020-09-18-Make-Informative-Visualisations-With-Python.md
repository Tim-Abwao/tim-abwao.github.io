---
layout: post
author: Abwao
last_modified_at: 2020-09-22T18:00:00+03:00
---

More often than not, a rather hefty amount of work is required to source and process raw data into the format that produces elaborate visualisations. However, choosing the right plotting tools can drastically make things easier for you.

Below are a few popular plotting libraries in Python. This article will focus on introducing how easily they generate informative graphs.

## 1. Static Graphs

[![seaborn logo](/assets/images/toolkit/seaborn-logo.svg)][1]

[Seaborn][1] is great for creating elegant statistical graphs with just a few lines of code. It provides a *high-level* interface to the ubiquitous [Matplotlib][2] plotting library.

*Seaborn's* *functions* & *classes* automatically transform data, and supply convenient defaults that yield rich *Matplotlib* graphics. For example:

```python
import seaborn as sns

sns.set_theme()
data = sns.load_dataset('iris')
sns.scatterplot(x='petal_width', y='sepal_width', data=data, hue='species')
```

In a [Jupyter notebook][3] with the [matplotlib inline back-end][4], the output will be displayed as follows:

![seaborn graph](/assets/images/articles/seaborn1.png)

The above example also demonstrates *Seaborn's* close integration with [pandas][5]. The data supplied is a *pandas DataFrame*:

```python
data.head()
   sepal_length  sepal_width  petal_length  petal_width species
0           5.1          3.5           1.4          0.2  setosa
1           4.9          3.0           1.4          0.2  setosa
2           4.7          3.2           1.3          0.2  setosa
3           4.6          3.1           1.5          0.2  setosa
4           5.0          3.6           1.4          0.2  setosa
```

But only the column names *"petal_width", "sepal_width"* and *"species"* need be specified. *Seaborn* takes care of the rest: getting the data for each given column, colour-coding based on *species*, and ultimately creating the scatter plot.

You can customise *Seaborn* graphs by passing *Matplotlib* parameters, and even display the output on *Matplotlib's* graphical user interface.

```python
>>> import seaborn as sns
>>> import matplotlib.pyplot as plt
>>> data = sns.load_dataset('iris')
>>> plt.figure(figsize=(10, 6))
<Figure size 1000x600 with 0 Axes>
>>> sns.scatterplot(x='petal_width', y='sepal_width', data=data, hue='species')
<matplotlib.axes._subplots.AxesSubplot object at 0x7f20667f3b50>
>>> plt.show()
```

The following window should pop up:

![Matplotlib GUI](/assets/images/articles/matplotlib1.png)

[![pandas](/assets/images/toolkit/pandas.svg)][5]

The [pandas plotting API][6] allows you to quickly create graphs from within *pandas* data structures using the `.plot` method, which is basically a [wrapper][7] around `matplotlib.pyplot.plot`

Recreating the above scatter plot:

```python
import pandas as pd

data = pd.read_csv('https://raw.githubusercontent.com/mwaskom/seaborn-data/master/iris.csv')
color_dict = dict(zip(data['species'].unique(), ['blue', 'orange', 'green']))

data.plot.scatter('petal_width', 'sepal_width', c=data['species'].apply(color_dict.get))
```

![pandas scatterplot](/assets/images/articles/pandas-plot1.png)

Additional options include:

- area
- bar
- barh
- box
- density
- hexbin
- hist
- kde
- line
- pie

```python
data.plot.hist(alpha=0.7)
```

![pandas plot](/assets/images/articles/pandas-plot.png)

```python
from pandas.plotting import andrews_curves
andrews_curves(data, 'species')
```

![pandas plot](/assets/images/articles/pandas-plot2.png)

[![matplotlib logo](/assets/images/toolkit/matplotlib.svg)][2]

No list of Python plotting libraries is truly complete without *Matplotlib*. High-level interfaces like *Seaborn* and *pandas* are all well and good; but when you need to make unique tweaks or create somewhat 'exotic' graphs, you'll probably need to apply ol' *Matplotlib's* versatile methods.

Here's one way to recreate the scatter plot in the examples above using `matplotlib.pyplot`:

```python
import matplotlib.pyplot as plt
import pandas as pd

data = pd.read_csv('https://raw.githubusercontent.com/mwaskom/seaborn-data/master/iris.csv')
color_dict = dict(zip(data['species'].unique(), ['blue', 'orange', 'green']))

plt.scatter(data['petal_width'], data['sepal_width'], c=data['species'].apply(color_dict.get))
```

![matplotlib scatterplot](/assets/images/articles/matplotlib2.png)

## 2. Interactive graphs

[![plotly logo](/assets/images/articles/plotly-logo.svg)][9]

[plotly.py][9] enables you to create spectacular, interactive, web-based graphs that can easily be integrated into dashboard apps and websites. You can hover over individual markers to get details, conveniently zoom in or out and isolate regions of interest.

Like *Seaborn*, *plotly.py* also features close integration with *pandas*, making it easy to create vivid, interactive graphs using *pandas* data structures.

```python
import plotly.express as px

data = px.data.iris()
fig = px.scatter(data, x='petal_width', y='sepal_width', color='species')
fig.show()
```

<iframe title="plotly scatter plot" src='/assets/images/articles/plotly-graph.html'></iframe>

```python
import plotly.express as px
data = px.data.iris()
fig = px.scatter_3d(
    data, x='petal_width', y='sepal_width', z='sepal_length', color='species')
fig.show()
```

<iframe title="plotly scatter plot" src='/assets/images/articles/plotly-graph2.html'></iframe>

*plotly.py* is built on top of the [plotly.js][10] *JavaScript* graphing library. There's also an *R* version, [plotly.r][11].

## Next Steps

For a more comprehensive catalogue of available Python Graphing libraries, check out the [PyViz website][12].

Each plotting library usually provides a gallery showcasing the graphs it can produce. You could peruse them all to expand your visualisation toolbox.

[1]: https://seaborn.pydata.org
[2]: https://matplotlib.org
[3]: https://jupyter.org
[4]: https://ipython.readthedocs.io/en/stable/interactive/plotting.html#id1
[5]: https://pandas.pydata.org
[6]: https://pandas.pydata.org/docs/user_guide/visualization.html
[7]: https://pandas.pydata.org/docs/user_guide/visualization.html#basic-plotting-plot
[8]: https://plotly.com/python/
[9]: https://plotly.com/python/
[10]: https://plotly.com/javascript/
[11]: https://plotly.com/r/
[12]: https://pyviz.org/index.html
