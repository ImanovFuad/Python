# Usage

Check on [DockerHub](https://hub.docker.com/r/csparpa/pyowm) the PyOWM images that are available

Choose the one you need, then run it with:

```shell
$ docker run -d --name pyowm <IMAGE-NAME>
```

The source code is under `/pyowm` inside the container.

You can globally install PyOWM on the container with:

```shell
$ docker exec -ti pyowm bash -c 'pip install pyowm'
```

# Build


Build a single image with its specific Dockerfile:

```shell
docker build  . -f dockerfiles/<the_dockerfile> -t testpyowm
```

Or build all dockerfiles:

```shell
cd scripts && ./generate_docker_images.sh
```

Use the sample `installation_test.py` script to test it:

```shell
# docker run testpyowm get_temperature.py -k your_api_key -p "Omsk"
Using key your_api_key to query temperature in "Omsk"...
Coordinates of Omsk: lon=73.4 lat=55.0
Temperature at 2017-12-11 20:00:00: -12.0C
```