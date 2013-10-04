In the following sections you will find a brief explanation of PyOWM's object model, with detail about the classes and datastructures of interest. For a detailed description of the classes, please refer to the [SW API documentation](https://pyowm.readthedocs.org/).

### The OWM class
The _OWM_ class acts as the main library entry-point.

In order to leverage the library features, you need to import the _OWM_ class and then feed it with an API key, if you have one (read [here](http://openweathermap.org/appid) on how to obtain an API key). Of course you can change your API Key after object instantiation, if you need.

Each kind of weather query you can issue against the OWM web API is done through a correspondent method invocation on your _OWM_ object instance:

    # CURRENT WEATHER QUERYING
    * find current weather at a specific location ---> eg: owm.weather_at('London,UK')
    * find current weather at specific lon/lat ------> eg: owm.weather_at_coords(-0.107331,51.503614)           
    * find current weathers in all locations 
      with name is equal/similar to a specific name -> eg: owm.find_weather_by_name('Springfield',search='accurate')
    * find current weathers in all locations
      in the surroundings of specific lon/lat -------> eg: owm.find_weather_by_coords(-2.15, 57.0)

    # WEATHER FORECAST QUERYING
    * find 3 hours weather forecast at a specific
      location --------------------------------------> eg: owm.three_hours_forecast('Venice,IT')
    * find daily weather forecast at a specific
      location --------------------------------------> eg: owm.daily_forecast('San Francisco,US')

    # WEATHER HISTORY QUERYING
    * find weather history for a specific location --> eg: owm.weather_history('Kiev,UA')

The methods illustrated above return a single object instance (_Observation_ or _Forecast_ types) a list of instances. In all cases, it is up to the clients to handle the returned entities.

This class also tells you the PyOWM library version and the currently supported OWM web API version.

### The Location class
The _Location_ class represents a location in the world. Each instance stores the geographic name of the location, the longitude/latitude couple and the country name. These data are retrieved from the OWM web API responses' payloads.

### The Weather class
This class is a databox containing information about weather conditions in a place. Stored data include text information such as weather status (sunny/rainy/snowy/...) and numeric information such as the values of measured phyisical entities (mx/min/current temperatures, wind speed/orientation, humidity, pressure, cloud coverage, ...). 

Some types of data are grouped and stored into Python dictionaries, such as weather and temperature info.

This class also stores the reference timestamp for the weather data, that is to say the time when the data was measured.

### The Observation class
An instance of this class is returned whenever a query about currently observed weather in a location is issued (hence, its name).

The _Observation_ class binds information about weather features that are currently being observed in a specific location in the world and that are stored as a _Weather_ object instance and the details about the location, which is stored into the class as a _Location_ object instance. Both current weather and location info are obtained via OWM web API responses parsing, which done by other classes in the PyOWM library: usually this data parsing stage ends with their storage into a newly created _Observation_ instance.

When created, every _Observation_ instance is fed with a timestamp that tells when the weather observation data have been received.

When using _OWM_ class for the retrieval of currently observed weather in multiple locations, eg:

    owm.find_weather_by_name('Springfield',search='accurate')
    owm.find_weather_by_coords(-2.15, 57.0)

a list of _Observation_ instances is returned to the clients while querying of weather forecasts gives
a _Forecaster_ object:

    owm.three_hours_forecast('Venice,IT')
    owm.daily_forecast('San Francisco,US')

and querying of weather history gives a list of _Weather_ objects:

    owm.weather_history('Kiev,UA')

### The Forecast class
This class represents a weather forecast for a specific location in the world. A weather forecast is made out by location data - encapsulated by a _Location_ object - and a collection of weather conditions - a list of _Weather_ objects.

The OWM web API provides two types of forecast intervals: three hours and daily; each _Forecast_ instance has a specific fields that tells the interval of the forecast. 

_Forecast_ instances can also tell the reception timestamp for the weather forecast, that is to say the time when the forecast has been recevied from the OWM web API.

This class also provides an iterator for easily iterating over the encapsulated _Weather_ list:

	>>> fcst = owm.daily_forecast('Tokyo')
	>>> for weather in fcst:
	...   print (weather.get_reference_time(format='iso'), weather.get_status())
	('2013-09-14 14:00:00+0','Clear')
	('2013-09-14 17:00:00+0','Clear')
	('2013-09-14 20:00:00+0','Clouds')

### The Forecaster class
Instances of this class are returned by weather forecast queries such as:

    f = owm.three_hours_forecast('London')
    f = owm.daily_forecast('Buenos Aires',limit=6)

A_Forecaster_ object wraps a _Forecast_ object and provides convenience methods that makes it possible to perform complex weather forecast data queries, which could not otherwise be possible using only the _Forecast_ class interface. A central concept with this regard is the "time coverage" of the forecast, that is to say the temporal length of the forecast.

It is then possible to know when a weather forecast starts/ends, know which _Weather_ items in the forecast carry sunny/cloudy/... weather conditions, determine wether the forecast contains sunny/cloudy/... _Weather_ items or not and to obtain the closest _Weather_ item of the forecast to the time provided by the
clients.

### Utilities functions

A few packages are provided, containing utility functions that support the base PyOWM entity classes and the user:

+ **conversion utils**: conversions between temperature units and timeformats
+ **HTTP utils**: network communications with the OWM web API
+ **JSON parsing utils**: parsing of OWM web API JSON responses and objects creation
+ **time utils**: convenience time functions for library users
+ **weather utils**: searching and filtering collections of _Weather_ objects
+ **XML utls**: dump data to XML 

### Exception classes

+ **APICallError** class: raises when failures in OWM web API invocation occur
+ **APIResponseError** class: raised when HTTP error status codes occur in OWM web API responses
+ **NotFoundError** class: raised when a search for an item in a collection has no result
+ **ParseResponseError** class: raised when failures occur in parsing payload data coming from OWM web API responses