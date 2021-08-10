---
tags: python statistics probability
last_modified_at: 2021-08-10T23:07:00+00:00
img_path: /assets/images/articles/probability-distributions/
---

A probability distribution is *"the mathematical function that gives the probabilities(likelihood) of occurrence of different possible outcomes for an experiment"* - [Wikipedia][prob_dist_wiki]

Probability distributions have numerous applications, some of the foremost being modelling real-life phenomena and simulating hypothetical conditions or events.

If you'd like to learn more about probability distributions, here are some resources that might interest you:

- [Probability concepts explained: probability distributions][linked_blog_1]
- [Understanding Probability Distributions][linked_blog_2]
- An extensive [list of probability distributions][dist_list_wiki].

This article will focus on demonstrating several ways to obtain random samples from the **Normal**, **Uniform** and **Exponential** distributions. You can run the examples in [this demo jupyter notebook][notebook], courtesy of [Binder][binder].

To get started locally:

1. Create a virtual environment, and activate it:

    ```bash
    python3 -m venv venv
    source venv/bin/activate
    ```

2. Install the required packages:

    ```bash
    pip install -U pip
    pip install notebook scipy seaborn
    ```

3. [Start the notebook server][running_jupyter] and open a new *Python3* notebook:

    ```bash
    jupyter notebook
    ```

4. Once a notebook is up and running, import the necessary packages, set the sample size and define the plotting function:

    ```python
    import seaborn as sns
    import random
    import numpy as np
    import scipy

    SAMPLE_SIZE = 1000


    def plot(data, title=""):
        """Plots a histogram with a kernel-density-estimate."""
        fig = sns.displot(data, kde=True)
        fig.ax.set_title(title, size=14)
    ```

[prob_dist_wiki]: https://en.wikipedia.org/wiki/Probability_distribution
[notebook]: https://mybinder.org/v2/gh/Tim-Abwao/blog-projects/HEAD?filepath=sampling-from-probability-distributions%2FProbalility%20Distributions%20in%20Python.ipynb
[linked_blog_1]: https://towardsdatascience.com/probability-concepts-explained-probability-distributions-introduction-part-3-4a5db81858dc
[linked_blog_2]: https://statisticsbyjim.com/basics/probability-distributions/
[dist_list_wiki]: https://en.wikipedia.org/wiki/List_of_probability_distributions
[binder]: https://mybinder.org/
[running_jupyter]: https://jupyter.readthedocs.io/en/latest/running.html

## 1. Using the `random` module

The [random][random] module is part of the *Python Standard Library*, and is thus readily available. It contains functions that can generate random samples.

The functions return a *single* `float` value, making it necessary to use looping techniques (a [list comprehension][list_comp] in this case) to get a sample of desired size.

### 1.1 Normal Distribution

```python
random_normal = [random.gauss(mu=0, sigma=1) for _ in range(SAMPLE_SIZE)]
plot(random_normal, title='Normal Sample (from $random$)')
```

![random normal]({{ page.img_path | append: 'random_normal.png' }})

### 1.2 Uniform Distribution

```python
random_uniform = [random.uniform(a=0, b=1) for _ in range(SAMPLE_SIZE)]
plot(random_uniform, title='Uniform Sample (from $random$)')
```

![random uniform]({{ page.img_path | append: 'random_uniform.png' }})

### 1.3 Exponential Distribution

```python
random_exponential = [random.expovariate(lambd=1) for _ in range(SAMPLE_SIZE)]
plot(random_exponential, title='Exponential Sample (from $random$)')
```

![random exponential]({{ page.img_path | append: 'random_exponential.png' }})

Other [available options][random_functions] include:

- `random.triangular(low, high, mode)`
- `random.betavariate(alpha, beta)`
- `random.gammavariate(alpha, beta)`
- `random.lognormvariate(mu, sigma)`
- `random.vonmisesvariate(mu, kappa)`
- `random.paretovariate(alpha)`
- `random.weibullvariate(alpha, beta)`

[list_comp]: https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions
[random]: https://docs.python.org/3/library/random.html
[random_functions]: https://docs.python.org/3/library/random.html#real-valued-distributions

## 2. Using `numpy.random`

