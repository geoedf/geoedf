Running Workflows
==================

The GeoEDF workflow engine has been deployed to the `MyGeoHub <https://mygeohub.org>`_ science gateway where users can 
design and execute workflows. Workflows on MyGeoHub are executed on Purdue University's Halstead cluster. In order to 
run a workflow on MyGeoHub, first launch the `Jupyter notebook tool <https://mygeohub.org/resources/jupyter70>`_ and 
create your workflow YML file in the Jupyter filesystem. You can then execute and monitor the status of this workflow 
using the following Python code from inside a Jupyter notebook.

.. code-block:: python
   
   import hublib.use
   %use pegasus-5.0.1
   %use geoedfengine-1.81
  
First, we import the GeoEDF workflow engine module via HUBzero's *use* library. Next, we import the necessary libraries from 
GeoEDF:

.. code-block:: python

   from geoedfengine.WorkflowEngine import WorkflowEngine
   
Finally, execute the desired workflow by specifying the workflow YML file path and a unique workflow name. The workflow name 
can then be used to monitor the status of the workflow.

.. code-block:: python
   
   WorkflowEngine.execute_workflow(<file-path>,'<workflow-name>')
   WorkflowEngine.workflow_status('<workflow-name>')
   
The *execute_workflow* method will print out the location of workflow outputs and any log files that the user can use to debug 
workflow errors. 
