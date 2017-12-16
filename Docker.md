# Ubuntu

You can run a Docker container mounting the latest PyOWM release code with:
```shell
$ docker run -d --name pyowm csparpa/pyowm
```

(you can check on [DockerHub for older tags](https://hub.docker.com/r/csparpa/pyowm/tags))

The source code is under `/pyowm` inside the container.

You can globally install PyOWM on the container with:

```shell
$ docker exec -ti pyowm bash -c 'pip install pyowm'
```

# Alpine


Build a single image with its specific Dockerfile:
```shell
docker build  . -f Dockerfile.alpine-py2 -t csparpa/pyowm.alpine-py2
```

Or build all dockerfiles:

```shell
cd scripts && ./generate_alpine_docker_images.sh
```

Use the sample `get_temperatur.py` script to test it:

```shell
# docker run csparpa/pyowm.alpine-py2 get_temperature.py -k your_api_key -p "Omsk"
Using key your_api_key to query temperature in "Omsk"...
Coordinates of Omsk: lon=73.4 lat=55.0
Temperature at 2017-12-11 20:00:00: -12.0C
```