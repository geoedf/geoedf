CSV to Header Array Format (HAR) conversion
===========================================

.. py:class:: GeoEDF.processor.CSV2HAR()

   This processor converts a comma separated value (CSV) file into a Header Array Format (HAR) 
   file that is used by the GEMPACK software. 

   .. py:attribute:: csvfile (str,required)

   This is the path to a csvfile that needs to be converted into a HAR file

Notes
-----

1. This processor only works with CSV files produced by the `SimpleDataClean` processor. It assumes that there 
   are two columns in the CSV file: *region* and *value*; where *region* is a world region code and *value* is 
   the aggregate value for this region.
