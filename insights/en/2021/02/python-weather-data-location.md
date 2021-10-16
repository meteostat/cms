---
topic: Developers
date: 2021-02-02
author: Christian Lamprecht
cover: https://media.meteostat.net/stock/earth-space.jpg
teaser: Meteostat's Point data enables you to obtain historical weather and climate data for any geographical location.
---

# Obtain Weather Data For Any Location With Python

We have just published the 1.1.0 release of the Meteostat Python library — and it comes with an exiting new feature! Thanks to the new Point data interface you are now able to obtain historical weather and climate data for any geographical location.

Point data provides more complete time series, as observations of multiple stations are joined together. The data output is being interpolated based on the geographical distance between the different weather stations and the reference point of the query. Additionally, Meteostat adjusts measurements based on difference in altitude.

## Example

All you need is the latest version of the Meteostat Python package:

```
pip install meteostat
```

Once you have successfully installed the package, you can start querying weather and climate data. First, you’ll need to *import some dependencies*:

```py
from datetime import datetime
from meteostat import Point, Daily
```

Then, you can specify *any period of time* using the `datetime` class. Here, we’re taking the year of 2018 as an example:

```py
start = datetime(2018, 1, 1)
end = datetime(2018, 12, 31)
```

Now you can simply specify *any geographical location* using the `Point` class. The class constructor takes three parameters:

1. Latitude
2. Longitude
3. Elevation

Let’s take Vancouver, BC as an example:

```py
vancouver = Point(49.2497, -123.1193, 70)
```

Using the `Point` we can now *query historical weather data* for the specified period of time:

```py
data = Daily(vancouver, start, end)
data = data.fetch()
```

Optionally, if you have _Matplotlib_ installed on your machine, you can *easily visualize the data output*. Remember to `import matplotlib.pyplot as plt` before running this part:

```py
data.plot(y=['tavg', 'tmin', 'tmax'])
plt.show()
```

This is the full script:

```py
# Import Meteostat library and dependencies
from datetime import datetime
import matplotlib.pyplot as plt
from meteostat import Point, Daily

# Set time period
start = datetime(2018, 1, 1)
end = datetime(2018, 12, 31)

# Create Point for Vancouver, BC
vancouver = Point(49.2497, -123.1193, 70)

# Get daily data for 2018
data = Daily(vancouver, start, end)
data = data.fetch()

# Plot line chart including average, minimum and maximum temperature
data.plot(y=['tavg', 'tmin', 'tmax'])
plt.show()
```

You can reproduce this example with a location of your choice. While some isolated places might not have a nearby weather station, most locations should be covered by our database.

For more information, please check the [documentation](https://dev.meteostat.net/python/) or head over to [GitHub](https://github.com/meteostat/meteostat-python).
