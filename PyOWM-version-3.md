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
- ~~drops legacy support for Python2 and support for Python 3.4~~
- ~~only supports py37+ (therefore also the new **py38**)~~

## Global library features
- give the `weatherapi` module exactly the same dignity as other api modules...
- ~~finalize deprecations already foreseen for v3~~
- [dict configuration](https://github.com/csparpa/pyowm/issues/248)
- ~~remove caches: pyowm won't feature any caching mechanism, that will be on the client's~~
- [ability to inject a custom Logger](https://github.com/csparpa/pyowm/issues/285)
- make a consistent Exceptions hierarchy and use it
- [async/awaitable API calls](https://github.com/csparpa/pyowm/issues/246)
- [HTTP/SOCKS proxies support](https://github.com/csparpa/pyowm/issues/233)
- [installable on Linux also via `apt` and `rpm`](https://github.com/csparpa/pyowm/issues/98)
- ~~No more Dockerfiles or Docker images~~
- ~~HTTP calls timeout is increased to 5 seconds (to allow to safely download satellite images)~~
- [rename weather forecast functions](https://github.com/csparpa/pyowm/issues/42)

## AgroAPI new features
 - [NDVI History](https://github.com/csparpa/pyowm/issues/274)
 - [Roadmap for remaining AgroAPI endpoints implementation](https://github.com/csparpa/pyowm/issues/273)

## PollutionAPI and UVIndexAPI new features
 - both will feature a Manager object, which will be instantiated by the new OWM entry point

## Companion docs
- migration guide from V2 to V3
- remove most of the development-oriented docs: users tipically don't care about it
- [add code recipes](https://github.com/csparpa/pyowm/issues/262)
- [document PyOWM 2 maintenance timeline](https://github.com/csparpa/pyowm/issues/265)

## Wiki
- Wiki pages must NOT serve as documentation sources! Therefore docs-like pages must be removed and links to them shall be replaced to links to the actual Readthedocs documentation pages

## Diffs with respect v2
- ~~write an automation script to generate boilerplate code for new entities~~
- ~~remove XML schemas and XML dumps for entities~~
- ~~remove JSON dumps for entities (only Python dict dumps will be allowed)~~
- remove all Java style getter methods (eg. `get_temperature`), so to allow Pythonic access to obj attributes
- all entities shall have methods: `__repr__`, `from_dict`, `to_dict`
- ~~do we really need parsers when we have `from_dict` methods??? If not, these can be dropped~~
- ~~clean modules style: add shebangs, file econding, order imports alphabetically~~