---
tags: python statistics probability
last_modified_at: 2021-04-15T21:24:00+00:00
img_path: /assets/images/articles/probability-distributions/
---

A probability distribution is *"the mathematical function that gives the probabilities(likelihood) of occurrence of different possible outcomes for an experiment"* - [Wikipedia][prob_dist_wiki]

This article demonstrates several ways to obtain random samples from some of the most popular probability distributions using *Python*. [This jupyter notebook][notebook] allows you to conveniently run the presented examples.

For brevity, we will focus on the *Normal*, *Uniform* and *Exponential* distributions. If you'd like to learn more about probability distributions, here are some resources that might interest you:

- [Probability concepts explained: probability distributions][linked_blog_1]
- [Understanding Probability Distributions][linked_blog_2]
- An extensive [list of probability distributions][dist_list_wiki].

## Getting Started

As earlier stated, you can run the examples in the [demo jupyter notebook][notebook] courtesy of [Binder][binder].

Just in case you wish to run them locally;

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

4. Once a notebook is up and running, import the necessary packages and run the start-up code:

    ```python
    import seaborn as sns
    import random
    import numpy as np
    import scipy

    SAMPLE_SIZE = 1000


    def plot(data, title=''):
        """Plots a combined histogram and kernel-density-estimation plot.
        """
        fig = sns.displot(data, kde=True)
        fig.ax.set_title(title, size=14)
    ```

You should now be able to run the example code blocks.

[prob_dist_wiki]: https://en.wikipedia.org/wiki/Probability_distribution
[notebook]: https://mybinder.org/v2/gh/Tim-Abwao/blog-projects/HEAD?filepath=sampling-from-probability-distributions%2FProbalility%20Distributions%20in%20Python.ipynb
[linked_blog_1]: https://towardsdatascience.com/probability-concepts-explained-probability-distributions-introduction-part-3-4a5db81858dc
[linked_blog_2]: https://statisticsbyjim.com/basics/probability-distributions/
[dist_list_wiki]: https://en.wikipedia.org/wiki/List_of_probability_distributions
[binder]: https://mybinder.org/
[running_jupyter]: https://jupyter.readthedocs.io/en/latest/running.html

## 1. Using the `random` module

The [random][random] module is part of the *Python Standard Library*, and is thus readily available. It contains functions that can generate random samples from probability distributions:

### 1.1 Normal Distribution

```python
random_normal = [random.gauss(mu=0, sigma=1) for _ in range(1000)]
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

### 1.4 More

Other [available options][random_functions] include:

- `random.triangular(low, high, mode)`
- `random.betavariate(alpha, beta)`
- `random.gammavariate(alpha, beta)`
- `random.lognormvariate(mu, sigma)`
- `random.vonmisesvariate(mu, kappa)`
- `random.paretovariate(alpha)`
- `random.weibullvariate(alpha, beta)`

[random]: https://docs.python.org/3/library/random.html
[random_functions]: https://docs.python.org/3/library/random.html#real-valued-distributions

## 2. Using `numpy.random`

[NumPy][numpy] is a third-party package - it has to be [installed][numpy_install].

*NumPy* is much beloved in *Python* because it provides objects that enable *fast operations on arrays*. See [What is Numpy?][numpy_intro] for more details.

The [numpy.random][numpy_random] sub-package contains functions that can generate random samples from probability distributions.

### 2.1 Normal Distribution

```python
rng = np.random.default_rng(12345)

# loc is the mean, scale is the standard deviation
random_normal = np.random.normal(loc=0, scale=1, size=SAMPLE_SIZE)
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

### 2.4 More

Please see [Random Generator: Distributions][numpy_dist] for more available options:

[numpy]: https://numpy.org/doc/stable/user/index.html
[numpy_install]: https://numpy.org/install/
[numpy_intro]: https://numpy.org/doc/stable/user/whatisnumpy.html
[numpy_random]: https://numpy.org/doc/stable/reference/random/index.html
[numpy_dist]: https://numpy.org/doc/stable/reference/random/generator.html#distributions

## 3. Using `scipy.stats`

[SciPy][scipy] is also a third-party package that has to be [installed][scipy_install]. It is tightly knit with [NumPy][numpy].

The [scipy.stats][scipy_stats] sub-package contains functions that can generate random samples from probability distributions.

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

### 3.4 More

Please see [Statistical functions][scipy_stats] for more available options:

[scipy]: https://docs.scipy.org/doc/scipy/reference/index.html
[scipy_install]: https://scipy.org/install.html
[scipy_stats]: https://docs.scipy.org/doc/scipy/reference/stats.html
