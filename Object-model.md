In the following sections you will find a brief explanation of PyOWM's object model, with detail about the classes and datastructures of interest. For a detailed description of the classes, please refer to the [SW API documentation](https://pyowm.readthedocs.org/).

### The OWM class
The OWM class acts as the main library entry-point.
In order to leverage the library features, you need to import the OWM class and then feed it with an API key, if you have one (read [here](http://openweathermap.org/appid) on how to obtain an API key):

    >>> from pyowm import OWM
    >>> API_key = 'G097IueS-9xN712E'
    >>> owm = OWM(API_key)
    
Of course you can change your API Key at a later time if you need:

    >>> owm.get_API_key()
    'G09_7IueS-9xN712E'
    >>> owm.set_API_key('6Lp$0UY220_HaSB45')

This class also tells you the PyOWM library version and the currently supported OWM web API version:

    >>> owm.get_version()
    '0.1'
    >>> owm.get_API_version()
    '2.5'

Each kind of weather query you can issue against the OWM web API is done through a correspondent method invocation on your _OWM_ object instance:

    # CURRENT WEATHER QUERYING
    * find current weather at a specific location ---> eg: owm.weather_at('London,UK')
    * find current weather at specific lon/lat ------> eg: owm.weather_at_coords(-0.107331,51.503614)           
    * find current weathers in all locations 
      with name is equal/similar to a specific name -> eg: owm.find_weather_by_name('NY',search='accurate')
    * find current weathers in all locations
      in the surroundings of specific lon/lat -------> eg: owm.find_weather_by_coords(-2.15, 57.0)

    # WEATHER FORECAST  QUERYING
    * find 3 hours weather forecast at a specific
      location --------------------------------------> eg: owm.three_hours_forecast('Venice,IT')
    * find daily weather forecast at a specific
      location --------------------------------------> eg: owm.daily_forecast('San Francisco,US')