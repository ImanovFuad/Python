Official support for Python 2 will be discontinued starting from January, 1st 2020

The PyOWM project has a *plan to gradually transition 2.x support to that date*

## tl;dr

### I use Python 2.x
  - You're OK with PyOWM **until release 2.9**.
  - You will get 2.x bugfixes implemented until January, 1st 2020 and you will be able to obtain them by installing the ad-hoc `v2.9-LTS` branch via `setup.py`
  - **From release 2.10 on, PyOWM will only work on Python 3.x**

### I use Python 3.x
You wont' have any issue: 🌞 shines in the sky

## Plan
The last PyOWM release with dual support for Python 2.x and 3.x is **release 2.9**

### Release 2.9
Release 2.9 will benefit of a "Long Term Support" (LTS) for
  - bug fixing
  - fixing of 2.x specific issues

Upon release 2.9 a new branch called **`v2.9-LTS`** will be created from the master branch, and the above mentioned fixes will be then applied on such a branch

The `v2.9-LTS` branch **will not embed any new feature** and **will not be released to PyPi** (it will only be installable via git clone + `setup.py`).

The `v2.9-LTS` branch will be operated **until January, 1st 2020**. After that date, a **tag** will be made out of the branch and the branch will be closed, *therefore ending Python 2.x support forever*

### ... but life still goes on...
After branching out the `v2.9-LTS` branch, the `develop` branch will **remove support to Python 2.x (as part of release 2.10)**.

This means that from release 2.10 on, PyOWM will only work on Python 3.x


## Timeline
Here is a visual representation of the timeline:

![Python 2.x support dropping timeline](http://i63.tinypic.com/34dnabo.jpg)