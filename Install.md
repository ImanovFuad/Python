You can install PyOWM in multiple ways

## Universal installer: `pip`

As easy as:

```
pip install pyowm
```

## Install from source with `setuptools`

You can install from source using `setuptools`: either download [a release from GitHub](https://github.com/csparpa/pyowm/releases) or just take the [latest main branch](https://github.com/csparpa/pyowm/archive/master.zip)), then:

```shell
$ unzip <zip archive>   # or tar -xzf <tar.gz archive>
$ cd pyowm-x.y.z
$ python setup.py install
```
The .egg will be installed into the system-dependent Python libraries folder:

    C:\PythonXY\Lib\site-packages            # Windows
    /usr/local/lib/pythonX.Y/dist-packages   # Ubuntu
    /usr/local/lib/pythonX.Y/dist-packages   # MacOS 10.5.4

## Platform-specific installations

### Windows .exe

Windows users can get an exe installer for earlier PyOWM versions on the [Python Package Index](https://pypi.python.org/pypi/pyowm)

### On ArchLinux with `Yaourt`
Run:

```
Yaourt -S python2-owm  # Python 2.7 (https://aur.archlinux.org/packages/python-owm)
Yaourt -S python-owm   # Python 3.x (https://aur.archlinux.org/packages/python2-owm)
```

### On OpenSuse with `YaST/Zypper`
Run:

```
zypper install python-pyowm
```