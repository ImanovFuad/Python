## Table of Contents
 - [Build and pull Docker image](#docker_img)
 - [Distribution channels](#dist_channels)


<a name="docker_img"></a>
## Build and push Docker image

Build the image with:

```shell
cd <pyowm-root-dir>
docker build -t pyowm:latest .
```

Start containers with:
```shell
docker run -d --name pyowm pyowm
```

Run Tox tests on containers
```shell
docker exec -ti pyowm tox
```


### Releasing on DockerHub

Eg: for tagged version 2.3.1

```shell
VERSION="2.3.1"

# Build and tag
docker build -t csparpa/pyowm:${VERSION} .
docker tag csparpa/pyowm:${VERSION} csparpa/pyowm:latest

# Push to DockerHub
docker push csparpa/pyowm:${VERSION}
docker push csparpa/pyowm:latest
```

<a name="dist_channels"></a>
## Distribution channels

**AUR (ArchLinux)**
  * https://aur.archlinux.org/packages/python-owm/
  * https://wiki.archlinux.org/index.php/PKGBUILD