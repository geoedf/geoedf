FAOInput
========

.. py:class:: GeoEDF.connector.input.FAOInput()

   Download data from the U.N. FAOSTAT database given a list of product names (keys)

   .. py:attribute:: dataset_codes (list,required)

   This is a list of dataset codes drawn from the master list in the `U.N. FAO dataset index`_.

Notes
-----

1. The FAOSTAT data is stored as zip files; this plugin will unzip the file and only retain the
   CSV file contained therein.


.. _U.N. FAO dataset index: http://fenixservices.fao.org/faostat/static/bulkdownloads/datasets_E.json
