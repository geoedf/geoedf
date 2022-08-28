DamFIMInput
===========

.. py:class:: GeoEDF.connector.input.DamFIMInput()

   Download flood inundation map in TIFF format from the USACE for a given U.S. dam

   .. py:attribute:: dam_id (str,required)

   This is the id of the dam that the user wants to download flood inundation maps for. These IDs can be specified 
   by the user or else derived using the DamFilter for a given region or watershed map.

   .. py:attribute:: scenarios (str,required)

   This is a list of scenarios for which flood inundation maps are sought. This can be one or more values drawn from 
   NH Non-Breach, NL Non-Breach, MH Breach 533.8 ft, SS Non-Breach, SS Breach, TAS Non-Breach, TAS Breach, MH Non-Breach 533.8 ft, 
   NH Breach, NL Breach.
