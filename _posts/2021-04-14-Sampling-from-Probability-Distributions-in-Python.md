---
tags: probability scipy
last_modified_at: 2022-07-02T23:43:00+00:00
img_path: /assets/images/articles/probability-distributions/
---

A probability distribution is *"the mathematical function that gives the probabilities(likelihood) of occurrence of different possible outcomes for an experiment"* - [Wikipedia][prob_dist_wiki]

Probability distributions have numerous applications, some of the foremost being modelling real-life phenomena and simulating hypothetical conditions or events.

If you'd like to learn more about probability distributions, here are some resources that might interest you:

- [Probability concepts explained: probability distributions][linked_blog_1]
- [Understanding Probability Distributions][linked_blog_2]
- An extensive [list of probability distributions][dist_list_wiki].

[prob_dist_wiki]: https://en.wikipedia.org/wiki/Probability_distribution
[linked_blog_1]: https://towardsdatascience.com/probability-concepts-explained-probability-distributions-introduction-part-3-4a5db81858dc
[linked_blog_2]: https://statisticsbyjim.com/basics/probability-distributions/
[dist_list_wiki]: https://en.wikipedia.org/wiki/List_of_probability_distributions

This article demonstrates several tools that can generate random samples from probability distributions:

### I. random

The [random][random] module is part of the *Python Standard Library*, and so is readily available.

Its functions return a single value. Thus, if you wish to create a sample of desired size **n**, you'll need to use looping techniques e.g. a *list comprehension*.

[random]: https://docs.python.org/3/library/random.html#real-valued-distributions

### II. NumPy

[NumPy][numpy] is a third-party package, and has to be [installed][np-install]. It is much beloved in *Python* because it provides objects that enable *fast operations* ([learn more][np-intro]).

The [`numpy.random`][np-random] sub-module can be used to generate samples from various probability distributions.

[numpy]: https://numpy.org/
[np-install]: https://numpy.org/install/
[np-intro]: https://numpy.org/doc/stable/user/whatisnumpy.html
[np-random]: https://numpy.org/doc/stable/reference/random/index.html

### III. SciPy

[SciPy][scipy] is also a third-party package that has to be [installed][sp-install]. It is closely knit with *NumPy*.

The [`scipy.stats`][sp-stats] sub-module can be used to generate samples from probability distributions.

[scipy]: https://scipy.org/
[sp-install]: https://scipy.org/install/
[sp-stats]: https://docs.scipy.org/doc/scipy/reference/stats.html

> **NOTE:** You can run the examples in [this demo jupyter notebook][notebook], courtesy of [Binder][binder]:

[notebook]: https://mybinder.org/v2/gh/Tim-Abwao/blog-projects/HEAD?filepath=sampling-from-probability-distributions%2FProbalility%20Distributions%20in%20Python.ipynb
[binder]: https://mybinder.org/

## 1. Normal Distribution

```python
random_normal = [random.gauss(mu=0, sigma=1) for _ in range(SAMPLE_SIZE)]
numpy_normal = numpy_gen.normal(loc=0, scale=1, size=SAMPLE_SIZE)
scipy_normal = scipy.stats.norm.rvs(loc=0, scale=1, size=SAMPLE_SIZE, random_state=SEED)
plot_samples("Normal", random=random_normal, numpy=numpy_normal, scipy=scipy_normal)
```

![normal distribution sample kde-plot]({{ page.img_path | append: 'normal.png' }})

## 2. Uniform Distribution

```python
random_uniform = [random.uniform(a=0, b=1) for _ in range(SAMPLE_SIZE)]
numpy_uniform = numpy_gen.uniform(low=0, high=1, size=SAMPLE_SIZE)
scipy_uniform = scipy.stats.uniform.rvs(loc=0, scale=1, size=SAMPLE_SIZE, random_state=SEED)
plot_samples("Uniform", random=random_uniform, numpy=numpy_uniform, scipy=scipy_uniform)
```

![uniform distribution sample kde-plot]({{ page.img_path | append: 'uniform.png' }})

## 3. Exponential Distribution

```python
random_exponential = [random.expovariate(lambd=1) for _ in range(SAMPLE_SIZE)]
numpy_exponential = numpy_gen.exponential(scale=1, size=SAMPLE_SIZE)
scipy_exponential = scipy.stats.expon.rvs(scale=1, size=SAMPLE_SIZE, random_state=SEED)
plot_samples("Exponential", random=random_exponential, numpy=numpy_exponential, scipy=scipy_exponential)
```

![exponential distribution samples kde-plot]({{ page.img_path | append: 'exponential.png' }})

## Conclusion

Please see

- [Real-valued distributions][random_dist] *(random)*
- [Random Generator: Distributions][numpy_dist] *(NumPy)*
- [Statistical functions][scipy_stats] *(SciPy)*

for more probability distrbutions.

[random_dist]: https://docs.python.org/3/library/random.html#real-valued-distributions
[numpy_dist]: https://numpy.org/doc/stable/reference/random/generator.html#distributions
[scipy_stats]: https://docs.scipy.org/doc/scipy/reference/stats.html
