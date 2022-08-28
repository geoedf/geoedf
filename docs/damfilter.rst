DamFilter
==========

.. py:class:: GeoEDF.connector.filter.DamFilter()

   This filter accepts a shapefile or bounding box specified as a vector of latitude and longitude pairs 
   and returns the IDs of all U.S. dams that fall within those bounds.

   .. py:attribute:: shapefile (str,optional)

   This is the path to a shapefile that defines the region of interest.

   .. py:attribute:: extent (str,optional)

   This is a comma separated list of four values representing the min and max latitudes and longitudes.


Notes
-----

1. While both the shapefile and extent parameters are optional, either one or both need to be specified.
   If both parameters are specified, the shapefile parameter takes precedence.
