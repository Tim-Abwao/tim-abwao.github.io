---
description: Generating samples from probability distributions using NumPy, SciPy and random.
tags: probability scipy
last_modified_at: 2022-08-02T02:55:00+00:00
img_path: /assets/images/articles/probability-distributions/
---

A probability distribution is *"the mathematical function that gives the probabilities(likelihood) of occurrence of different possible outcomes for an experiment"* - [Wikipedia][prob_dist_wiki]

Probability distributions are chiefly employed in modelling real-life phenomena such as customer arrival patterns, the lifespan of machine components, and even the spread of diseases.

![falling dice]({{ page.img_path | append: 'dice.jpg' }})

Photo by [Riho Kroll][dice-source] on [Unsplash][dice-unsplash]
{: .caption }

If you'd like to learn more about probability distributions, here are some resources that might interest you:

- [Probability concepts explained: probability distributions][linked_blog_1]
- [Understanding Probability Distributions][linked_blog_2]
- An extensive [list of probability distributions][dist_list_wiki].

[prob_dist_wiki]: https://en.wikipedia.org/wiki/Probability_distribution
[dice-source]: https://unsplash.com/@rihok
[dice-unsplash]: https://unsplash.com/photos/m4sGYaHYN5o
[linked_blog_1]: https://towardsdatascience.com/probability-concepts-explained-probability-distributions-introduction-part-3-4a5db81858dc
[linked_blog_2]: https://statisticsbyjim.com/basics/probability-distributions/
[dist_list_wiki]: https://en.wikipedia.org/wiki/List_of_probability_distributions

This article presents 3 tools that can be used to generate random samples from probability distributions:

### I. random

The [random][random] module is part of the *Python Standard Library*, and so is readily available. Its functions return a single value. Thus, if you wish to create a sample of desired size ***n***, you'll need to use looping techniques e.g. a *list comprehension*.

[random]: https://docs.python.org/3/library/random.html#real-valued-distributions

### II. NumPy

[NumPy][numpy] is a third-party package - it has to be [installed][np-install]. It is much beloved in *Python* because it provides objects that enable *fast operations* ([learn more][np-intro]). The [`numpy.random`][np-random] sub-module can be used to generate samples from various probability distributions.

[numpy]: https://numpy.org/
[np-install]: https://numpy.org/install/
[np-intro]: https://numpy.org/doc/stable/user/whatisnumpy.html
[np-random]: https://numpy.org/doc/stable/reference/random/index.html

### III. SciPy

[SciPy][scipy] is also a third-party package that has to be [installed][sp-install]. It is closely knit with *NumPy*. The [`scipy.stats`][sp-stats] sub-module can be used to generate samples from quite a large number of probability distributions.

[scipy]: https://scipy.org/
[sp-install]: https://scipy.org/install/
[sp-stats]: https://docs.scipy.org/doc/scipy/reference/stats.html

## Examples

What follows is a demonstration of how to create samples from the [Normal][normal], [Uniform][uniform] and [Exponential][exponential] distributions using the above tools.

> **NOTE:** You can run the examples in [this demo jupyter notebook][notebook], courtesy of [Binder][binder]:

[normal]: https://en.wikipedia.org/wiki/Normal_distribution
[uniform]: https://en.wikipedia.org/wiki/Continuous_uniform_distribution
[exponential]: https://en.wikipedia.org/wiki/Exponential_distribution
[notebook]: https://mybinder.org/v2/gh/Tim-Abwao/blog-projects/HEAD?filepath=sampling-from-probability-distributions%2FProbalility%20Distributions%20in%20Python.ipynb
[binder]: https://mybinder.org/

```python
import numpy as np
import pandas as pd
import random
import scipy
import seaborn as sns

sns.set_theme(font="serif", style="white", palette="tab10")
SAMPLE_SIZE = 5000

# For reproducability
SEED = 12345
random.seed(SEED)
numpy_gen = np.random.default_rng(SEED)


def plot_samples(distribution: str, **samples) -> None:
    """Get a layered kde-plot of the various `samples`.
    
    Args:
        distribution (str): The probability distribution sampled from.
        **samples: `dict` of samples to plot.
    """
    df = pd.DataFrame(samples)
    ax = sns.kdeplot(data=df)
    ax.set_title(
        f"{distribution.title()} Distribution Sample",
        pad=16,
        size=16,
        weight=600,
    )
    sns.despine()
```

### 1. Normal Distribution

```python
random_normal = [random.gauss(mu=0, sigma=1) for _ in range(SAMPLE_SIZE)]
numpy_normal = numpy_gen.normal(loc=0, scale=1, size=SAMPLE_SIZE)
scipy_normal = scipy.stats.norm.rvs(loc=0, scale=1, size=SAMPLE_SIZE, random_state=SEED)
plot_samples("Normal", random=random_normal, numpy=numpy_normal, scipy=scipy_normal)
```

![normal distribution sample kde-plot]({{ page.img_path | append: 'normal.png' }})

### 2. Uniform Distribution

```python
random_uniform = [random.uniform(a=0, b=1) for _ in range(SAMPLE_SIZE)]
numpy_uniform = numpy_gen.uniform(low=0, high=1, size=SAMPLE_SIZE)
scipy_uniform = scipy.stats.uniform.rvs(loc=0, scale=1, size=SAMPLE_SIZE, random_state=SEED)
plot_samples("Uniform", random=random_uniform, numpy=numpy_uniform, scipy=scipy_uniform)
```

![uniform distribution sample kde-plot]({{ page.img_path | append: 'uniform.png' }})

### 3. Exponential Distribution

```python
random_exponential = [random.expovariate(lambd=1) for _ in range(SAMPLE_SIZE)]
numpy_exponential = numpy_gen.exponential(scale=1, size=SAMPLE_SIZE)
scipy_exponential = scipy.stats.expon.rvs(scale=1, size=SAMPLE_SIZE, random_state=SEED)
plot_samples("Exponential", random=random_exponential, numpy=numpy_exponential, scipy=scipy_exponential)
```

![exponential distribution samples kde-plot]({{ page.img_path | append: 'exponential.png' }})

## Further Reading

Please see

- [Real-valued distributions][random_dist] *(random)*
- [Random Generator: Distributions][numpy_dist] *(NumPy)*
- [Statistical functions][scipy_stats] *(SciPy)*

for more probability distrbutions.

[random_dist]: https://docs.python.org/3/library/random.html#real-valued-distributions
[numpy_dist]: https://numpy.org/doc/stable/reference/random/generator.html#distributions
[scipy_stats]: https://docs.scipy.org/doc/scipy/reference/stats.html
