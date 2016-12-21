## Table of Contents
 - [Build and pull Docker image](#docker_img)
 - [Distribution channels](#dist_channels)
 - [GitHub Wiki management](#gh_wiki)
 - [Installing multiple Python versions](#multiple_pys)
 - [Goodreads](#goodreads)
 - [Releasing](#releasing)


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

<a name="multiple_pys"></a>
## Installing multiple Python versions
On Ubuntu:
```shell
$ sudo apt-add-repository ppa:fkrull/deadsnakes
$ sudo apt-get update
$ sudo apt-get install python3.2 python 3.3
```

<a name="goodreads"></a>
## Goodreads
 - [Jeff Knupp on open sourcing a Python project the right way](http://www.jeffknupp.com/blog/2013/08/16/open-sourcing-a-python-project-the-right-way/)
 - [Guide on setuptools](https://pythonhosted.org/an_example_pypi_project/setuptools.html)
 - [Setup.py constant values reference](https://pypi.python.org/pypi?%3Aaction=list_classifiers)


<a name="releasing"></a>
## Releasing

### Checklist
* consider major, minor and patch version numbers according to SemVer
* update `constants.py`
* update `setup.py`
* update city ID files
* check for domain entities changes and update Django models on https://github.com/csparpa/django-pyowm
* update `README.md`
* update GitHub Wiki pages:
  - changelog
  - deprecations
* run tests locally using `tox` (or `setup.py` with all Python supported envs)
* update local technical docs into `docs/` folder
* generate documentation locally
* merge develop branch into master branch (no feature/hotfix branches left open)
* close milestone on GitHub
* tag release on GitHub
* generate and upload release on pypi
* push any update to Docker image on DockerHub

### Detailed steps

### Build documentation
First install Sphinx:

    $> easy_install sphinx

Then setup the docs folder: move to the main project folder and launch

    $> mkdir sphinx
    $> sphinx-apidoc -A "<authorname>" -F -o sphinx pyowm/

Sphinx will create its configuration stuff under the sphinx/ subfolder
Modify the sphinx/conf.py file by adding/uncommenting this line:

    sys.path.insert(0, os.path.abspath('..'))

Now you are ready to generate HTML docs by launching:

    $> cd sphinx/
    $> make html

HTML docs will be generated under sphinx/_build/html


### Uploading to PyPi using Twine
```shell
python2.7 setup.py sdist --format=zip  # source dist
python2.7 setup.py bdist_egg  # py27 egg
python3.2 setup.py bdist_egg  # py32 egg
python3.3 setup.py bdist_egg  # py33 egg
python3.4 setup.py bdist_egg  # py34 egg
python3.5 setup.py bdist_egg  # py35 egg
python3.6 setup.py bdist_egg  # py36 egg
twine upload dist/*           # upload to pypi
```

### Upload manually to PyPi
The following commands are to be issued using a specific Python interpreter (eg: if you launch them using Python 3.3 it will result in 3.3-compatible artifacts (.zip with sources, .egg and win installer) being uploaded to the Cheesehop.
Enter the main project directory and issue:

    $> <path-to-python-interpreter> setup.py sdist register upload  # Raw source dist
    $> <path-to-python-interpreter> setup.py bdist_egg upload       # Eggball
    $> <path-to-python-interpreter> setup.py bdist_wininst upload   # Windows .exe installer

If you don't want artifacts to be uploaded but just be created locally, omit the `upload` switch.

Some references:
 - [Guide](http://pythonhosted.org/an_example_pypi_project/setuptools.html#intermezzo-pypirc-file-and-gpg)
 - [Issue](http://stackoverflow.com/questions/1569315/setup-py-upload-is-failing-with-upload-failed-401-you-must-be-identified-t)
