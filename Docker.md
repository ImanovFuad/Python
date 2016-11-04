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