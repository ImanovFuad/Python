What's new in Release 2.0.0
---------------------------

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

* Can now retrieve current weather from city IDs  weather_at_id(id=<id>)

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

* Now checking code coverage via coveralls.io


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