*NumPy* is much beloved in *Python* because it provides objects that enable *fast operations on arrays*. See [What is Numpy?][numpy_intro] for more details.

[NumPy][numpy] is a third-party package - it has to be [installed][numpy_install].

The [numpy.random][numpy_random] sub-package contains functions that can generate random samples. These functions return a [numpy.ndarray][numpy_ndarray], which has numerous useful [attributes][numpy_attributes] and [methods][numpy_methods].

### 2.1 Normal Distribution

```python
rng = np.random.default_rng(12345)

# loc is the mean, scale is the standard deviation
random_normal = rng.normal(loc=0, scale=1, size=SAMPLE_SIZE)
plot(random_normal, title='Normal Sample (from $numpy.random$)')
```

![numpy normal]({{ page.img_path | append: 'numpy_normal.png' }})

### 2.2 Uniform Distribution

```python
random_uniform = rng.uniform(low=0, high=1, size=SAMPLE_SIZE)
plot(random_uniform, title='Uniform Sample (from $numpy.random$)')
```

![numpy uniform]({{ page.img_path | append: 'numpy_uniform.png' }})

### 2.3 Exponential Distribution

```python
# scale 𝛽 = 1/𝜆, 𝜆 is the non-zero expected mean
random_exponential = rng.exponential(scale=1, size=SAMPLE_SIZE)
plot(random_exponential, title='Exponential Sample (from $numpy.random$)')
```

![numpy exponential]({{ page.img_path | append: 'numpy_exponential.png' }})

Please see [Random Generator: Distributions][numpy_dist] for more available options:

[numpy]: https://numpy.org/doc/stable/user/index.html
[numpy_install]: https://numpy.org/install/
[numpy_intro]: https://numpy.org/doc/stable/user/whatisnumpy.html
[numpy_random]: https://numpy.org/doc/stable/reference/random/index.html
[numpy_dist]: https://numpy.org/doc/stable/reference/random/generator.html#distributions
[numpy_ndarray]: https://numpy.org/doc/stable/reference/arrays.ndarray.html
[numpy_attributes]: https://numpy.org/doc/stable/reference/arrays.ndarray.html#array-attributes
[numpy_methods]: https://numpy.org/doc/stable/reference/arrays.ndarray.html#array-methods

## 3. Using `scipy.stats`

The [SciPy library][scipy_lib] is also a third-party package, and has to be [installed][scipy_install].

*SciPy* is tightly knit with *NumPy* — they are both included in the [SciPy ecosystem][scipy].

The [scipy.stats][scipy_stats] sub-package contains functions that can generate random samples. These functions too return [numpy.ndarray][numpy_ndarray]s.

### 3.1 Normal Distribution

```python
# loc is the mean, scale is the standard deviation
random_normal = scipy.stats.norm.rvs(loc=0, scale=1, size=SAMPLE_SIZE)
plot(random_normal, title='Normal Sample (from $scipy.stats$)')
```

![scipy normal]({{ page.img_path | append: 'scipy_normal.png' }})

### 3.2 Uniform Distribution

```python
# loc is the lower boundary 𝑎, scale is the range 𝑏−𝑎
random_uniform = scipy.stats.uniform.rvs(loc=0, scale=1, size=SAMPLE_SIZE)
plot(random_uniform, title='Uniform Sample (from $scipy.stats$)')
```

![scipy uniform]({{ page.img_path | append: 'scipy_uniform.png' }})

### 3.3 Exponential Distribution

```python
# scale 𝛽 = 1/𝜆, 𝜆 is the non-zero expected mean
random_exponential = scipy.stats.expon.rvs(scale=1, size=SAMPLE_SIZE)
plot(random_exponential, title='Exponential Sample (from $scipy.stats$)')
```

![scipy exponential]({{ page.img_path | append: 'scipy_exponential.png' }})

Please see [Statistical functions][scipy_stats] for more available options:

[scipy]: https://scipy.org/index.html
[scipy_lib]: https://docs.scipy.org/doc/scipy/reference/index.html
[scipy_install]: https://scipy.org/install.html
[scipy_stats]: https://docs.scipy.org/doc/scipy/reference/stats.html
