ERA5Input
=========

.. py:class:: GeoEDF.connector.input.ERA5Input()

   Download ERA5 reanalysis data from the Copernicus Climate Data Store

   .. py:attribute:: uid (str,required)

   This is the uid attribute obtained by registering a user for use with the CDS API. Follow instructions at the 
   `api how to <https://cds.climate.copernicus.eu/api-how-to>`_ on registering a new user and retrieving the *uid* 
   and *api_key*.

   .. py:attribute:: api_key (str,required)

   The *api_key* is obtained along with the *uid* as described above.

   .. py:attribute:: dataset (str,optional)

   The *dataset* parameter is optional with the default value: insitu-gridded-observations-global-and-regional

   .. py:attribute:: format (str,optional)

   The *format* parameter is optional with the default value: zip

   .. py:attribute:: region (str,optional)

   The *regiont* parameter is optional with the default value: conus

   .. py:attribute:: origin (str,optional)

   The *origin* parameter is optional with the default value: cpc_conus

   .. py:attribute:: variable (str,optional)

   The *variable* parameter is optional with the default value: precipitation

   .. py:attribute:: time_aggregation (str,optional)

   The *time_aggregation* parameter is optional with the default value: daily

   .. py:attribute:: horizontal_aggregation (str,optional)

   The *horizontal_aggregation* parameter is optional with the default value: 0_25_x_0_25

   .. py:attribute:: year (str,optional)

   The *year* parameter is optional and can be an array of year values; the default is: ['1972','1976','1980']

   .. py:attribute:: version (str,optional)

   The *version* parameter is optional with the default value: v1.0
