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