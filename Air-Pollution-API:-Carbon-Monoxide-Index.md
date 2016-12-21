You can query the OWM API for Carbon Monoxide (CO) measurements in the surroundings of specific geocoordinates.

Please refer to the official API docs for [CO](http://openweathermap.org/api/pollution/v1/co) data consumption for details about how the search radius is influenced by the decimal digits on the provided lat/lon values.

Queries return the latest CO Index values available since the specified
`start` date and across the specified `interval` timespan. If you don't
specify any value for `interval` this is defaulted to: `'year'`.
Eg:

  - `start='2016-07-01 15:00:00Z'` and `interval='hour'`: searches from 3 to 4 PM of day 2016-07-01
  - `start='2016-07-01'` and `interval='day'`: searches on the day 2016-07-01
  - `start='2016-07-01'` and `interval='month'`: searches on the month of July 2016
  - `start='2016-07-01'` and `interval='year'`: searches from day 2016-07-01 up to the end of year 2016

Please be aware that also data forecasts can be returned, depending on the search query.


### Querying CO index

Getting the data is easy:
```
# Get latest CO Index on geocoordinates
coi = owm.coindex_around_coords(lat, lon)

# Get available CO Index in the last 24 hours
coi = owm.coindex_around_coords(lat, lon,
    start=timeutils.yesterday(), interval='day')

# Get available CO Index in the last ...
coi = owm.coindex_around_coords(
    lat, lon,
    start=start_datetime,  # iso-8601, unix or datetime
    interval=span)         # can be: 'minute', 'hour', 'day', 'month', 'year'
```


### `COIndex` entity
`COIndex` is an entity representing a set of CO measurements on a certain geopoint.
Each CO measurement is taken at a certain air pressure value and has a VMR (Volume Mixing Ratio) value
for CO. Here are some of the methods:

```
list_of_samples = coi.get_co_samples()
location = coi.get_location()
coi.get_reference_time()
coi.get_reception_time()

max_sample = coi.get_co_sample_with_highest_vmr()
min_sample = coi.get_co_sample_with_lowest_vmr()
```

If you want to know if a COIndex refers to the future - aka: is a forecast - wth respect to the
current timestamp, then use the `is_forecast()` method