---
layout: post
author: Abwao
last_modified_at: 2020-09-04T16:10:00+03:00
---
*pandas* is a "*fast*, *powerful*, *flexible* and *easy to use* open source data analysis and manipulation tool, built on top of the Python programming language." - *[pandas home page][1]*

It provides data structures that are portable among multiple packages in Python (graphical, statistical, machine-learning, etc).

## Installation

You can install *pandas* using `pip`:

```bash
pip install pandas
```

However, it's authors [recommend][2] that the easiest way to install it is as part of the [Anaconda][3] distribution.

## Basic Usage

```python
>>> import pandas as pd
>>> s = pd.Series(range(1, 6))
>>> s
0    1
1    2
2    3
3    4
4    5
dtype: int64
>>> df = pd.DataFrame({"X": s, "Squared": s**2})
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
>>> df['X'] >= 3
0    False
1    False
2     True
3     True
4     True
Name: X, dtype: bool
>>> df['Cubed'] = df['X'] * df['Squared']
>>> df
   X  Squared  Cubed
0  1        1      1
1  2        4      8
2  3        9     27
3  4       16     64
4  5       25    125
```

## Getting Started

*pandas* features the iconic [10 minutes to pandas][4] to walk those completely new to it through the basics:

- Creating *Series* and *DataFrames*
- Selecting and viewing data
- Handling missing data
- Merging, joining and reshaping
- Importing and exporting files, among others.

Anyone with prior experience in a different platform (e.g. R, SQL, SAS, STATA) will benefit from [this comparison with pandas][5].

## Next Steps

Browsing through the [extensive User Guide][6], [API reference][7] and the [cookbook][8] is a wonderful way to discover advanced, convenient methods and best practices.

I'm working on [this collection][9] of Jupyter notebooks as I go through the docs. Please feel free to use them.

[1]: https://pandas.pydata.org
[2]: https://pandas.pydata.org/docs/getting_started/install.html
[3]: https://docs.continuum.io/anaconda/
[4]: https://pandas.pydata.org/docs/getting_started/10min.html
[5]: https://pandas.pydata.org/docs/getting_started/comparison/index.html
[6]: https://pandas.pydata.org/docs/user_guide/index.html
[7]: https://pandas.pydata.org/docs/reference/index.html
[8]: https://pandas.pydata.org/docs/user_guide/cookbook.html
[9]: https://github.com/Tim-Abwao/learning-pandas
