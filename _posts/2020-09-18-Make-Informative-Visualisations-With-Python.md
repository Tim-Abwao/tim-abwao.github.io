---
tags: data-viz seaborn pandas matplotlib plotly
last_modified_at: 2021-11-08T00:45:00+00:00
img_path: /assets/images/articles/data-viz/
---

More often than not, a rather hefty amount of work is required to transform and/or aggregate raw data into a form that can be fed into graphical software to yield *elaborate* visualisations. However, this doesn't always have to be the case.

You can make things drastically easier for youself by choosing the right tools. Below are a few popular plotting libraries in Python. This article will focus on introducing how easily they generate informative graphs. The dataset used in the examples is the well known [iris dataset][iris-data].

## 1. Static Graphs

[![seaborn logo](/assets/images/toolkit/seaborn-logo.png)][seaborn]

[Seaborn][seaborn] is great for creating elegant statistical graphs with just a few lines of code. It provides a *high-level interface* to the ubiquitous [Matplotlib][matplotlib] plotting library.

*Seaborn's functions* & *classes* work behind the scenes and supply convenient defaults that yield rich *Matplotlib* graphics. For example:

```python
import seaborn as sns

iris_data = sns.load_dataset('iris')
sns.pairplot(iris_data, hue='species', kind='reg')
```

In a [Jupyter notebook][jupyter] with the [matplotlib inline back-end][inline-backend], the output will be displayed as follows:

![seaborn graph]({{ page.img_path }}seaborn-pairplot.png)

The above example demonstrates *Seaborn's* close integration with [pandas][pandas]. The data supplied is a *pandas DataFrame*:

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

*Seaborn* automatically selected the numeric columns in the data, colour-coded them by 'species', and generated scatter-plots (with linear regression lines fitted) on column pairs. If the goal was to study the relationship between iris sepal and petal dimensions, the graph says it all.

Suppose we were interested in visualising the range of values for each of the columns *sepal_length*, *sepal_width*, *petal_length* and *petal_width*. This can very easily be achieved with:

```python
sns.violinplot(data=iris_data)
```

![seaborn violinplot]({{ page.img_path }}seaborn-violinplot.png)

Since *seaborn* is built on top of *Matplotlib*, you can customise its graphs using *Matplotlib's* keyword arguments and methods:

```python
ax = sns.violinplot(data=iris_data)
ax.set_title('Comparing Iris Sepal & Petal Dimensions', size=15, pad=10)
ax.set_ylabel('Length in $cm$', size=12)
ax.set_xlabel('Iris flower dimensions', size=12)
```

![seaborn violinplot with labels]({{ page.img_path }}seaborn-violinplot-detailed.png)

For more on *seaborn*, please visit its [official documentation][seaborn] and [example gallery][seaborn-gallery]

[![pandas](/assets/images/toolkit/pandas.svg)][pandas]

The [pandas plotting API][pandas-plot] allows you to quickly create graphs from within *pandas* data structures using the `.plot` method, which is basically a wrapper around `matplotlib.pyplot.plot`

```python
iris_data.plot.scatter(x='petal_width', y='sepal_width')
```

![pandas scatterplot]({{ page.img_path }}pandas-scatterplot.png)

If we wished to produce a scatter-plot with a different color for each species, we'd have to map *species* values to acceptable color input values. (In *seaborn*, there's a convenient *hue* parameter that does this implicitly)

```python
color_dict = {'setosa': 'blue', 'versicolor': 'orange', 'virginica': 'green'}
iris_data.plot.scatter(x='petal_width', y='sepal_width',
                       c=iris_data['species'].map(color_dict))
```

![pandas scatterplot color-coded]({{ page.img_path }}pandas-scatterplot-colored.png)

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

![pandas histogram]({{ page.img_path }}pandas-hist.png)

[Andrews curves][andrew-curves] made easy:

```python
from pandas.plotting import andrews_curves
andrews_curves(iris_data, 'species')
```

![pandas andrewcurves]({{ page.img_path }}pandas-andrewcurves.png)

[![matplotlib logo](/assets/images/toolkit/matplotlib.svg)][matplotlib]

High-level interfaces like *Seaborn* and *pandas* are all well and good. But when you need to make unique tweaks and customize graphs just to your liking, you'll probably need to use good ol' *Matplotlib*:

```python
import matplotlib.pyplot as plt


fig, axes = plt.subplots(nrows=1, ncols=3, figsize=(18, 5), sharey=True)

iris_species_data = iris_data.groupby('species', as_index=False)

for ax, species_data in zip(axes, iris_species_data):
    species, species_df = species_data
    ax.plot(species_df.drop("species", axis=1))
    ax.set_title(f'{species.title()} Dimensions')
    ax.set_ylabel('Length in $cm$')
    ax.set_xlabel('Index')
    ax.legend(species_df.columns)
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)
```

![matplotlib subplots]({{ page.img_path }}matplotlib-subplots.png)

## 2. Interactive graphs

[![plotly logo]({{ page.img_path }}plotly-logo.svg)][plotly-py]

[plotly.py][plotly-py] enables you to create spectacular interactive graphs that can easily be integrated into dashboard apps and websites.

*plotly.py* is a python wrapper for the [plotly.js][plotly-js] *JavaScript* graphing library. It allows you to hover over markers to get details, and conveniently zoom in or out of regions of interest.

Like *Seaborn*, *plotly.py* works well with *pandas*, making it easy to create vivid graphs using *pandas* data structures.

```python
import plotly.express as px

data = px.data.iris()
fig = px.scatter(data, x='petal_width', y='sepal_width', color='species')
fig.show()
```

<div>
    <iframe class="post-iframe" title="plotly scatter plot" src='{{ page.img_path }}plotly-scatter.html'></iframe>
</div>

Here's an example from its [basic chart example gallery][plotly-gallery]. Try clicking on the inner levels:

```python
import plotly.express as px

df = px.data.tips()
fig = px.sunburst(df, path=['day', 'time', 'sex'], values='total_bill')
fig.show()
```

<div>
    <iframe class="post-iframe" title="plotly sunburst" src='{{ page.img_path }}plotly-sunburst.html'></iframe>
</div>

## Next Steps

For a more comprehensive catalogue of available Python graphing libraries, please visit the [PyViz website][pyviz].

Each plotting library usually provides an example gallery showcasing the graphs it can produce. You could peruse them all to expand your visualisation toolbox.

The images used in this article were obtained from [this jupyter notebook][img-source].

[seaborn]: https://seaborn.pydata.org
[seaborn-gallery]: https://seaborn.pydata.org/examples/index.html
[matplotlib]: https://matplotlib.org
[jupyter]: https://jupyter.org
[inline-backend]: https://ipython.readthedocs.io/en/stable/interactive/plotting.html#id1
[pandas]: https://pandas.pydata.org
[pandas-plot]: https://pandas.pydata.org/docs/user_guide/visualization.html
[plotly-py]: https://plotly.com/python/
[plotly-js]: https://plotly.com/javascript/
[plotly-gallery]: https://plotly.com/python/basic-charts/
[pyviz]: https://pyviz.org/index.html
[iris-data]: https://en.wikipedia.org/wiki/Iris_flower_data_set
[andrew-curves]: https://en.wikipedia.org/wiki/Andrews_plot
[img-source]: https://github.com/Tim-Abwao/blog-projects/tree/main/basic-visualisation-python
