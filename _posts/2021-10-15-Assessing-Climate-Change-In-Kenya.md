---
tags: dataviz time-series
last_modified_at: 2021-10-15T16:32:00+03:00
img_path: /assets/images/articles/kenya-climate
---

With the recent surge in floods and droughts, and the erratic rain pattern; it is quite evident that climate change is at work in Kenya.

## Climate Change

Climate change is "a long-term shift in global or regional climate patterns"[^climate-change].

Climate is the average weather pattern in a given location over a long period of time, usually 30 years[^climate].

Climate change is mainly characterised by an increase in global temperatures, and is largely due to human activities such as the use of fossil fuels.

This article investigates the degree of climate change in Kenya by analysing two indicators: *temperature* and *precipitation*.

The data used in this exercise is obtained from the *World Bank Group's* [Climate Change Knowledge Portal][weather-data].

> **NOTE:** Regional information in the data is given in terms of Provinces, which have been subsequently replaced by Counties[^kenya-counties].

## Trends in Temperature

The average temperature has risen from a low of *22.54°C* in 1917 to *25.43°C* in 2020, having peaked at *25.56°C* in 2009 and 2016.

<div>
    <iframe class="post-iframe-wide" title="temperature lineplot" src='{{ page.img_path }}/temp-plot.html'></iframe>
</div>

A *3°C* increase is by no means trivial; it strongly implies climate change.

It is projected that Kenya's average temperature could reach *26.25°C* by 2039, and *29.25°C* by 2099.[^temp-projections]

The Central region has the coolest average temperature (*15.9°C*), whereas the North-Eastern region has the hottest (*27.3°C*).

<div>
    <iframe class="post-iframe-wide" title="temperature choropleth" src='{{ page.img_path}}/temp-map.html'></iframe>
</div>

## Trends in Precipitation

Precipitation in Kenya predominantly occurs in form of rain.

The lowest annual rainfall was recorded in 1949 (452.54mm), while the most was recorded in 2019 (1100.16mm).

There is no clear upward or downward trend in annual rainfall, but the range of variation has definitely increased, perhaps as a result of the increased prevalence of droughts and floods.

<div>
    <iframe class="post-iframe-wide" title="precipitation lineplot" src='{{ page.img_path }}/precip-plot.html'></iframe>
</div>

The Western region experiences the most rain (1506.3mm), and the North-Eastern region is the driest (432.3mm).

<div>
    <iframe class="post-iframe-wide" title="precipitation choropleth" src='{{ page.img_path}}/precip-map.html'></iframe>
</div>

## Trends in Climate

There seem to be relatively few differences apparent when contrasting Kenya's climate in 1961-1990 to that in 1991-2020.

However, a deeper look reveals that the monthly average temperature is consistently higher in 1991-2020 than in 1961-1990. Additionally, the October - December short-rain season exhibits higher average rainfall now than in the past.

<div>
    <iframe class="post-iframe" title="climate subplots" src='{{ page.img_path}}/climate-plot.html'></iframe>
</div>

Kenya's climate has changed, and is still changing.

## References

[^climate-change]: <https://www.nationalgeographic.org/encyclopedia/climate-change/>
[^climate]: Planton, Serge (France; editor) (2013). ["Annex III. Glossary: IPCC – Intergovernmental Panel on Climate Change"](https://web.archive.org/web/20160524223615/http://www.ipcc.ch/pdf/assessment-report/ar5/wg1/WG1AR5_AnnexIII_FINAL.pdf)
[^temp-projections]: <https://climateknowledgeportal.worldbank.org/country/kenya/climate-data-projections>
[^kenya-counties]: <https://en.wikipedia.org/wiki/Counties_of_Kenya>

[weather-data]: https://climateknowledgeportal.worldbank.org/download-data
