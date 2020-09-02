DatetimeFilter
==============

.. py:class:: GeoEDF.connector.filter.DateTimeFilter()

   This filter is used to construct DateTime strings in a specific format for a given time period (or single date-time)
   and frequency

   .. py:attribute:: pattern (str,required)

   This is the requested pattern for the returned DateTime values. Any valid Python DateTime `format`_ string can
   be provided.

   .. py:attribute:: start (str, required)

   This is the start date entered in the standard MM/DD/YY or MM/DD/YY h:m:s formats. Whenever time is entered, the
   ``has_time`` attribute also needs to be set.

   .. py:attribute:: has_time (bool, conditional)

   This attribute is optional unless the time has also been provided along with the date.

   .. py:attribute:: end (str, optional)

   This is the end date for which filter outputs need to be generated. It needs to be entered in the same format as
   the ``start`` date.

   .. py:attribute:: period (str, conditional)

   This is the frequency to apply when determining all intervening datetimes between the start and end date. The filter
   returns datetime strings encoded as ``pattern`` for each of these intervening datetimes. The period needs to follow
   the Pandas datetime frequency `aliases`_. For example, ``2M`` is a period of 2 months, ``Y`` is a yearly period.
    
Notes
-----

1. This filter has several attributes that are ``conditionally required``. When an end date is provided, the
   period also needs to be provided. If the start date includes a time component, the ``has_time`` attribute
   needs to be set.

2. If only a start date is provided, the filter simply returns a single value, formatting the start date with
   the provided pattern.

3. If the start date includes a time component and an end date is provided, it too needs to include a time component.


.. _format: https://docs.python.org/3/library/datetime.html#strftime-strptime-behavior
.. _aliases: https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html#timeseries-offset-aliases
