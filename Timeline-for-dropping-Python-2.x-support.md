Official support for Python 2 will be discontinued starting from January, 1st 2020

The PyOWM project has a *plan to gradually transition 2.x support to that date*

## Plan
The last PyOWM release with dual support for Python 2.x and 3.x is **release 2.9**

Release 2.9 will benefit of a "Long Term Support" (LTS) for
  - bug fixing cross-impacting 2.x-3.x code
  - fixing of 2.x specific issues

Upon release 2.9 a new branch called **`v2.9-LTS`** will be created from the master branch, and the above mentioned fixes will be then applied on such a branch

The `v2.9-LTS` branch **will not embed any new feature** and **will not be released to PyPi** (it will only be installable via git clone + `setup.py`).

The `v2.9-LTS` branch will be operated **until January, 1st 2020**. After that date, a **tag** will be made out of the branch and the branch will be closed, *therefore ending Python 2.x support forever*


## Timeline
Here is a visual representation of the timeline:

![Python 2.x support dropping timeline](http://i63.tinypic.com/34dnabo.jpg)