HDFEOSShapefileMask
====================

.. py:class:: GeoEDF.processor.HDFEOSShapefileMask()

   This processor aggregates the data values from a HDF file for a given shapefile
   containing polygons. One or more subdatasets from the HDF file can be aggregated.
   The result is a new shapefile with the same features as the original with new fields
   added for each subdataset's aggregate value for a polygon feature.

   .. py:attribute:: hdffile (str,required)

   This is the input HDF file. The attribute can be a local file path or a workflow stage
   reference.

   .. py:attribute:: shapefile (str,required)

   This needs to be a local file path to an ESRI ``.shp`` shapefile.

   .. py:attribute:: datasets (list,required)

   This is a list of one or more names of subdatasets that need to be aggregated.

Notes
-----

1. This processor supports both HDF4 and HDF5, but assumes that the files are in the HDF-EOS format.

2. All processing occurs in the latitude-longitude space by reprojecting the shapefile to WGS84 and
   extracting the lat-lon for each grid cell in the HDF file. Extraction of cell lat-lon pairs for
   HDF4 files relies on the eos2dump utility.


