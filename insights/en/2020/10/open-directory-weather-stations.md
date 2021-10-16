---
topic: Meteostat
date: 2020-10-08
author: Christian Lamprecht
cover: https://media.meteostat.net/stock/fall-trail.jpg
teaser: Meteostat launches a list of public weather stations everyone can edit and share.
---

# Let’s Build an Open Directory of Weather Stations

Today, Meteostat takes the next step in the effort of making meteorological data open and accessible for everyone. We are launching a [GitHub repository](https://github.com/meteostat/weather-stations) which serves the purpose of collecting information about public weather stations worldwide. From now on, everyone is able to download and contribute to the full list of weather stations available via Meteostat.

![A trail in fall.](https://media.meteostat.net/stock/fall-trail.jpg)

## Contributing

If you want to add a new weather station, update some information or correct an error, you can either correct/update the affected file(s) & create a pull request or [fill an issue](https://github.com/meteostat/weather-stations/issues/new) & describe your concern. Your pull requests will be reviewed by the Meteostat team. Once they are merged into the `master` branch your changes will be visible in all Meteostat products within a few days.

Essentially, every weather station is represented by a simple JSON file. Let’s take the weather station at John F. Kennedy airport as an example. You can view the JSON file [here](https://github.com/meteostat/weather-stations/blob/master/stations/74486.json). It sits in the `stations` directory and contains an object. The file is named after the object’s first property: the Meteostat `id` of the weather station.

## Properties

The `name` property is an object which contains the name of the weather station in multiple languages. The English name must always be present. It is defined using the `en` property of the `name` object. You can define names in other languages by adding new properties to the `name` object. The property keys must equal the ISO-639–1 code of the respective language.

Next in line is the `country` property. That’s the ISO 3166–1 alpha-2 country code of the weather station. Same goes for the `region` property which needs to be filled with the ISO 3166–2 state or region code.

The `identifiers` object holds the weather station’s IDs as defined by organizations like the International Civil Aviation Organization (ICAO) and the World Meteorological Organization (WMO). Some of the identifiers might not be shipped in the data dumps as they are only required for Meteostat-internal communication with public data interfaces.

The `location` object is crucial. It defines coordinates through the `latitude` & `longitude` properties and also contains the station’s `elevation`.

## Data Access

Meteostat provides both a [full](https://bulk.meteostat.net/stations/full.json.gz) and a [lite](https://bulk.meteostat.net/stations/lite.json.gz) dump of its weather station directory. The collection is available under the [Creative Commons Attribution 4.0 International Public License](https://creativecommons.org/licenses/by/4.0/legalcode).
