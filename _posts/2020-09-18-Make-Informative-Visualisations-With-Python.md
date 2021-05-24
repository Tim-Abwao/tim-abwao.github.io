---
tags: python visualisation
last_modified_at: 2020-11-17T03:00:50+00:00
---

More often than not, a rather hefty amount of work is required to transform and/or aggregate raw data into the form that can be fed into graphical software to yield *elaborate* visualisations. However, this doesn't always have to be the case.

You can make things drastically easier for youself by choosing the right tools. Below are a few popular plotting libraries in Python. This article will focus on introducing how easily they generate informative graphs. The data set used in the examples is the well known [iris dataset][13].

## 1. Static Graphs

[![seaborn logo](/assets/images/toolkit/seaborn-logo.png)][1]

[Seaborn][1] is great for creating elegant statistical graphs with just a few lines of code. It provides a *high-level interface* to the ubiquitous [Matplotlib][2] plotting library.

*Seaborn's functions* & *classes* perform the necessary operations on the data behind the scenes, and supply convenient defaults that yield rich *Matplotlib* graphics. For example:

```python
import seaborn as sns

iris_data = sns.load_dataset('iris')
sns.pairplot(iris_data, hue='species', kind='reg')
```

In a [Jupyter notebook][3] with the [matplotlib inline back-end][4], the output will be displayed as follows:

![seaborn graph](/assets/images/articles/data-viz/seaborn-pairplot.png)

The above example demonstrates *Seaborn's* close integration with [pandas][5]. The data supplied is a *pandas DataFrame*:

```text
iris_data.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 150 entries, 0 to 149
Data columns (total 5 columns):
 #   Column        Non-Null Count  Dtype
---  ------        --------------  -----
 0   sepal_length  150 non-null    float64
 1   sepal_width   150 non-null    float64
 2   petal_length  150 non-null    float64
 3   petal_width   150 non-null    float64
 4   species       150 non-null    object
dtypes: float64(4), object(1)
memory usage: 6.0+ KB
```

*Seaborn* automatically selected the numeric columns in the data, colour-coded them by 'species', and generated scatter plots (with linear regression lines fitted) on column pairs. If the goal was to study the relationship between iris sepal and petal dimensions, the graph says it all.

Suppose we were interested in comparing the range of values for each of the columns *sepal_length*, *sepal_width*, *petal_length* and *petal_width*. This can very easily be achieved with:

```python
sns.violinplot(data=iris_data)
```

![seaborn violinplot](/assets/images/articles/data-viz/seaborn-violinplot.png)

Since *seaborn* is built on top of *Matplotlib*, you can customise its graphs using *Matplotlib's* methods and parameters:

```python
ax = sns.violinplot(data=iris_data)
ax.set_title('Comparing Iris Sepal & Petal Dimensions', size=15, pad=10)
ax.set_ylabel('Length in $cm$', size=12)
ax.set_xlabel('Iris flower dimensions', size=12)
```

![seaborn violinplot with labels](/assets/images/articles/data-viz/seaborn-violinplot-detailed.png)

For more on *seaborn*, please visit its [official documentation][1] and [example gallery][14]

[![pandas](/assets/images/toolkit/pandas.svg)][5]

The [pandas plotting API][6] allows you to quickly create graphs from within *pandas* data structures using the `.plot` method, which is basically a [wrapper][7] around `matplotlib.pyplot.plot`

```python
iris_data.plot.scatter(x='petal_width', y='sepal_width')
```

![pandas scatterplot](/assets/images/articles/data-viz/pandas-scatterplot.png)

If we wish to produce a scatterplot with a different color for each iris species, we have to map *species* values to acceptable color input values. (In *seaborn*, there's a convenient *hue* parameter that does this implicitly)

```python
color_dict = {'setosa': 'blue', 'versicolor': 'orange', 'virginica': 'green'}
iris_data['colors'] = iris_data['species'].apply(color_dict.get)
iris_data.plot.scatter(x='petal_width', y='sepal_width', c='colors')
```

![pandas scatterplot color-coded](/assets/images/articles/data-viz/pandas-scatterplot-colored.png)

You can also specify the type of graph to plot by passing any of the following as the `kind` parameter of the `.plot` method:

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
- scatter

```python
iris_data.plot(kind='hist', alpha=0.5)
```

![pandas histogram](/assets/images/articles/data-viz/pandas-hist.png)

[Andrew curves][15] made easy:

```python
from pandas.plotting import andrews_curves
andrews_curves(iris_data, 'species')
```

![pandas andrewcurves](/assets/images/articles/data-viz/pandas-andrewcurves.png)

[![matplotlib logo](/assets/images/toolkit/matplotlib.svg)][2]

High-level interfaces like *Seaborn* and *pandas* are all well and good. But when you need to make unique tweaks, or create somewhat 'peculiar' graphs just to your liking; you'll probably need to use good ol' *Matplotlib*.

For example,

```python
import matplotlib.pyplot as plt


fig, axes = plt.subplots(nrows=1, ncols=3, figsize=(18, 5), sharey=True)

iris_species_data = iris_data.groupby('species')

for ax, species in zip(axes, ['setosa', 'versicolor', 'virginica']):
    data = iris_species_data.get_group(species).reset_index(drop=True)
    ax.plot(data.select_dtypes(include='number'))
    ax.set_title(f'{species.title()} Dimensions')
    ax.set_ylabel('Length in $cm$')
    ax.set_xlabel('Index')
    ax.legend(data.columns)
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)
```

![matplotlib subplots](/assets/images/articles/data-viz/matplotlib-subplots.png)

## 2. Interactive graphs

[![plotly logo](/assets/images/articles/data-viz/plotly-logo.svg)][9]

[plotly.py][9] enables you to create spectacular interactive graphs that can easily be integrated into dashboard apps and websites. *plotly.py* is built on top of the [plotly.js][10] *JavaScript* graphing library.

Some of its most appealing features are that it allows you to hover over markers to get details, and conveniently zoom in or out of regions of interest. Like *Seaborn*, *plotly.py* is integrated with *pandas*, making it easy to create vivid graphs using *pandas* data structures.

```python
import plotly.express as px

data = px.data.iris()
fig = px.scatter(data, x='petal_width', y='sepal_width', color='species')
fig.show()
```

<iframe title="plotly scatter plot" src='/assets/images/articles/data-viz/plotly-scatter.html'></iframe>

Here's an example from its [basic chart example gallery][16]. Try clicking on the inner levels:

```python
import plotly.express as px

df = px.data.tips()
fig = px.sunburst(df, path=['day', 'time', 'sex'], values='total_bill')
fig.show()
```

<iframe title="plotly scatter plot" src='/assets/images/articles/data-viz/plotly-sunburst.html'></iframe>

## Next Steps

For a more comprehensive catalogue of available Python Graphing libraries, please visit the [PyViz website][12].

Each plotting library usually provides an example gallery showcasing the graphs it can produce. You could peruse them all to expand your visualisation toolbox.

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
[13]: https://en.wikipedia.org/wiki/Iris_flower_data_set
[14]: https://seaborn.pydata.org/examples/index.html
[15]: https://en.wikipedia.org/wiki/Andrews_plot
[16]: https://plotly.com/python/basic-charts/
