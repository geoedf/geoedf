PathFilter
==========

.. py:class:: GeoEDF.connector.filter.PathFilter()

   This filter accepts a string with zero or more variables and returns a fully instantiated string

   .. py:attribute:: pattern (str,required)

   This is the string input to the filter containing zero or more variables


Notes
-----

1. This is named ``PathFilter`` since it's primary use is for binding variables representing substrings in
   endpoint URLs to data products. It is really just a simple string filter that can contain zero or more
   variables which can be bound by other filters. GeoEDF will ensure that these other filters are bound first
   before instantiating those variables into the ``pattern``. 
