If you want to leverage external cache systems in combination with PyOWM, it is possible to write custom adapters for them and inject the adapters into PyOWM code.

For your convenience, you can find drafts for a few adapters in the [pyowm-cache-adapters GitHub repo](https://github.com/csparpa/pyowm-cache-adapters).

Adapters can be injected directly via an external configuration module - read how in [the usage examples relevant section](https://github.com/csparpa/pyowm/blob/master/pyowm/docs/usage-examples.md) 

An more detailed example on how to write and wire a custom adapter into the PyOWM library's code is described [here](http://csparpa.github.io/blog/2013/12/how-to-use-memcached-with-pyowm.html).