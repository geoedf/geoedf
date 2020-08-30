GeoEDF Workflow Engine
======================

The GeoEDF workflow engine transforms *abstract* GeoEDF workflows expressed in 
YAML syntax into a sequence of *concrete* connector and processor execution jobs. 
The engine validates a given GeoEDF YAML workflow, determines connector and processor 
plugin execution order, performs data staging, and derives the necessary bindings 
for connectors and processors as they become ready for execution. 

.. toctree::
   :maxdepth: 1

   workflow-syntax
   workflow-plan-exec
