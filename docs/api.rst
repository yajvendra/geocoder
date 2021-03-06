API Overview
============

.. _install:

Installation
~~~~~~~~~~~~

PyPi Install
------------

To install Geocoder, simply:

.. code-block:: bash

    $ pip install geocoder

GitHub Install
--------------

Installing the latest version from Github:

.. code-block:: bash

    $ git clone https://github.com/DenisCarriere/geocoder
    $ cd geocoder
    $ python setup.py install

Examples
~~~~~~~~

Many properties are available once the geocoder object is created.

Forward Geocoding
-----------------

.. code-block:: python

    >>> import geocoder
    >>> g = geocoder.google('Mountain View, CA')
    >>> g.geojson
    >>> g.json
    >>> g.wkt
    >>> g.osm
    ...

Reverse Geocoding
-----------------

.. code-block:: python

    >>> g = geocoder.google([45.15, -75.14], method='reverse')
    >>> g.city
    >>> g.state
    >>> g.state_long
    >>> g.country
    >>> g.country_long
    ...

House Addresses
---------------

.. code-block:: python

    >>> g = geocoder.google("453 Booth Street, Ottawa ON")
    >>> g.housenumber
    >>> g.postal
    >>> g.street
    >>> g.street_long
    ...

IP Addresses
------------

.. code-block:: python

    >>> import geocoder
    >>> g = geocoder.ip('199.7.157.0')
    >>> g = geocoder.ip('me')
    >>> g.latlng
    >>> g.city

Command Line Interface
----------------------

Basic usesage with CLI

.. code-block:: bash

    $ geocode "Ottawa, ON" --provider bing

Saving results into a file

.. code-block:: bash

    $ geocode "Ottawa, ON"  >> ottawa.geojson

Reverse geocoding with CLI

.. code-block:: bash

    $ geocode "45.15, -75.14" --provider google --method reverse

Using JQ to query out a specific attribute

.. code-block:: bash

    $ geocode "453 Booth Street" -p canadapost --output json | jq .postal

Using a Session
---------------

In case you have several addresses to encode, to use persistent HTTP connection as recommended by the request-library
http://docs.python-requests.org/en/master/user/advanced/#session-objects
you might use the following:


.. code-block:: python
    >>> with requests.Session() as session:
    >>>    berlin = geocoder.google("Ritterstr. 12, 10969 Berlin", session=session)
    >>>    ottawa = geocoder.google("453 Booth Street, Ottawa ON", session=session)
