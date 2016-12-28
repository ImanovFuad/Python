# Study of OWM Weather Stations API

You can use the OWM API to manage your own meteostations and to publish real weather data to the OWM API service, thus helping to improve the quality of the overall weather forecasts.
Moreover, you can get punctual and aggregated data related to your stations' measurements.

This API is still in _beta testing_.

# API methods
## Stations
```
GET http://api.openweathermap.org/data/3.0/stations
GET http://api.openweathermap.org/data/3.0/stations/{id}
POST http://api.openweathermap.org/data/3.0/stations
PUT http://api.openweathermap.org/data/3.0/stations/{id}
DELETE http://api.openweathermap.org/data/3.0/stations/{id}
```

## Measurements
```
POST http://api.openweathermap.org/data/3.0/measurements
GET http://api.openweathermap.org/data/3.0/measurements

```

# Object model
TBD

We already have an entity (`webapi25.station.Station`) representing a meteostation, it's worth of reuse.

# High-level PyOWM API
TBD