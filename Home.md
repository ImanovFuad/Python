### What is PyOWM?
PyOWM is a client Python wrapper library for the OpenWeatherMap (OWM) web API.

It allows quick and easy consumption of OWM weather data (either observations 
and forecast) from Python applications via a simple object model.

PyOWM is released under the [MIT](https://github.com/csparpa/pyowm/blob/master/LICENSE) license.

PyOWM does not require any additional library. Only the Python 2.7+ standard library modules are required.

### Current PyOWM version
0.1

### Currently supported OWM API version
2.5

### Installation
You will need _setuptools_ installed - read [here](https://pypi.python.org/pypi/setuptools) 
how to do it. Just run (superuser privileges might be needed):

    python setup.py install

and you'll be done.

### Test the codebase
*Unit tests* can be launched by moving into the library installation folder and 
executing:

    python -m unittest discover
    
*Integration tests* can be launched by moving into the library installation folder
and executing:

    cd functional-tests
    python integration-tests.py  

Integration testing needs network connectivity in order to reach the real OWM web API.

### API documentation
The library API documentation is available on [Read the Docs](https://pyowm.readthedocs.org).

### Usage examples
Usage examples are available [here](https://github.com/csparpa/pyowm/blob/master/docs/usage-examples.md).