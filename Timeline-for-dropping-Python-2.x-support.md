Official support for Python 2 will be discontinued starting from January, 1st 2020

The PyOWM project has a *plan to gradually transition 2.x support to that date*

# tl;dr

### I use Python 2.x, do I have to worry?
  - You're OK with PyOWM **until release 2.9**
  - You will get 2.x bugfixes implemented until January, 1st 2020 and you will be able to obtain them by installing the ad-hoc `v2.9-LTS` branch
  - **From release 2.10 on, PyOWM will only work on Python 3.x**

### I use Python 2.x and I usually update PyOWM to the latest available release
If you will try to update PyOWM from a release < 2.9 to the latest available - say, via `pip` - you will get release 2.9 even if higher releases will be available (as these will only support Python 3.x)

### I use Python 2.x and will need to install PyOWM from scratch with a release higher than 2.9
That will be impossible: on Python 2.x platforms you will only be able to get PyOWM releases up to 2.9. If you then want to install the `v2.9-LTS` branch code updates, you will need to do this manually by running
```
$ pip install git+https://github.com/csparpa/pyowm.git@v2.9-LTS
```

### Q: I use Python 3.x, do I have to worry?
You wont' have any issue: 🌞 shines in the sky

# Plan
The last PyOWM release with dual support for Python 2.x and 3.x is **release 2.9**

### Release 2.9
Release 2.9 will benefit of a "Long Term Support" (LTS) for
  - bug fixing
  - fixing of 2.x specific issues

Upon release 2.9 a new branch called **`v2.9-LTS`** will be created from the master branch, and the above mentioned fixes will be then applied on such a branch

The `v2.9-LTS` branch **will not embed any new feature** and **will not be released to PyPi** (it will only be installable via `pip install git+https://github.com/csparpa/pyowm.git@v2.9-LTS` or git clone + `setup.py`).

The `v2.9-LTS` branch will be operated **until January, 1st 2020**. After that date, a **tag** will be made out of the branch and the branch will be closed, *therefore ending Python 2.x support forever*

### ... but life still goes on...
After branching out the `v2.9-LTS` branch, the `develop` branch will **remove support to Python 2.x (as part of release 2.10)**.

This means that from release 2.10 on, PyOWM will only work on Python 3.x


# Timeline
Here is a visual representation of the timeline:

![Python 2.x support dropping timeline](http://i63.tinypic.com/34dnabo.jpg)