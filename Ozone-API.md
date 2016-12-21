### Querying Ozone data

Getting the data is easy:
```
# Get latest O3 value on geocoordinates
o3 = owm.ozone_around_coords(lat, lon)

# Get available O3 value in the last 24 hours
oz = owm.ozone_around_coords(lat, lon,
         start=timeutils.yesterday(), interval='day')

# Get available O3 value in the last ...
oz = owm.ozone_around_coords(
       lat, lon,
        start=start_datetime,  # iso-8601, unix or datetime
        interval=span)         # can be: 'minute', 'hour', 'day', 'month', 'year'
```

### `Ozone` entity
`Ozone` is an entity representing a set of CO measurements on a certain geopoint.
Each ozone value is expressed in [Dobson Units](http://www.theozonehole.com/dobsonunit.htm).
Here are some of the methods:

```
location = oz.get_location()
oz = get_du_value()
oz.get_reference_time()
oz.get_reception_time()
```

If you want to know if an Ozone measurement refers to the future - aka: is a forecast - wth respect to the
current timestamp, then use the `is_forecast()` method