.. GeoEDF documentation master file, created by
   sphinx-quickstart on Fri Aug  7 00:51:05 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to GeoEDF's documentation!
==================================

GeoEDF is an extensible data framework designed to simplify data wrangling in 
geospatial research workflows. GeoEDF enables researchers to define scientific 
workflows as a logical sequence of data acquisition and processing steps. 

Reusable building blocks termed *data connectors* and *data processors* implement data acquisition 
from various repositories using various data access protocols, and a range of domain-agnostic
domain-specific geospatial processing operations respectively. 

The GeoEDF *framework* defines the syntax and semantics of connectors and processors, while 
the *engine* implements the validation, transformation, job planning, and execution of declarative 
GeoEDF workflows encoded in YAML syntax.

GeoEDF Framework
----------------

A guide to the key components of the GeoEDF framework package that help with executing data connectors and 
processors as workflow jobs in any execution environment.

.. toctree::
   :maxdepth: 1

   framework

GeoEDF Engine
-------------

A guide to the GeoEDF workflow engine that transforms *logical* GeoEDF workflows into jobs for various execution 
environments.

.. toctree::
   :maxdepth: 2

   engine

Data Connectors
---------------

.. toctree::
   :maxdepth: 3

   connectors-list

Data Processors
---------------

.. toctree::
   :maxdepth: 2

   processors-list

Development and Deployment
----------

A guide to the tools available for developing new connectors and processors, and the deployment of 
GeoEDF in a cyberinfrastructure environment. 

.. toctree::
   :maxdepth: 1

   development
   deployment

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
