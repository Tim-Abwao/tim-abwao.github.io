---
tags: data-viz plotly climate
last_modified_at: 2021-11-05T18:35:00+03:00
img_path: /assets/images/articles/kenya-climate
---

With the recent surge in floods and droughts, and the erratic rain patterns witnessed throughout the country; it is quite evident that climate change is at work here. But, does historical data back this assertion?

## 1. Defining Climate Change

**Climate** is the *average weather pattern* in a given location over a *long period of time*, usually 30 years[^climate].

**Climate change** is *"a long-term shift in global or regional climate patterns"*[^climate-change]. It usually occurs gradually, but has been immensely accelerated by human activities such as deforestation and the use of fossil fuels.

Climate change is mainly characterised by an increase in global temperatures, commonly referred to as *Global Warming*.

This article investigates the degree of climate change in Kenya by analysing two key indicators: *temperature* and *precipitation*.

The data used in this exercise is obtained from the *World Bank Group's* [Climate Change Knowledge Portal][weather-data].

> **NOTE:** Regional information in the data is given in terms of *Provinces*, which have been subsequently replaced by *Counties*[^kenya-counties].

## 2. Trends in Temperature

### 2.1 Annually (1901 - 2020)

The average temperature has risen from a low of *22.54°C* in 1917 to *25.43°C* in 2020; having peaked at *25.56°C* in 2009 and 2016.

<div>
    <iframe class="post-iframe-wide" title="temperature lineplot" src='{{ page.img_path }}/temp-plot.html'></iframe>
</div>

This *3°C* increase is by no means trivial. Furthermore, it is projected that Kenya's average temperature could reach *26.25°C* by 2039, and *29.25°C* by 2099.[^temp-projections]

The *Central* region has had the coolest temperatures (*avg. 15.9°C*), while the *North Eastern* region has had the hottest (*avg. 27.3°C*).

<div>
    <iframe class="post-iframe-wide" title="temperature choropleth" src='{{ page.img_path}}/temp-map.html'></iframe>
</div>

### 2.2 Periodically (1961-1990 and 1991-2020)

The average temperature has gone up in all regions, most notably in *Western* and *Rift Valley* (*+0.7°C*).

<div>
    <iframe class="post-iframe-wide" title="temperature barplot" src='{{ page.img_path}}/temp-plot-regional.html'></iframe>
</div>

|               | Temperature Gain (°C) |
| :------------ | --------------------: |
| Rift Valley   |                   0.7 |
| Western       |                   0.7 |
| Nyanza        |                  0.67 |
| Eastern       |                  0.62 |
| Central       |                   0.6 |
| Nairobi       |                  0.59 |
| North Eastern |                  0.53 |
| Coast         |                  0.51 |

## 3. Trends in Precipitation

### 3.1 Annually (1901 - 2020)

Precipitation in Kenya predominantly occurs in form of rain.

The lowest annual rainfall was recorded in 1949 (452.54mm), while the most was recorded in 2019 (1,100.16mm).

<div>
    <iframe class="post-iframe-wide" title="precipitation lineplot" src='{{ page.img_path }}/precip-plot.html'></iframe>
</div>

There is no clear upward or downward trend in annual rainfall, but the range of variation appears to have increased over the past half-century, perhaps due to floods and droughts.

The *Western* region experienced the most rain (*avg. 1,506.3mm*), whereas the *North-Eastern* region was the driest (*avg. 432.3mm*).

<div>
    <iframe class="post-iframe-wide" title="precipitation choropleth" src='{{ page.img_path}}/precip-map.html'></iframe>
</div>

### 3.2 Periodically (1961-1990 and 1991-2020)

In an interesting turn of events, the avarage annual rainfall has increased in the *Nyanza*, *Rift Valley* and *Western* regions; but decreased in the rest of the regions.

<div>
    <iframe class="post-iframe-wide" title="precipitation barplot" src='{{ page.img_path}}/precip-plot-regional.html'></iframe>
</div>

|               | Rainfall Gain (mm) |
| :------------ | -----------------: |
| Western       |              97.67 |
| Nyanza        |              59.31 |
| Rift Valley   |              19.77 |
| North Eastern |              -9.18 |
| Eastern       |              -9.88 |
| Central       |              -18.6 |
| Coast         |             -26.42 |
| Nairobi       |             -53.76 |

## Conclusion

There may seem to be hardly any differences when contrasting Kenya's climate in 1961-1990 to that in 1991-2020.

<div>
    <iframe class="post-iframe" title="climate subplots" src='{{ page.img_path}}/climate-plot.html'></iframe>
</div>

However, a closer look reveals that the monthly average temperature is consistently higher in 1991-2020 than in 1961-1990.

|      | 1961-1990 (°C) | 1991-2020 (°C) | Gain (°C) |
| :--- | -------------: | -------------: | --------: |
| Jan  |          24.87 |           25.5 |      0.63 |
| Feb  |          25.67 |          26.28 |      0.61 |
| Mar  |          26.07 |          26.74 |      0.67 |
| Apr  |          25.43 |          26.11 |      0.68 |
| May  |          24.48 |          25.05 |      0.57 |
| Jun  |          23.42 |          24.06 |      0.64 |
| Jul  |          22.86 |          23.44 |      0.58 |
| Aug  |          23.14 |          23.83 |      0.69 |
| Sep  |          23.92 |          24.59 |      0.67 |
| Oct  |           24.8 |          25.37 |      0.57 |
| Nov  |          24.54 |          25.08 |      0.54 |
| Dec  |          24.54 |          25.03 |      0.49 |

Additionally, the *October - December short-rain* season exhibits higher average rainfall now than in the past.

|      | 1961-1990 (mm) | 1991-2020 (mm) | Gain (mm) |
| :--- | -------------: | -------------: | --------: |
| Jan  |          31.99 |          36.05 |      4.06 |
| Feb  |             29 |          26.87 |     -2.13 |
| Mar  |          61.54 |          61.08 |     -0.46 |
| Apr  |         139.57 |         122.95 |    -16.62 |
| May  |          91.72 |          86.64 |     -5.08 |
| Jun  |          36.51 |          36.28 |     -0.23 |
| Jul  |          31.79 |          31.28 |     -0.51 |
| Aug  |          30.83 |          32.85 |      2.02 |
| Sep  |          30.48 |          29.62 |     -0.86 |
| Oct  |          60.56 |          70.87 |     10.31 |
| Nov  |         103.65 |         107.02 |      3.37 |
| Dec  |          51.14 |          57.61 |      6.47 |

Kenya's climate has changed, and is still changing.

## References

[^climate-change]: National Geographic Society. (2019, March 28). [Climate Change](https://www.nationalgeographic.org/encyclopedia/climate-change/). Encyclopedic entry from the *Resource Library*.
[^climate]: Planton, Serge (France; editor) (2013). ["Annex III. Glossary: IPCC – Intergovernmental Panel on Climate Change"](https://web.archive.org/web/20160524223615/http://www.ipcc.ch/pdf/assessment-report/ar5/wg1/WG1AR5_AnnexIII_FINAL.pdf)
[^temp-projections]: World Bank Group. [Climate Change Knowledge Portal - Mean Projections (Kenya)](https://climateknowledgeportal.worldbank.org/country/kenya/climate-data-projections)
[^kenya-counties]: Wikipedia contributors. (2021, October 4). Counties of Kenya. In Wikipedia, The Free Encyclopedia. Retrieved 14:59, November 5, 2021, from <https://en.wikipedia.org/w/index.php?title=Counties_of_Kenya&oldid=1048216077>

[weather-data]: <https://climateknowledgeportal.worldbank.org/download-data>
