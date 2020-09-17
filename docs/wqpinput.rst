WQPInput
========

.. py:class:: GeoEDF.connector.input.WQPInput()

   Download data from a EPA Water Quality Portal (WQP)

   .. py:attribute:: site_id (str,required)

   The Station Identifier 

   .. py:attribute:: start_date (str,optional)

   The earliest Activity Start Date (MM-DD-YYYY)
   
   .. py:attribute:: end_date (str,optional)

   The latest Activity End Date (MM-DD-YYYY)

   
Notes
-----

1. The file is downloaded as CSV file.

2. If no start or end date is given all available data is retrieved .
