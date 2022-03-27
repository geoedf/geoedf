WQPMap
========

.. py:class:: GeoEDF.processor.WQPMap()

   Create an interactive standalone map (HTML/JS) using data from a USGS NLDI and EPA Water Quality Portal (WQP)

   .. py:attribute:: nwis_site (str,required)

   The USGS Gage Station Identifier 
   
   .. py:attribute:: um_dist (int,optional)

   The distance (km) from USGS Station that defines upstream extent of stream reach 
   
   .. py:attribute:: ud_dist (int,optional)

   The distance (km) from USGS Station that defines downstream extent of stream reach 

   .. py:attribute:: begin_date (str,optional)

   The earliest Activity Begin Date (MM-DD-YYYY)
   
   .. py:attribute:: end_date (str,optional)

   The latest Activity End Date (MM-DD-YYYY)
   
   .. py:attribute:: ignore_wqp_dates (boolean,optional)

   Flag to denote whether to ignore date range for WQP data

   
Notes
-----

1. The generated file contains only HTML and JavaScript, and is capable of running standalone in a browser.
2. If um_dist and/or dm_dist are not given they will be set to 50km and 25km, respectively.
3. If no begin_date is given, it will be set to Jan 1 of two years prior to the current year.
4. If no end_date is give, it will be set to the current date.
5. If ignore_wqp_dates is True (the default), then all available data is retrieved.
