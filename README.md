Heroku buildpack: Python
========================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for Python apps, powered by [pip](http://www.pip-installer.org/).

[![Build Status](https://secure.travis-ci.org/Bouke/heroku-buildpack-python.png?branch=master)](http://travis-ci.org/Bouke/heroku-buildpack-python)

This extends the normal Python/Django buildpack with installing the Maxmind GeoIP C Library and downloading the GeoIP City Database. Using Django, you'd only have to include the following in your settings:

    GEOIP_PATH = '/app/GeoLiteCity.dat'

Usage
-----

Example usage:

    $ ls
    Procfile  requirements.txt  web.py

    $ heroku create --stack cedar --buildpack git://github.com/Bouke/heroku-buildpack-python-geoip.git

    $ git push heroku master
    ...
    -----> Fetching custom git buildpack... done
    -----> Python app detected
    -----> No runtime.txt provided; assuming python-2.7.4.
    -----> Using Python runtime (python-2.7.4)
    -----> Installing Maxmind GeoIP C Library
           GeoIP City Database is available at: /app/GeoLiteCity.dat
    -----> Installing dependencies using Pip (1.3.1)
           Cleaning up...

You can also add it to upcoming builds of an existing application:

    $ heroku config:add BUILDPACK_URL=git://github.com/Bouke/heroku-buildpack-python-geoip.git

The buildpack will detect your app as Python if it has the file `requirements.txt` in the root. 

It will use Pip to install your dependencies, vendoring a copy of the Python runtime into your slug. 

Specify a Runtime
-----------------

You can also provide arbitrary releases Python with a `runtime.txt` file.

    $ cat runtime.txt
    python-3.3.2
    
Runtime options include:

- python-2.7.4
- python-3.3.2
- pypy-1.9 (experimental)
