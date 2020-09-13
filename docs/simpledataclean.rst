SIMPLE Data Preprocessor (Part 1)
=================================

.. py:class:: GeoEDF.processor.SimpleDataClean()

   This processor preprocesses data downloaded from the U.N. FAOSTAT database to develop 
   a database for the SIMPLE model. The CSV files downloaded from FAOSTAT are filtered 
   and aggregated based on data products and world spatial regions.

   .. py:attribute:: fao_input_dir (str,required)

   This is the directory where the FAOSTAT CSV files have been downloaded to.

   .. py:attribute:: start_year (str,required)

   This is the start year for the data filtering.

   .. py:attribute:: end_year (str,required)

   This is the end year for the data filtering.

   .. py:attribute:: regsets_csv (str,optional)
   
   This is the path to a local CSV file that overrides the default set of regions to be considered 
   for the filtering and aggregation operations.

   .. py:attribute:: cropsets_csv (str,optional)
   
   This is the path to a local CSV file that overrides the default set of crops being considered for 
   the filtering and aggregation operations.

   .. py:attribute:: livestocksets_csv (str,optional)
    
   This is the path to a local CSV file that overrides the default set of livestock being considered for 
   the filtering and aggregation operations.

Notes
-----

1. This processor only works with a fixed set of FAOSTAT datasets (LandUse, Macro-statistics Key Indicators, 
   Population, Prices, Production Crops, and Production Livestock); you will need to develop your own processor 
   if you intend to work with other FAOSTAT products.

2. When using this processor in a workflow following the `FAOInput` connector, use the `dir()` modifier when 
   providing an input for the *fao_input_dir* parameter.
