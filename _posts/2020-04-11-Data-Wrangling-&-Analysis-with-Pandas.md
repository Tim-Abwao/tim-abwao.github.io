---
layout: post
author: Abwao
last_modified_at: 2020-04-20T12:00:00+03:00
---
*pandas* is a "**fast**, **powerful**, **flexible** and **easy to use** open source data analysis and manipulation tool, built on top of the Python programming language." - *[pandas home page](https://pandas.pydata.org)*

It holds data in a format that's portable among multiple packages in Python (graphical, statistical, machine-learning, etc).

## Installation

You can install pandas from [PyPI](https://pypi.org/project/pandas/) using:

```bash
$ pip install pandas
```

However, *pandas* [recommends](https://pandas.pydata.org/docs/getting_started/install.html) that the easiest way to install it is as part of the [Anaconda](http://docs.continuum.io/anaconda/) distribution.

## Basic Usage

```python
>>> import pandas as pd
>>> s = pd.Series(range(1,6))  # creating a series
>>> s
0    1
1    2
2    3
3    4
4    5
dtype: int64
>>> df = pd.DataFrame({"X": s, "Squared": s*s})  # dataframe made using series s
>>> df
   X  Squared
0  1        1
1  2        4
2  3        9
3  4       16
4  5       25
>>> df.describe()
              X   Squared
count  5.000000   5.00000
mean   3.000000  11.00000
std    1.581139   9.66954
min    1.000000   1.00000
25%    2.000000   4.00000
50%    3.000000   9.00000
75%    4.000000  16.00000
max    5.000000  25.00000
```

## Getting Started

*pandas* features the iconic [10 minutes to pandas](https://pandas.pydata.org/docs/getting_started/10min.html) to walk those completely new to it through the basics:

- Creating *series* and *dataframes*
- Selecting and viewing data
- Handling missing data
- Merging, joining and reshaping
- Importing and exporting files, among others.

Anyone with prior experience in a different platform (e.g. R, SQL, SAS, STATA) will benefit from [this comparison with pandas](https://pandas.pydata.org/docs/getting_started/comparison/index.html).

## Next Steps

Browsing through the [extensive User Guide](https://pandas.pydata.org/docs/user_guide/index.html), [API reference](https://pandas.pydata.org/docs/reference/index.html) and the [cookbook](https://pandas.pydata.org/docs/user_guide/cookbook.html) is a wonderful way to discover advanced, convenient methods and best practices.

I'm working on [this collection](https://github.com/Tim-Abwao/learning-pandas) of Jupyter notebooks as I go through the docs. Please feel free to use them.
