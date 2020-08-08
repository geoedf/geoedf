NASAInput
=========

.. py:class:: GeoEDF.connector.input.NASAInput()

   Download data from a NASA DAAC

   .. py:attribute:: url (str,required)

   This is the endpoint URL to file(s) served by a NASA DAAC or any repository that uses NASA Earthdata authentication.
   This connector supports wildcards in the URL, look below for more details on how this works. 

   .. py:attribute:: user (str,required)

   This is your login username for NASA Earthdata

   .. py:attribute:: password (str,required)

   This is your login password for NASA Earthdata

Notes
-----

1. If the ``url`` contains a ``*`` in its last segment, all files matching the wildcard string will be downloaded. 
   For example, ``https://e4ftl01.cr.usgs.gov/MOTA/MCD15A3H.006/2002.07.16/*`` will result in all files served at 
   this URL to be downloaded.
   If ``url`` were ``https://e4ftl01.cr.usgs.gov/MOTA/MCD15A3H.006/2002.07.16/MCD15A3H.*.h09v07*.hdf``, only files 
   matching the ``MCD15A3H.*.h09v07*.hdf`` pattern will be downloaded.

2. The connector uses simple HTML parsing to determine the list of files matching the wildcard entry. It is assumed that 
   navigating to the base URL i.e. ``https://e4ftl01.cr.usgs.gov/MOTA/MCD15A3H.006/2002.07.16`` above, returns a simple 
   HTML listing of ``<a href=...></a>`` elements.  
