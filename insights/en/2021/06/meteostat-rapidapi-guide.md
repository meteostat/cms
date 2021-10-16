---
topic: Developers
date: 2021-06-24
author: Christian Lamprecht
cover: https://media.meteostat.net/stock/thunderstorm.jpg
teaser: A short guide on how to use Meteostat's JSON API.
---

# An Introduction to Meteostat on RapidAPI

Meteostat provides a [JSON API](https://rapidapi.com/meteostat/api/meteostat/) which focuses on historical weather and climate data. With artificial intelligence and machine learning on the rise, meteorological time series data is becoming increasingly important. There are various use cases for weather and climate statistics. Think about predictive analytics or clarification of insurance claims due to storms. Meteostat’s goal is simple: serving as a record keeper for earth’s weather and climate.

The roots of Meteostat lie in the open source community and remain the project’s overall focus. You can find most of our code basis under the MIT license on [GitHub](https://github.com/meteostat). However, more and more people requested a flexible solution which allows developers to scale — and that’s what this API was made for.

## Station vs. Point Data

When using Meteostat for the first time you might ask yourself whether you should work with weather station or point data. Most weather APIs don’t provide records of individual weather stations. Due to its ease of use, they usually only offer model data which is queried by geo location. Meteostat does it both. Weather stations are great if you need high quality data. Especially when dealing with scientific use cases, you need to be precise. Models tend to produce weird results with local precipitation events and other regional extremes. If you really want to be sure, there is no way around actual station data.

Otherwise, if you want to get an idea of how the weather has been in a certain location without the hassle of looping through nearby weather stations, point data has you covered. Our point data endpoints automatically aggregate records provided by nearby weather stations using weighted interpolation. The response times of these endpoints tend to be a bit slower, as data is interpolated on the fly, but they are very easy to use and still give you all the benefits of Meteostat’s high-quality observation data.

*Tip*: when using point data, make sure to pass the location’s elevation using the `alt` parameter — it will improve the model’s data quality.

## Time Series & Frequencies

Meteostat provides time series with different frequencies: hourly, daily and monthly data. For shorter periods, you’ll probably want to use hourly data as it provides all the details about how the weather was throughout the day. However, when looking at longer periods, daily or monthly data might be your best bet. Keep in mind that hourly data can only be queried for a period of up to 30 days per request. Daily data has a limit of 10 years per call.

Additionally, Meteostat provides climate normals for both weather stations and geographical points. If you don’t set a specific `start` and `end` year when querying this kind of data, Meteostat will return all available reference periods for you to choose from. Climate normals are great for learning more about the typical weather at a location and provide a solid basis for the calculation of anomalies.

## Terms & Conditions

Meteostat collects data from multiple public interfaces. The [license](https://dev.meteostat.net/terms.html) offers you the freedom to build upon the material for any purpose — as long as you mention Meteostat as a source of data. However, you’re not allowed to redistribute Meteostat data for commercial purposes “as is”.

## The Road Ahead

We’re just starting to grow our infrastructure. It’s our goal to incorporate even more data sources to improve our global data coverage. As more people start to adapt our solution, we will be able to implement features like load balancers and powerful servers, leading to even better performance and stability. If you want to support Meteostat on its mission of making weather and climate data available to everyone, feel free to build some amazing stuff on top of our API. By the way, if you want to get involved, learn more about how to [contribute](https://dev.meteostat.net/contributing.html).

_Thanks for reading!_
