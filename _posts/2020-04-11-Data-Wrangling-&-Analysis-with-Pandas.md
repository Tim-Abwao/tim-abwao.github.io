---
layout: post
author: Abwao
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
>>> s = pd.Series(range(5))
>>> s
0    0
1    1
2    2
3    3
4    4
dtype: int64
>>> df = pd.DataFrame({'S': s, 'S-squared': s**2})
>>> df
   S  S-squared
0  0          0
1  1          1
2  2          4
3  3          9
4  4         16
>>> df[df['S-squared'] > 5]
   S  S-squared
3  3          9
4  4         16
>>> df['S-cubed'] = df['S'] * df['S-squared']
>>> df
   S  S-squared  S-cubed
0  0          0        0
1  1          1        1
2  2          4        8
3  3          9       27
4  4         16       64
>>> df.describe()
              S  S-squared   S-cubed
count  5.000000   5.000000   5.00000
mean   2.000000   6.000000  20.00000
std    1.581139   6.595453  26.87936
min    0.000000   0.000000   0.00000
25%    1.000000   1.000000   1.00000
50%    2.000000   4.000000   8.00000
75%    3.000000   9.000000  27.00000
max    4.000000  16.000000  64.00000
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
