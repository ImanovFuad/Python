# Study of OWM Weather triggers

You can use the OWM API to create triggers, each trigger represents the check if a set of conditions are met over certain weather parameter values over certain geographic areas are met. An alert is created for each condition and you can poll the API to check if and when the alerts are met.

# OWM website references
 - https://openweathermap.org/triggers
 - http://openweathermap.org/triggers-struct
 - https://medium.com/@openweathermap/the-weather-alerts-on-base-on-meteorological-data-f99cd8cb2e25

# API methods

## triggers
```
POST http://api.openweathermap.org/data/3.0/triggers
GET http://api.openweathermap.org/data/3.0/triggers
GET http://api.openweathermap.org/data/3.0/triggers/{id}
PUT http://api.openweathermap.org/data/3.0/triggers/{id}
DELETE http://api.openweathermap.org/data/3.0/triggers/{id}
```

## alerts
```
GET http://api.openweathermap.org/data/3.0/triggers/{id}/history
DELETE http://api.openweathermap.org/data/3.0/triggers/{id}/history
GET http://api.openweathermap.org/data/3.0/triggers/{id}/history/{alert_id}
DELETE http://api.openweathermap.org/data/3.0/triggers/{id}/history/{alert_id}
```

# Object model

This is the descending object model:

  - *Trigger*: collection of alerts to be met over specified areas and within a specified time frame according to specified weather params conditions
  - *Condition*: rule for matching a weather measuerment with a specified threshold
  - *Alert*: whenever a condition is met, an alert is created (or updated) and can be polled to verify when it has been met and what the actual weather param value was.
  - *Area*: geographic area over which the trigger is checked
  - *AlertChannel*: as OWM plans to add push-oriented alert channels (eg. push notifications), we need to encapsulate this into a specific class

## Area

Attributes:
  - coordinates: list of lists (each sublist representing a point)

Subtypes: Can be point, multipoint, polygon, multipolygon. Topology is set out as stated by GeoJSON.

It could be useful to forge a factory for Areas, based on eg. a library such as this one https://pypi.org/project/geojson/


## Condition

Attributes:
  - id: str, unique condition identifier
  - target_param: weather parameters to be checked. Can be: temp, pressure, humidity, wind_speed, wind_direction, clouds.
  - expression: str, operator for the comparison. Can be: $gt, $gte, $lt, $lte, $eq, $ne
  - amount: number, the comparison value

Conditions should be bound to Triggers, as they are set on Trigger instantiation.

As Conditions can be only set on a limited number of meteo variables and can be expressed only through a closed set of value comparison operators, a factory (with eg. internal enumerators) is envisioned here.

## Alert

Attributes:
  - id: str, unique alert identifier
  - trigger_id: str, link back to parent Trigger
  - met_conditions: list of dict, each one reports a link to a parent's Condition obj and the current values that made the Alert fire
  - last_update: epoch, last time when the alert has been fired
  - coordinates: dict representing the coordinates where the condition were met

## Trigger

Attributes:
  - start: epoch when the trigger starts
  - end: epoch when the trigger ends
  - alerts: list of Alert objects
  - conditions: list of Condition objects
  - area: list of dicts, each one representing a geoJSON data structure
  - alertChannels: list of AlertChannel objects

*Notes on time period*:
As per OWM documentation, *start* and *end* times are expressed with respect to the moment when you create/update the Trigger

Example 1 (using the *$after*) operator:

```
  API call                 start                           end
(validation)           $after amount                  $after amount
     X---------------------- X -----------------------------X------------>
```

Example 2 (using the *$exact*) operator:

```
  API call                 start                           end
(validation)           $exact amount                  $exact amount
     X---------------------- X -----------------------------X------------>
```

**By design, PyOWM will only allow users to specify absolute datetimes for start/end and will send them to the API using $after**

Therefore whenever given [t_start, t_end] absolute datetime/epoch values, and given the current datetime/epoch t_curr, PyOWM shall:

  1. check if t_start and t_end are not in the past; then check that t_end > t_start
  2. calculate `start = t_start - t_curr` (in milliseconds)
  3. calculate `end = t_end - t_curr` (in milliseconds)
  4. send `start` and `end` values to the Alert API


## AlertChannel
We don't know anything about it yet. Possibly, when you will setup a trigger you shall also specify the channels you want to be notified on: that's why it would be better to add pointer to a list of alert channels directly on the Trigger objects (the list can be empty for now)

# High level PyOWM API for Weather alerts

```python
from pyowm import OWM
from pyowm.utils import geo
from pyowm.alertapi30.enums import WeatherParametersEnum
from pyowm.alertapi30.trigger import Trigger
from pyowm.alertapi30.alert import Alert

owm = OWM(API_Key='blablabla')
am = owm.alert_manager()

# area
geom_1 = geo.Point(lon, lat)  # available types: Point, MultiPoint, Polygon, MultiPolygon
geom_1.geojson()
'''
{
  "type": "Point",
  "coordinates":[ lon, lat ]
}
'''
geom_2 = geo.MultiPolygon([[lon1, lat1], [lon2, lat2], [lon3, lat3], [lon1, lat1]]
                          [[lon7, lat7], [lon8, lat8], [lon9, lat9], [lon7, lat7]])

# a very nice feature: look for city ID and get its corresponding geopoint!
reg = owm.city_id_registry()
geoms = reg.geopoints_for('London', country='GB')

# ... also, add to Location class a .to_geopoint() method that returns a geo.Point instance


# condition
condition_1 = alerting.Condition('TEMPERATURE', 'GREATER_THAN', 313.15)  # kelvin
condition_2 = alerting.Condition('CLOUDS','EQUAL', 80)                   # clouds % coverage

# triggers
trigger = am.create_trigger(start_ts=1234567890, end_ts=1278654300, conditions=[condition_1, condition_2], area=[geom_1, geom_2], alert_channel=AlertChannelsEnum.OWM_API)
triggers_list = am.get_triggers()
trigger_2 = am.get_trigger('trigger_id')
am.update_trigger(trigger_2)
am.delete_trigger(trigger_2)

# alerts (retrieved from the local parent Trigger obj)
alerts_list = trigger.get_alerts()
alerts_list = trigger.get_alerts_since('2018-01-09T23:07:24Z')  # useful for polling alerts
alerts_list = trigger.get_alerts_on(WeatherParametersEnum.TEMPERATURE)
alert = trigger.get_alert('alert_id')

# alerts (retrieved from the remote API)
alerts_list_alternate = am.get_alerts_for(trigger)
alert_alternate = am.get_alert('alert_id')

am.delete_all_alerts_for(trigger)
am.delete_alert_for(trigger, alert)
```
