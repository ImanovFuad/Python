# Study of OWM Weather triggers

You can use the OWM API to create triggers, each trigger represents the check if a set of conditions are met over certain weather parameter values over certain geographic areas are met. An alert is created for each condition and you can poll the API to check if and when the alerts are met.

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

  - Trigger: collection of alerts to be met over specified areas and within a specified time frame according to specified weather params conditions
  - Condition: rule for matching a weather measuerment with a specified threshold
  - Alert: whenever a condition is met, an alert is created (or updated) and can be polled to verify when it has been met and what the actual weather param value was.
  - Area: geographic area over which the trigger is checked

## Area

Attributes:
  - coordinates: list of lists (each sublist representing a point)

Subtypes: Can be point, multipoint, polygon, multipolygon.
Topology is set out as stated by GeoJSON.

It could be useful to forge a factory for Areas (GeoJSON parser)


## Condition

Attributes:
  - target_param: weather parameters to be checked. Can be: temp, pressure, humidity, wind_speed, wind_direction, clouds.
  - expression: operator for the comparison. Can be: $gt, $gte, $lt, $lte, $eq, $ne
  - amount: the comparison value
  - current_value: if the condition is "live", this contains the last checked measured value for the target_param


## Alert

Attributes:
  - id: unique alert identifier
  - list of Condition objects
  - last_update: last time when the alert was updated because a condition was met
  - date: "time of the measurement meeting trigger conditions" (???)
  - coordinates: object representing the coordinates where the condition were met

## Trigger

Attributes:
  - start: epoch when the trigger starts
  - end: epoch when the trigger ends
  - alerts: list of Alert objects
  - conditions: list of Condition objects
  - area: an Area object