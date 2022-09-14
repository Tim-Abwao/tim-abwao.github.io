---
description: Visualizing Kenya's temperature and precipitation data to detect climate change.
tags: data-viz plotly climate
last_modified_at: 2022-07-01T16:50:00+03:00
img_path: /assets/images/articles/kenya-climate
---

With the recent surge in floods and droughts, and the constantly shifting weather patterns witnessed throughout the country; it's easy to conclude that climate change is at work here. But, does historical data back this assertion?

## Definitions & Background

**Climate** is the *average weather pattern* in a given location over a *long period of time*, usually 30 years.[^climate]

**Climate change** is *"a long-term shift in global or regional climate patterns"*.[^climate-change] It usually occurs naturally and gradually, but has been immensely accelerated by human activities such as deforestation and the use of fossil fuels.

Climate change is mainly characterised by an increase in global temperatures, commonly referred to as **Global Warming**.

This article investigates the existence (and degree) of climate change in Kenya by analysing two key indicators: *temperature* and *precipitation*. The data used in this exercise is obtained from the *World Bank Group's* [Climate Change Knowledge Portal][weather-data].

> **NOTE:** Regional information in the data is given in terms of *Provinces*, which have been subsequently replaced by *Counties*.[^kenya-counties]

## Things Are Heating Up

The average annual temperature has risen from a low of *22.54°C* in 1917 to *25.43°C* in 2020; having peaked at *25.56°C* in 2009 and 2016.

<iframe class="post-iframe-wide" title="temperature lineplot" src='{{ page.img_path }}/temp-plot.html'></iframe>

A *3°C* rise in temperatures is a serious cause for concern. Furthermore, it is projected that Kenya's average annual temperature could reach *26.57°C* by 2059.[^temp-projections]

All regions experience higher temperatures:

<iframe class="post-iframe-wide" title="temperature barplot" src='{{ page.img_path}}/temp-plot-regional.html'></iframe>

The *Central* region has been the coolest (*avg. 15.9°C*); the *North Eastern* region the hottest (*avg. 27.3°C*).

<iframe class="post-iframe-wide" title="temperature choropleth" src='{{ page.img_path}}/temp-map.html'></iframe>

## Rain... How unpredictable you've become

Precipitation in Kenya predominantly occurs in form of rain, mostly expected around *March - May (long rains)* and *October - December (short rains)*.

However, in recent years, both the onset and duration of the rainy seasons have varied greatly.

The lowest annual rainfall was recorded in 1949 (452.54mm), while the most was recorded in 2019 (1,100.16mm).

<iframe class="post-iframe-wide" title="precipitation lineplot" src='{{ page.img_path }}/precip-plot.html'></iframe>

Annual rainfall has increased in the *Nyanza*, *Rift Valley* and *Western* regions; but decreased in the rest of the regions.

<iframe class="post-iframe-wide" title="precipitation barplot" src='{{ page.img_path}}/precip-plot-regional.html'></iframe>

The *Western* region experienced the most rain (*avg. 1,506.3mm*), whereas the *North-Eastern* region has been the driest (*avg. 432.3mm*).

<iframe class="post-iframe-wide" title="precipitation choropleth" src='{{ page.img_path}}/precip-map.html'></iframe>

## Conclusion

Our assertion that Kenya's climate has changed seems to hold true. Monthly average temperatures are consistently higher in 1991-2020 than in 1961-1990, and the seasonal rain cycle fluctuates.

<iframe class="post-iframe" title="climate subplots" src='{{ page.img_path}}/climate-plot.html'></iframe>

## References

[^climate-change]: National Geographic Society. (2019, March 28). [Climate Change](https://www.nationalgeographic.org/encyclopedia/climate-change/). Encyclopedic entry from the *Resource Library*.
[^climate]: Planton, Serge (France; editor) (2013). ["Annex III. Glossary: IPCC – Intergovernmental Panel on Climate Change"](https://web.archive.org/web/20160524223615/http://www.ipcc.ch/pdf/assessment-report/ar5/wg1/WG1AR5_AnnexIII_FINAL.pdf)
[^temp-projections]: World Bank Group. [Climate Change Knowledge Portal - Mean Projections (Kenya)](https://climateknowledgeportal.worldbank.org/country/kenya/climate-data-projections)
[^kenya-counties]: Wikipedia contributors. (2021, October 4). Counties of Kenya. In Wikipedia, The Free Encyclopedia. Retrieved 14:59, November 5, 2021, from <https://en.wikipedia.org/w/index.php?title=Counties_of_Kenya&oldid=1048216077>

[weather-data]: <https://climateknowledgeportal.worldbank.org/download-data>
