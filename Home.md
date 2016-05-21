### What is PyOWM?
PyOWM is a client Python wrapper library for the OpenWeatherMap (OWM) web API.

It allows quick and easy consumption of OWM weather data from Python applications via a simple object model and in a human-friendly fashion.

PyOWM is released under the [MIT](https://github.com/csparpa/pyowm/blob/master/LICENSE) license.

PyOWM does not require any additional library to the standard Python library modules.


### Currently supported Python versions
2.7, 3.2, 3.3

### Currently supported OWM API versions
2.5

### Currently supported platforms
Windows, Linux, MacOS X

### Installation
There are many ways to install.

You can use the [pip](https://pypi.python.org/pypi/pip) installer with:  `pip install pyowm`

You can install from source with [setuptools](https://pypi.python.org/pypi/setuptools): first, download your release either from [GitHub](https://github.com/csparpa/pyowm/releases) or from the from the [Python Package Index](https://pypi.python.org/pypi/pyowm) and then install with

    unzip pywom-x.y.z
    cd pywom-x.y.z
    python setup.py install

Windows users may also install PyOWM using a specific .exe binary which is available on the [Python Package Index](https://pypi.python.org/pypi/pyowm)

### Test the codebase
Unit tests can be run by moving into the library installation folder and executing:

    python setup.py test -s tests.unit

This will run tests using your default Python interpreter (usually is 2.7).
You can test all supported Python interpreter versions using `tox`:

    tox

The full test battery can be issued by moving into the library installation folder and executing:

    python setup.py test

Be aware that this will also run integration tests (which need a valid API key to be provided and network connectivity in order to talk to the real OWM web API): therefore you will need to put your own API key inside the `pyowm.tests.functional.api_key` module


### API documentation
The library API documentation is available on [Read the Docs](https://pyowm.readthedocs.org).

### Usage examples
Usage examples are available on [the wiki page](https://github.com/csparpa/pyowm/wiki/Usage-examples).