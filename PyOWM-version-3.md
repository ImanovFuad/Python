This is meant to be a **feature manifest** for PyOWM version 3

## Supported OWM APIs
- Agro APIs
    - Polygons
    - Soil
    - Satellite Imagery
    - MORE TBD
- Weather API --> **transition to Agro weather API???**
- Stations API
- UV Index API
- Air Pollution API
- Weather Alerts API
- Map tiles


## Supported Python versions
- drops legacy support for Python2 and support for Python 3.4
- supports py35, py36, py37, **py38**

## Global library features
- dict configuration
- async/awaitable API calls
- HTTP/SOCKS proxies support
- installable on Linux also via `apt` and `rpm`

## Diffs with respect v2
- removes XML schemas and XML dumps for entities
- removes JSON dumps for entities (only Python dict dumps will be allowed)
- remove all Java style getter methods (eg. `get_temperature`), so to allow Pythonic access to obj attributes
- all entities shall have methods: `__repr__`, `from_dict`, `to_dict`

