---
description: A glance at Python pandas' data manipulation features.
tags: data-wrangling pandas
last_modified_at: 2020-11-25T14:18:00+03:00
---
*pandas* is a "*fast*, *powerful*, *flexible* and *easy to use* open source data analysis and manipulation tool..." - *[pandas home page][1]*. It's primary data structures, *Series* and *DataFrames*, are equipped with numerous methods, to conveniently handle everyday data wrangling tasks:

- detecting & dealing with missing values
- computing statistics (mean, variance, skewness, correlation, etc)
- applying transformations
- filtering, selection & sorting
- merging data sets & performing group aggregations
- serialization & exports to various formats
- plotting visualisations

among others.

*pandas* leverages [NumPy][12]'s optimized data structures. `DataFrames` are two-dimensional arrays with labelled columns and rows. `Series` are one-dimensional arrays with labelled rows. Most graphical and analytical packages in Python work well with *pandas*, making it essential to learn.

## Getting Started

You can easily install *pandas* using `pip`.

```bash
pip install pandas
```

However, the [recommend way][2] to install it is as part of the [Anaconda][3] distribution.

*pandas* features the iconic [10 minutes to pandas][4] to walk those completely new to it through the basics.

Anyone with prior experience in a different platform (i.e. R, SQL, SAS, STATA) will benefit from [this comparison with pandas][5].

## Basic Usage

```python
>>> import pandas as pd
>>> s = pd.Series(range(50))
>>> s.head()
0    0
1    1
2    2
3    3
4    4
dtype: int64
>>> s2 = s * s - 2
>>> s2.head()
0    -2
1    -1
2     2
3     7
4    14
dtype: int64
>>> df = pd.DataFrame({"x": s, "x-cubed": s**3})
>>> df.head()
   x  x-cubed
0  0        0
1  1        1
2  2        8
3  3       27
4  4       64
>>> df["category"] = list("abcde") * 10
>>> df.head()
   x  x-cubed category
0  0        0        a
1  1        1        b
2  2        8        c
3  3       27        d
4  4       64        e
>>> df.groupby("category").mean()
             x  x-cubed
category               
a         22.5  25312.5
b         23.5  27518.5
c         24.5  29865.5
d         25.5  32359.5
e         26.5  35006.5
>>> df.groupby("category").agg(["count", "std", "skew"])
             x                 x-cubed                        
         count        std skew   count           std      skew
category                                                      
a           10  15.138252  0.0      10  31411.872424  1.277811
b           10  15.138252  0.0      10  33548.118117  1.247907
c           10  15.138252  0.0      10  35771.304549  1.218897
d           10  15.138252  0.0      10  38081.803124  1.190780
e           10  15.138252  0.0      10  40479.948483  1.163548
```

## Next Steps

Browsing through the extensive, and well-detailed [User Guide][6], [API reference][7] and [pandas cookbooks][8] is a wonderful way to discover advanced methods and best practices.

I'm working on [this collection][9] of Jupyter notebooks as I peruse the *pandas* docs. You can [view and run them here][10], courtesy of [Binder][11].

[1]: https://pandas.pydata.org
[2]: https://pandas.pydata.org/docs/getting_started/install.html
[3]: https://docs.continuum.io/anaconda/
[4]: https://pandas.pydata.org/docs/getting_started/10min.html
[5]: https://pandas.pydata.org/docs/getting_started/comparison/index.html
[6]: https://pandas.pydata.org/docs/user_guide/index.html
[7]: https://pandas.pydata.org/docs/reference/index.html
[8]: https://pandas.pydata.org/docs/user_guide/cookbook.html
[9]: https://github.com/Tim-Abwao/learning-pandas
[10]: https://mybinder.org/v2/gh/Tim-Abwao/learning-pandas/HEAD
[11]: https://mybinder.org
[12]: https://numpy.org
