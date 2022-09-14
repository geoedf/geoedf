Deployment of GeoEDF on a cyberinfrastructure
=============================================

We recommend most users to use the GeoEDF workflow engine on the MyGeoHub science gateway.
If you would like to deploy your own version of GeoEDF, the recommended solution is our standalone
deployment that makes the GeoEDF workflow engine available in JupyterHub.

The standalone deployment is based on the `Zero to JupyterHub`_ approach to deploying JupyterHub in a
Kubernetes cluster. Building on top of that deployment, we replace the standard single user image with
a Docker image that comprises the GeoEDF workflow engine, HTCondor, and other necessary configuration files.

**Note:** In this deployment, all workflows will run in a HTCondor pool in the single user container. The
deployment currently does not support scalable HTCondor pools alongside the single user container.

Interested users may take a look at the `Standalone GeoEDF`_ repository for the necessary files for building
the GeoEDF-enabled single user container and configuring JupyterHub to use this Docker image.

.. _Zero to JupyterHub: https://zero-to-jupyterhub.readthedocs.io/en/latest/
.. _Standalone GeoEDF: https://github.com/geoedf/standalone-geoedf-jupyter

