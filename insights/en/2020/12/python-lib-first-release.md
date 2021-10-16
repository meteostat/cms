---
topic: Developers
date: 2020-12-08
author: Christian Lamprecht
cover: https://media.meteostat.net/stock/dawn-mountains.jpg
teaser: Today we are announcing the first stable release of the Meteostat Python library on PyPI.
---

# Meteostat Python Library Reaches First Stable Release

> This article uses an outdated version of Meteostat Python. Please check the [documentation](https://dev.meteostat.net/python/) for the latest version.

Today we are announcing the first stable release of the Meteostat Python library on PyPI. With version 1.0.0, the library becomes much more mature and performant. Furthermore, future minor releases will guarantee full compatibility from version 1.0 upwards.

![Beautiful dawn in the mountains.](https://media.meteostat.net/stock/dawn-mountains.jpg)

With our Python library we wanted to build a scalable solution which allows users to analyze historical weather and climate data on a large scale — both time-wise and geographically. In contrast to the [Meteostat JSON API](https://dev.meteostat.net/api/), the library provides unlimited data access and doesn’t require users to sign up. This is made possible with the help of Cloudflare, a global CDN provider, which allows Meteostat to serve data dumps relatively fast — no matter where you are. The ability to provide large amounts of data through a flexible, open and free interface makes the Meteostat project even more suitable for data science use cases.

## Installation

The Meteostat Python package is available through [PyPI](https://pypi.org/project/meteostat/). Therefore, installing the library is as easy as running this command:

```
pip install meteostat==1.0.0
```

Once the package is installed, you can start analyzing historical weather and climate data without limits.

## Getting Started

The library features a [detailed documentation](https://dev.meteostat.net/python/) with a lot of examples and details about the library’s API. Essentially, the package provides three classes which give you access to historical weather and climate data:

* [Stations](https://dev.meteostat.net/python/stations.html): Filter available weather stations
* [Hourly](https://dev.meteostat.net/python/hourly.html): Access hourly weather data
* [Daily](https://dev.meteostat.net/python/daily.html): Access daily weather data

The `Stations` class is useful if you do not have a specific weather station ID at hand. It provides different filters for finding weather stations which are suitable for your use case. A common task is the lookup of the closest weather station to a certain geographical location. Take a look at this example:

```py
# Import Meteostat library and dependencies
from datetime import datetime
import matplotlib.pyplot as plt
from meteostat import Stations, Daily

# Set coordinates of Vancouver
lat = 49.2497
lon = -123.1193

# Set time period
start = datetime(2018, 1, 1)
end = datetime(2018, 12, 31)

# Get closest weather station to Vancouver, BC
stations = Stations()
stations = stations.nearby(lat, lon)
stations = stations.inventory('daily', (start, end))
station = stations.fetch(1)

# Get daily data for 2018 at the selected weather station
data = Daily(station, start, end)
data = data.fetch()

# Plot line chart including average, minimum and maximum temperature
data.plot(y=['tavg', 'tmin', 'tmax'])
plt.show()
```

The example prints a 2018 temperature chart for the city of Vancouver, BC using the `Daily` class. The data access does not require knowledge about the available weather stations and could easily be adapted to another location.

More examples and explanations are available in the [documentation](https://dev.meteostat.net/python/).

## Roadmap

Once the library has settled and we do have some experience with how exactly people are using it, we will proceed with adding monthly data and an interface which provides regional averages. Furthermore, on mid to long-term distance, we want to move from [Creative Commons Attribution-NonCommercial 4.0 International Public License](https://creativecommons.org/licenses/by-nc/4.0/legalcode) to a license which enables commercial usage of meteorological data.

Also, we want to focus on stabilizing what is already there and implementing additional data sources. Going forward, all coding of the project will be open sourced under the MIT license.

If you want to get involved in the development of the Meteostat Python library, are running into an issue or just want to give some feedback, please refer to the [GitHub repository](https://github.com/meteostat/meteostat-python). Also, you can support our work with a donation or by becoming a patron of Meteostat. Also, you can support our work with a [donation](https://paypal.me/meteostat) or by [becoming a patron](https://www.patreon.com/meteostat) of Meteostat.

Last but not least: a big thanks to all [users](https://github.com/meteostat/meteostat-python/network/dependents), [Stargazers](https://github.com/meteostat/meteostat-python/stargazers) and supporters of the Meteostat Python library and the overall project.

_Let’s continue to democratize weather and climate data!_
