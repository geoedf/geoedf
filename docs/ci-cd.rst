Continuous Integration and Deployment
=====================================

When you submit a PR of your new connector or processor plugin, it gets turned
into a Singularity container that is hosted on GeoEDF's Singularity `registry`_.

The ``recipe.hpccm`` file that you created will be used to build a Singularity recipe,
which will then be used to build a Singularity container image that is pushed to the
registry. This process happens automatically when a PR is accepted and merged through
the use of GitHub actions.

When a GeoEDF workflow references a ``published`` connector or processor plugin, this
registry is queried to fetch the container and use it for executing the workflow.


.. _registry: https://www.registry.geoedf.org
