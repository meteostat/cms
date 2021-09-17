---
topic: Developers
author: Christian Lamprecht
cover: https://media.meteostat.net/stock/explore.jpg
excerpt: How to access and analyze historical weather data with Python.
---

# Analyze Historical Weather Data with Python

Just one week after the release of our open weather station directory, we are now launching an official Meteostat Python library. The library will co-exist with our JSON API and provides a more flexible interface which targets the data science community. It’s build on top of the Meteostat bulk data interface and utilizes Pandas for data analysis. We invite everyone to test the 0.1.0 version of the Meteostat Python library. If that sounds interesting to you, keep reading this article and learn how to get started.

## Installation

The Meteostat Python package is available through PyPI. Therefore, installing the library is as easy as running this command:

```
pip install meteostat==0.3.0
```

The library depends on Pandas and PyArrow. PIP will install all dependencies automatically for you. Once the package is installed you can start analysing. Thanks to Cloudflare’s CDN, Meteostat data dumps can be accessed relatively fast from anywhere. That’s why you don’t even need an API key or any other form of authentication. In fact, you can access weather and climate data without any limits from our side. However, keep in mind that the library will cache data dumps on your local drive. If you are short in storage, consider keeping an eye on the size of your cache. By default, files will be stored in the ~/.meteostat/cache directory. If you want to keep these files somewhere else, just specify the cache_dir parameter when calling any of the library’s classes.

## Example: 2018 Temperature Data for Vancouver

Enough of the preparation, let’s dive into the data. In this example we will utilize the Stations and Daily classes of the library to create a chart which visualizes the 2018 daily temperatures in Vancouver, BC. This use case is similar to the ones covered by our JSON API and is a very common task when working with weather and climate data. We do know a geographic location we want to analyze data for, but have no idea about the weather stations nearby.

Let’s import some classes & functions, first:

```
from datetime import datetime
import matplotlib.pyplot as plt
from meteostat import Stations, Daily
```

Now we can fetch a weather station which is located close to our point of interest. Simply pass a latitude and longitude to the nearby method:

```
# Get weather stations ordered by distance to Vancouver, BC
stations = Stations(lat = 49.2497, lon = -123.1193, daily = datetime(2018, 1, 1))
# Fetch closest station (limit = 1)
station = stations.fetch(1)
```

In this block we’re also specifying a daily parameter. By doing so we are making sure, that the weather station did actually provide daily statistics in 2018. It’s not required but really makes sense it this case. After calling fetch() the station variable holds a Pandas DataFrame which contains meta information about the weather station we’ve selected. This DataFrame can be passed on to the Daily class for access to the actual weather data:

```
# Get daily data for 2018 at the selected weather station
data = Daily(station, start = datetime(2018, 1, 1), end = datetime(2018, 12, 31))
# Fetch Pandas DataFrame
data = data.fetch()
```

`data` is now a Pandas DataFrame which contains one row per day (exception: time series might contain gaps). From now on, we can use Pandas methods on our DataFrame. In this example we will visualize the average, minimum and maximum temperatures in a line chart:

```
# Plot line chart including average, minimum and maximum temperature
data.plot(y = ['tavg', 'tmin', 'tmax'], kind = 'line')
# Show chart
plt.show()
```

The chart should look like that:

![2018 Temperature Data for Vancouver](https://media.meteostat.net/insights/historical-weather-python-1.png "2018 Temperature Data for Vancouver")
