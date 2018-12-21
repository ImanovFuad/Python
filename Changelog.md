What's new in Release 2.10.0
----------------------------
Notably, introducing support for **Agro API free features**!

- New features:
  - Support for [editing polygons](https://agromonitoring.com/api/polygons) (Agro API)
  - Support for [current soil data](https://agromonitoring.com/api/current-soil) (Agro API)
  - Support for [satellite imagery search, download and statistics](https://agromonitoring.com/api/images) (Agro API)
  - Support for searching current weather on cities inside a bounding box via the new `owm25.weather_at_stations_in_bbox` function
  - Now it is possible to download [Map Tiles provided by OpenWeatherMap](https://openweathermap.org/api/weathermaps) using the new dedicated `pyowm.tiles.tile_manager.TileManager` client

- Enhancements:
  - Refactored Weather API code to a dedicated package
  - Implemented an automated integration and release pipeline

- Bugfixes:
  - fixed wrong object to JSON dumping when calling `send_measurements()` on Stations API
  - relaxing hard upper limit on dependency `geojson`: from `geojson>=2.3.0,<2.4` to `geojson>=2.3.0,<3`

- Security:
  - upgraded version for dependencies `requests` and `urllib3` as known security issues were raised on them

- Python Versions Support:
  - dropped **Python 3.3** support as it has reached end of life


What's new in Release 2.9.0
---------------------------
**Python 2.7 is now officially deprecated**

Bugfixing support for it will be granted on the dedicated `v2.9-LTS` branch that will be killed off on Jan 1st, 2020

Please check out the [drop timeline](https://github.com/csparpa/pyowm/wiki/Timeline-for-dropping-Python-2.x-support) for details. 

- New features:
  - Support for [Weather Alerts](https://openweathermap.org/triggers)
  - Support for [UV Index Forecast and History](http://openweathermap.org/api/uvi)
  - Logos for the project have been introduced! :)
  - Support for Python 3.7
  - Support for [Pipfile](https://github.com/pypa/pipfile)


- Enhancements:
  - Heavily improved readthedocs documentation
  - Now PyOWM talks to OWM APIs over SSL
  - Refactored out one single consistent HTTP base client, based on [requests](http://docs.python-requests.org/en/master/)
  - Refactored UV API and Air Pollution API code to dedicated packages


- Bugfixes:
  - issue on `requests==2.19.1` incompatibility
  - now printing on console the detailed weather status (language-sensitive) instead of generic english-based weather status
  - fixed broken links in a few Markdown docs

- Deprecations introduced:
   - will be removed on 3.0.0: `OWM25.weather_at_stations_in_bbox`, `OWM25.weather_at_station`

What's new in Release 2.8.0
---------------------------
- New features:
  - introduced support for [Stations API 3.0](https://github.com/csparpa/pyowm/blob/master/pyowm/docs/stations-api-usage-examples.md)
  - new methods for `Forecaster` class: `will_have_clear`, `when_clear`, `will_be_clear_at`
  - new light Docker images based on Alpine Linux

- Enhancements:
  - In the moment `Forecast` objects are created, their `Weather` objects having reference timestamps prior to that moment are discarded (this means: you only get *real* forecasts!)
  - Introduced `requests` as only PyOWM dependency: `requests>=2.18.2,<2.19`

- Bugfixes:
  - issue on `city_id_registry` read behaviour on Windows
  - issue on parsing `Location` objects

- Deprecations introduced:
   - will be removed on 3.0.0: `forecaster.Forecaster.will_have_sun`, `forecaster.Forecaster.when_sun` and `forecaster.Forecaster.will_be_sunny_at`


What's new in Release 2.7.1
---------------------------
- New features:
  - introduced support for Sulphur Dioxide (SO2) and Nitric Dioxide (NO2): new methods `owm25.no2index_around_coords` and `owm25.so2index_around_coords`
  - implemented wind speed units specification (imperial/metric)


- Bugfixes:
  - updated weather history endpoint (was broken)
  - fix bug about data parsing at `station_at_coords` and `weather_at_station` methods
  - now the `deg` attribute is correctly parsed from 16 day forecast weather data items
  - fix bug on printing Unicode upon library exceptions
  - fix handling of `Weather` objects parsing (it was failing whenever some data wasn't provided by OWM)


- Enhancements:
  - shrinked city ID files size by 60% (via compression)
  - reported in the Wiki [a list](https://github.com/csparpa/pyowm/wiki/Community-Projects-using-PyOWM) of known projects that use PyOWM
  - integrated the [Say Thanks! hook](https://saythanks.io/to/csparpa)
  - introduced `CONTRIBUTING.md` and `CODE_OF_CONDUCT.md` files, thus welcoming GitHub's suggested best practices for building better open source communities
  - introduced installation tests
  - improved integrations tests organization and running

- **Breaking changes**:
  - OWM [decided to change](http://openweathermap.org/news/post/we-are-happy-announce-one-our-products-api-uv-index-has-got-significant-improvement) the syntax of API endpoint for fetching UV data and its format in a non-retrocompatible manner. This results into `UVIndex` object entity fields changing, as well as the corresponding OWM25 method signature (`owm25.uvindex_around_coords`).

What's new in Release 2.6.1
---------------------------
 * Bugfixes:
    - 2.6.0 was not packaging resource files (eg. city IDs text files)

What's new in Release 2.6.0
---------------------------
 * New features:
    - new method `owm25.weather_at_zip_code`
    - new methods `CityIDRegistry.ids_for` and `CityIDRegistry.locations_for`
    - introduced deprecation decorators to mark methods that will be removed/modified in future versions
    - Python 3.6 support
 * Bugfixes:
    - reverted a [breaking interface change](https://github.com/csparpa/pyowm/issues/158) wrongly released on 2.5.0
    - fixed `CityIDRegistry.id_for` and `CityIDRegistry.location_for` methods -> oh man, they were so buggy!
    - fixed a [bug on Unicode input handling](https://github.com/csparpa/pyowm/issues/143)
 * Enhancements:
    - reorganized project Wiki
    - embedded PyOWM usage examples as markdown file into the distribution package
 * Deprecations introduced:
    - will be removed on 3.0.0: `webapi25.cityidregistry.id_for` and `webapi25.cityidregistry.location_for`
    - will be modified on 3.0.0: `webapi25.owm25.get_version` and `webapi25.owm25.get_API_version`


What's new in Release 2.5.0
---------------------------
 * New features:
    - Air Pollution data API: [Carbon Monoxide endpoint](https://github.com/csparpa/pyowm/wiki/Air-Pollution-API:-Carbon-Monoxide-Index): `OWM25.coindex_around_coords`, [Ozone endpoint](https://github.com/csparpa/pyowm/wiki/Air-Pollution-API:-Ozone): `OWM25.ozone_around_coords`
    - [Ultraviolet data API](https://github.com/csparpa/pyowm/wiki/Ultra-Violet-API): `OWM25.uvindex_around_coords`
 * Bugfixes:
    - fixed `OWM25.is_API_online` method (was not working)
    - more robust support for querying data on Unicode place names
  * Enhancements: now datetime objects across all library are timezone-aware
  * [PyOWM Slack team](http://pyowm-slackin.herokuapp.com/) is live!

What's new in Release 2.4.0
---------------------------
 * New features:
    - `weather_at_ids`
    - `weather_history_at_coords`
    - introduced support for Python 3.4 and 3.5
 * Bugfixes: full support for Unicode place names
 * Enhancements:
    - datetime representation of reception/reference times in `Weather`, `Forecast`, `History` objects
    - better exception hierarchy
 * Updated city ID registry files

What's new in Release 2.3.2
---------------------------
 * Bugfix: no crashes when data about wind, snow and rain in JSON API responses are `null`

What's new in Release 2.3.1
---------------------------
 * Bugfix: always send an API key to OWM API

What's new in Release 2.3.0
---------------------------

* New feature: can now specify wether to use the pro OWM API version or not:

```
    owm = OWM(subscription_type='pro', API_key='my-pro-api-key')
```

* Better support for Python 3 on `CityIDRegistry`
* Bug fixes on parsing of humidity,  wind and visibility


What's new in Release 2.2.1
---------------------------

* Fixed bug on visibility distance parsing

What's new in Release 2.2.0
---------------------------

* New entity Station: represents a meteostation recording weather data

```
    Station(name, station_ID, station_type, status, lat, lon, distance=None, last_weather=None)
```

* New feature: search for meteostations around a lat/lon couple

```
    owm25.station_at_coords(42.4, 13.9)
```

* New feature: retrieve weather currently measured by a meteostation

```
    owm25.weather_at_station(916)
```

* New feature: retrieve weathers currently measured by meteostations within a bounding box

```
    owm25.weather_at_stations_in_bbox(lat_top_left, lon_top_left, lat_bottom_right, lon_bottom_right, cluster=False, limit=None)
```

* Can now query for weather forecasts based on geographical coordinates

```
    three_hours_forecast_at_coords(42.4, 13.9)
    daily_forecast_at_coords(42.4, 13.9, limit=4)
```

* Can now query for weather forecasts based on city ID

```
    three_hours_forecast_at_id(7768)
    daily_forecast_at_id(7768, limit=4)
```

* Support querying of extreme weather conditions in Forecaster convenience methods

```
    when_storm()
    will_have_storm()
    will_be_stormy_at()

    when_tornado()
    will_have_tornado()
    will_be_tornado_at()

    when_hurricane()
    will_have_hurricane()
    will_be_hurricane_at()
```

* Enriched `Weather` class with methods to support data fields retrieved from meteostations

```
    get_dewpoint()
    get_humidex()
    get_heatindex()
    get_visibility_distance()
```

* Now supporting Unicode strings as parameters for all PyOWM public methods

* Increased test coverage



### Release 2.0.0 ###

* Renaming of some functions in PyOWM public interface (**breaking change!**)

```
    owm25.API_online             -> owm25.is_API_online
    owm25.weather_at             -> owm25.weather_at_place
    owm25.find_weather_by_name   -> owm25.weather_at_places
    owm25.find_weather_by_coords -> owm25.weather_around_coords
    owm25.weather_history        -> owm25.weather_history_at_place
```

* Multilingual support for weather data descriptions

```
    owm = OWM(language='ru')
    obs = owm.weather_at('Moscow')
    obs.get_weather().get_detailed_status()  # "ясно"
```

* Can now retrieve current weather from city IDs

```
    owm.weather_at_id(5128581)
```

* Can now retrieve weather history from city IDs
```
    owm.weather_history_at_id(5128581)
```

* Can now do toponyms to city IDs conversions using a registry

```
    registry = owm.city_id_registry()
    registry.id_for("New York,US")  # 5128581
```

* Added more human-friendly utilities in Historian and timeutils modules
```
    Historian.max_temperature()
    Historian.max_humidity()
    Historian.max_pressure()
    Historian.max_rain()
    Historian.min_temperature()
    Historian.min_humidity()
    Historian.min_pressure()
    Historian.min_rain()
    Historian.average_temperature()
    Historian.average_humidity()
    Historian.average_pressure()
    Historian.average_rain()

    timeutils.next_week()
    timeutils.last_week()
    timeutils.next_hour()
    timeutils.last_hour()
```

* Now checking code coverage via *coveralls.io*


Older Releases
--------------
_Release 1.2.0_

* Ported to Python 3 while maintaining Python 2.7+ compatibility
* Python 2.6 is now unsupported (please update to 2.7)
* Bug fixes

_Release 1.0.0_

* Users can inject configuration when instantiating the library
* Code is now compliant to PEP-8 guidelines
* Added XMLNS support to printed XML
* Refactoring of low-level utility functions
* Bug fixes