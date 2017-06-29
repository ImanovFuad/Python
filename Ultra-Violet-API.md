You can query the OWM API for Ultra Violet (UV) intensity data in the surroundings of
specific geocoordinates.

Please refer to the official API docs for [UV](http://openweathermap.org/api/old-uvi)
data consumption for details about how the search radius is influenced by the decimal 
digits on the provided lat/lon values.

### Querying UV index

Getting the data is easy:

```
uvi = owm.uvindex_around_coords(lat, lon)

# Get available UV Index in the last 24 hours
uvi = owm.uvindex_around_coords(lat, lon,
    start=timeutils.yesterday(), interval='day')

# Get available UV Index in the last ...
uvi = owm.uvindex_around_coords(
    lat, lon,
    start=start_datetime,  # iso-8601, unix or datetime
    interval=span)         # can be: 'minute', 'hour', 'day', 'month', 'year'
```

The query returns the latest UV Index value available since the specified
`start` date and across the specified `interval` timespan. If you don't
specify any value for `interval` this is defaulted to: `'year'`.
Eg:


  - `start='2016-07-01 15:00:00Z'` and `interval='hour'`: searches from 3 to 4 PM of day 2016-07-01
  - `start='2016-07-01'` and `interval='day'`: searches on the day 2016-07-01
  - `start='2016-07-01'` and `interval='month'`: searches on the month of July 2016
  - `start='2016-07-01'` and `interval='year'`: searches from day 2016-07-01 up to the end of year 2016

Please be aware that also data forecasts can be returned, depending on the search query.


### `UVIndex` entity
`UVIndex` is an entity representing a UV intensity measurement on a certain geopoint.
Here are some of the methods:

```
uvi.get_value()
uvi.get_reference_time()
uvi.get_reception_time()
uvi.get_exposure_risk()
```

The `get_exposure_risk()` methods returns a string estimating the risk of harm from 
unprotected sun exposure if an average adult was exposed to a UV intensity such as the on
in this measurement. [This is the source mapping](https://en.wikipedia.org/wiki/Ultraviolet_index)
for the statement.