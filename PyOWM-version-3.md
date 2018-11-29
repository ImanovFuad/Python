This is meant to be a **manifest** for PyOWM version 3

## Community interactions
- Ask the community to prioritize new v3 features
- Ask the community to propose new features for v3
- Ask the community help with development of support for paid OWM APIs features


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
- finalize deprecations already foreseen for v3
- dict configuration
- remove caches: pyowm won't feature any caching mechanism, that will be on the client's
- make a consistent Exceptions hierarchy and use it
- async/awaitable API calls
- HTTP/SOCKS proxies support
- installable on Linux also via `apt` and `rpm`

## Companion docs
- migration guide from V2 to V3
- remove most of the development-oriented docs: users tipically don't care about it
- add more usage-oriented snippets (eg. recipes)

## Diffs with respect v2
- removes XML schemas and XML dumps for entities
- removes JSON dumps for entities (only Python dict dumps will be allowed)
- remove all Java style getter methods (eg. `get_temperature`), so to allow Pythonic access to obj attributes
- all entities shall have methods: `__repr__`, `from_dict`, `to_dict`
- do we really need parsers when we have `from_dict` methods??? If not, these can be dropped

