The Official Resy Python SDK
============================

# About Resy

[Resy](http://resy.com/) is a mobile restaurant reservations app in beta on [iOS](https://itunes.apple.com/us/app/resy/id866163372?ls=1&mt=8) and [Android](https://play.google.com/store/apps/details?id=com.resy.android).  The app is for people who love eating at great restaurants but hate hassling for reservations.

The developers behind Resy are craftspeople that hold themselves and their peers to an extremely high but attainable standard for work product (code).  They ship constantly but never sacrifice code quality to meet a deadline.

The Resy application runs at AWS using python3, uWSGI, nginx, MySQL and [tinyAPI](https://github.com/mcmontero/tinyAPI).

If you're interested in working with us, please email jobs@resy.com.

## Installation

    pip3 install https://github.com/resy/developers/raw/master/python/dist/resy-0.1.tar.gz

## Obtaining an API Key

Email us at api@resy.com and we'll create one for you.

## Usage

```python
import resy

# Find some reservations.
resys = \
    resy.API('[API Key]') \
        .reservation_find(
            -73.9772046,
            40.7643304,
            '2014-11-26',  # A date no more than 10 days in the future.
            2
        )

# Get a list of all active venues.
venues = resy.API('[API Key]').venues()

# Get a list of active venues in a specific market.
venues = resy.API('[API Key]').venues('ny')
```
