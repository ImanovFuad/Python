## Table of Contents
 - [Build and pull Docker image](#docker_img)
 - [Distribution channels](#dist_channels)
 - [GitHub Wiki management](#gh_wiki)
 - [Release Checklist](#release)

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


<a name="gh_wiki"></a>
## GitHub Wiki management

The Wiki is handled as a Git submodule of the project.

The submodule is "mounted" under the '/wiki' folder.

These are the instructions to setup the submodule:

```shell
$ cd <PYOWM-root>
$ git submodule add https://github.com/csparpa/pyowm.wiki.git wiki
$ git submodule init
```

Clone the wiki as a submodule by running: `git submodule update --init`


<a name="release"></a>
## Release checklist
* consider major, minor and patch version numbers according to SemVer
* update constants.py
* update setup.py
* update city ID files
* check for domain entities changes and update Django models on https://github.com/csparpa/django-pyowm
* update README.md
* update github wiki pages (including changelog+deprecations) in the /wiki folder
* run tests locally using tox (or setup.py with all Python supported envs)
* generate documentation locally
* merge develop branch into master branch (no feature/hotfix branches left open)
* close milestone on github
* tag release on github
* generate and upload release on pypi
* update docker image on DockerHub