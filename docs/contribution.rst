Contributing your connector or processor
========================================

Once you have tested your plugin to make sure it functions as expected, you can then
contribute it to the official GeoEDF repository to make it available for public use.

The contribution process involves a pair of pull requests:

1. Fork the GeoEDF `connectors`_ or `processors`_ repository, add a new folder containing your
   plugin and submit a pull request.
2. Once your code PR has been accepted and merged, you need to add the official documentation for
   your plugin, aka this ReadTheDocs.
3. Fork the GeoEDF `documentation`_ repository and add a new RestructuredText document describing
   your plugin, following the existing examples in there. In order to have your entry listed in the
   top-level list of connector or processor plugins, also edit the ``input-plugins`` or ``filter-plugins``
   or ``output-plugins`` or ``processors-list`` file to add the name of the document you just created.
4. Submit a PR with your changes.

.. _connector: https://github.com/geoedf/connectors
.. _processor: https://github.com/geoedf/processors
.. _documentation: https://github.com/geoedf/geoedf

