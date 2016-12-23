
The PyOWM has a strong focus on testing: we want it to be _an open source project with industrial quality_!

## Unit tests
Unit tests aim to test the SW API of each class/module.

We make use of _monkey patching_ (which is more convenient than mocking because
Python is a dynamically typed) whenever there is the need to test the behavior
of a SW component which is bound to an external SW entity/system (ie: the parts
of the PyOWM library that call the real PyOWM web API via HTTP).

The default unit testing environment is Python's _unittest_: simple and clean enough, so no additional dependencies are needed.

Unit tests can be easily run using [Tox](http://tox.readthedocs.org) along with _py.test_. 

Running:

    $ tox

triggers unit tests execution on all Python platfoms that are supported by PyOWM.

Also, unit tests can be run with:

```shell
$ pythonX.Y setup.py test -s tests.unit`
```


### Integration tests
Export your API Key as an environment variable named `OWM_API_KEY`:

    $ export OWM_API_KEY='<your-api-key>'

and then you can run the integration tests with:

    $ cd tests/integration
    $ tox

Please note that depending on your subscription type some of the tests may be neglected, eg: if you have a free subscription tier, the test cases that invoke the OWM API to get historical weather data will fail as these data can only be retrieved using a paid account.

## Testing using Docker
[A Docker image](https://github.com/csparpa/pyowm/wiki/Docker) is available for developing/testing PyOWM.

## Continuous Integration
PyOWM is continuously built with [Travis-CI](https://travis-ci.org/csparpa/pyowm)
CI builds every time a Git push and a Github pull request are issued.

# Code coverage
Code coverage is checked on each CI build with [Coveralls.io](https://coveralls.io/r/csparpa/pyowm)
