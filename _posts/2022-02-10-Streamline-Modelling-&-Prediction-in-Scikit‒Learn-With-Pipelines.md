---
tags: machine-learning scikit-learn
---

It's always fascinating watching a well orchestrated production line at work ([How It's Made][how-made]). Raw materials go in, *magic happens*, and something wonderful comes out the other end. Such elegant efficiency can, and does exist in *machine learning* too.

![A doughnut production line](/assets/images/articles/scikit-learn-pipelines/production-line.jpg)
*(Image by Neil T, [Wikimedia Commons][wiki-image])*

Raw data is often messy, and needs to be pre-processed. Most models expect input data to be numeric, with no missing values. Some models require input data to be [normalized][normalize]. So far, that's three steps (*encoding categorical features*, *imputing blanks* and *normalization*).

[Pipelines][pipeline] *"sequentially apply a list of transformations"*. They allow you to pool all the pre-processing steps and a predictor into one object ‒ a production line of sorts.

Pipelines:

- Prevent [data leakage][data-leakage]:
  - There is much less risk of mixing up training and validation datasets.
- Are convenient and efficient:
  - You don't have to complicate things by nesting several transformers, or using intermediate variables after each transformation.
  - You don't have to process new data when making predictions.

## A Simple Example

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/Tim-Abwao/blog-projects/HEAD?filepath=scikit-learn-pipelines/pipelines.ipynb)

Consider a case where we wish to fit a [Support Vector Regressor][svr] on the [Auto MPG][auto-mpg] dataset, which has both numeric and categorical features.

One possible course of action would be to:

1. Convert categorical features to numeric
2. Standardize the features
3. Impute missing values
4. Perform a [grid-search][grid-search-cv] to get the best model

### I. Performing transformations manually

```python
column_transformer = ColumnTransformer(
    [
        ("categorical", OneHotEncoder(), make_column_selector(dtype_exclude="number")),
        ("numeric", StandardScaler(), make_column_selector(dtype_include="number")),
    ]
)
X_train_transformed = column_transformer.fit_transform(X_train)
X_test_transformed = column_transformer.transform(X_test)

imputer = SimpleImputer(strategy="mean")
X_train_imputed = imputer.fit_transform(X_train_transformed)
X_test_imputed = imputer.transform(X_test_transformed)

model = SVR()
params = {"C": np.logspace(1, 5, 5)}

best_model_without_pipeline = GridSearchCV(model, param_grid=params, cv=5, n_jobs=4)
best_model_without_pipeline.fit(X_train_imputed, y_train)
best_model_without_pipeline.score(X_test_imputed, y_test)
```

### II. Using a pipeline

```python
model_pipeline = make_pipeline(
    ColumnTransformer(
        [
            ("categorical", OneHotEncoder(), make_column_selector(dtype_exclude="number")),
            ("numeric", StandardScaler(), make_column_selector(dtype_include="number")),
        ]
    ),
    SimpleImputer(strategy="mean"),
    SVR(),
)

params = {"svr__C": np.logspace(1, 5, 5)}

best_model_with_pipeline = GridSearchCV(model_pipeline, param_grid=params, cv=5, n_jobs=4)
best_model_with_pipeline.fit(X_train, y_train)
best_model_with_pipeline.score(X_test, y_test)
```

### Making Predictions on New Data

```python
new_row = pd.DataFrame([(9, 250.0, 150.0, 4100, 11.6, 84, "usa")], columns=X.columns)

# With pipeline
prediction1 = best_model_with_pipeline.predict(new_row)

# Without pipeline
new_row_transformed = imputer.transform(column_transformer.transform(new_row))

prediction2 = best_model_without_pipeline.predict(new_row_transformed)
```

## Conclusion

This was meant to be a brief demonstration of the power of *pipelines*. You can find out more on how to make them even better in [Scikit-Learn's User Guide][pipeline-docs].

[auto-mpg]: https://archive.ics.uci.edu/ml/datasets/auto+mpg
[data-leakage]: https://en.wikipedia.org/wiki/Leakage_(machine_learning)
[grid-search-cv]: https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html
[how-made]: https://en.wikipedia.org/wiki/How_It%27s_Made
[normalize]: https://en.wikipedia.org/wiki/Normalization_(statistics)
[pipeline]: https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.Pipeline.html
[pipeline-docs]: https://scikit-learn.org/stable/modules/compose.html
[svr]: https://scikit-learn.org/stable/modules/generated/sklearn.svm.SVR.html
[wiki-image]: https://commons.wikimedia.org/w/index.php?curid=5816068>
