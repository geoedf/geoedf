Building and testing a new connector or processor plugin
========================================================

Develop a new connector or processor plugin following existing examples that can be
found in the `connector`_ and `processor`_ repositories. Some key points to be aware of:

1. Follow the prescribed package structure for each plugin, only changing the module and
   class name as needed.
2. Inherit the ``GeoEDFPlugin`` class and implement the appropriate class method for your
   plugin (``get``, ``filter``, or ``process``).
3. You should be able to keep the ``__init__`` method as is, except for fixing the error
   messages and required and optional parameter lists.
4. Each plugin is fashioned as a Python package. Make sure to modify the ``setup.py`` script
   to include any Python library dependencies and other static data files.
5. Each plugin is eventually turned into a Singularity container. A helpful high-level recipe
   based on NVIDIA's `HPC Container Maker`_ is provided along with each existing plugin.
   Adapt this ``recipe.hpccm`` file for your plugin. Typically, you would only need to change
   the plugin name in a few places unless your plugin requires any additional system libraries.
   Take a look at the ``OS Packages`` section in the ``HDFEOSShapefileMask`` processor's recipe
   for ideas.

Once your plugin has been developed and organized in a folder like other existing plugins, you
can and should test it before officially submitting it as a pull request (PR) to the GeoEDF repository.

Testing
-------

You can test your plugins in GeoEDF's `development environment container`_. Follow the instructions
in the ``sample-geoedf-wf/GeoEDF.ipynb`` Jupyter notebook which will walk you through the process of
building a Singularity container image of your plugin and then using it in a GeoEDF workflow. You can
use any previously published connector or processor plugin in your testing. A list of these plugins can
be found in this `documentation`_.


.. _connector: https://github.com/geoedf/connectors
.. _processor: https://github.com/geoedf/processors
.. _HPC Container Maker: https://github.com/NVIDIA/hpc-container-maker
.. _development environment container: https://github.com/geoedf/pegasus-workflow-development-environment
.. _documentation: https://geoedf.readthedocs.io/en/latest/
