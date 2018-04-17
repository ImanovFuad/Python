# Study of OWM Weather triggers

You can use the OWM API to create triggers, each trigger represents the check if a set of conditions are met over certain weather parameter values over certain geographic areas are met. An alert is created for each condition and you can poll the API to check if and when the alerts are met.

# OWM website reference
 - https://openweathermap.org/triggers
 - http://openweathermap.org/triggers-struct

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
  - fires: list of dict, each one reports a link to a parent's Condition obj and the current values that made the Alert fire
  - last_update: big int (UNIX), last time when the alert was updated because a condition was met
  - date: big int (UNIX), "time of the measurement meeting trigger conditions" (???)
  - coordinates: dict representing the coordinates where the condition were met

As one needs to poll for alerts being fired, it would be nice if PyOWM provided utilities to understand eg.
  - given a timestamp in the past and a named trigger, what alerts have been fired from that timestamp up to now (that would be super-useful for polling)
  - filter historic alert firing based on monitored meteo variable (eg. temperature, etc.)
  - filter historic alert firing based on inclusion of its conditions in specific geographic areas
  - more (TBD)

## Trigger

Attributes:
  - start: epoch when the trigger starts
  - end: epoch when the trigger ends
  - alerts: list of Alert objects
  - conditions: list of Condition objects
  - area: dict representing the topology where to check conditions on
  - alertChannels: list of AlertChannel objects

## AlertChannel
We don't know anything about it yet. Possibly, when you will setup a trigger you shall also specify the channels you want to be notified on: that's why it would be better to add pointer to a list of alert channels directly on the Trigger objects (the list can be empty for now)