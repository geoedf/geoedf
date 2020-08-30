Workflow Syntax
===============

GeoEDF workflows are constructed using a simple YAML syntax. Briefly, workflows are 
encoded as a sequence of connector or processor instances with each instance identified 
by its index in the workflow's sequence of execution. Each connector or processor instance 
is in turn expressed as a mapping of the plugin's class attributes to binding values.

A connector instance typically contains a set of connector plugins: input, filter, and output. 
Specifically, each connector instance can be composed of exactly one input or output plugin 
and zero or more filter plugins. Processor instances on the other hand are fairly straightforward; 
each processor instance consists of exactly one processor plugin. Further details of the 
syntax and special workflow bindings can be found below.

Connector Syntax
----------------

The key design principles for GeoEDF connector plugins are generality, reusability, and 
modularity. Consider the example of a data connector that seeks to download MODIS satellite 
data from a NASA DAAC. The straightforward and obvious approach would be to develop an NASA MODIS 
*input* plugin that accepts the MODIS dataset and region of interest, and downloads the data from 
the NASA DAAC using a standard FTP or HTTP request. Such a plugin would internally construct the 
direct download URL for the datasets based on the provided arguments. Generality dictates that we 
instead develop an *input* plugin that accepts a NASA DAAC FTP or HTTP direct download URL and 
downloads the data at that URL. The direct download URL can be constructed based on the specific 
NASA dataset (MODIS, SMAP, etc.) being downloaded [#f1]_. 

GeoEDF filter plugins are used to construct such attribute bindings for other plugins [#f2]_ whenever 
non-trivial temporal, spatial, or some other processing is required for the construction. For 
instance, a filter plugin may receive as input, an ESRI shapefile representing a watershed's 
boundary and return the set of MODIS grids that intersect this watershed. These grid identifiers 
are then used to construct the necessary direct download URLs for all MODIS data from the watershed's 
region. An entire attribute binding or simply portions of a binding can be constructed using a 
filter plugin. The portion that needs to be computed by a filter is specified using GeoEDF workflow 
variables, identified as ``%{var}``. Each such variable requires a corresponding filter plugin in 
the same connector instance.

Here is an example connector instance that illustrates these various syntactic elements:

.. literalinclude:: connector.yml
  :language: yaml

You will note various things here:

1. Each connector instance has separate ``Input`` and ``Filter`` sections.
2. The top-level element in the ``Input`` section is a Input plugin class name, followed by a mapping 
   of the plugin's class attributes to binding values.
3. The top-level elements in the ``Filter`` section are filter variables. Each variable is followed 
   by the actual Filter plugin class that binds that variable. Just like Input plugin instances, Filter 
   plugin instances contain a mapping of the class attributes to bindings.
4. As illustrated here, a filter can contain variables of its own (e.g. ``dtstring``), which have their 
   corresponding Filter plugin binding.
5. Note that the ``password`` attribute to ``NASAInput`` has not been provided a binding. For details of 
   the special processing undertaken for sensitive arguments such as passwords, see :ref:`special`.

A separate note on valid connector instances:

1. Variables (i.e. those bound by filters) can only be used once and need to have a name distinct from 
   any of the plugin attribute names.
2. When the value of an attribute is set to be equal to a variable, quotes need to be used; i.e. "%{var}".
   This is to avoid YAML parser errors due to the leading ``%`` character.
3. Each connector instance must have exactly one Input or Output plugin and zero or more Filter plugins.
   If a variable is present in an attribute binding, a corresponding Filter binding must be provided.

Processor Syntax
----------------

Processors are much simpler than connectors and in general do not require or cannot adhere by the generality 
and modularity principles. While these principles should be considered when developing processors corresponding 
to generic geospatial processing operations (for example, resampling, reprojection, masking, etc.); in general 
domain-specific processors may not be generalizable. A processor instance is simply an instance of a processor 
plugin specified in YAML syntax. One such example is:

.. literalinclude:: processor.yml
   :language: yaml

A couple of things of note here:

1. This processor references the output of a prior workflow stage ``$1``. The specifics of how such references 
   are bound are described in the documentation on workflow planning and execution. Suffice it to say that at 
   runtime, such references are bound to each individual file produced by the connector or processor instance in 
   the referenced workflow stage.
2. Lists (for example, ``[Lai]``) can be provided as bindings to plugin attributes as long as the plugin class 
   has been designed to expect a list there.

Workflow Syntax
---------------

Workflows are sequences of connector and processor instances where each instance is indexed by its corresponding 
workflow step number. The connector and processor instances above can be combined into a two-step workflow as 
follows:

.. literalinclude:: mcd15.yml
   :language: yaml

.. _special:
Special Workflow Bindings
-------------------------

Workflow bindings can contain certain special keywords, characters, or directives that trigger special processing.

*Sensitive Arguments:* When a binding for a plugin attribute is left empty, it is assumed that the attribute is 
sensitive and its value should not be exposed in a public workflow YAML file. At workflow execution time, the 
user is prompted to enter a value for the attribute via the Python ``getpass`` password input module. Public 
key encryption is used to transfer the value securely to the execution site.

*Stage References:* One of the central capabilities of any workflow engine is the ability to reference prior workflow 
steps and establish output-input dependencies between workflow steps. Each connector or processor instance is identified 
by a sequential workflow stage index. The output of any of these stages can be referenced in a subsequent stage by the 
``$n`` binding where ``n`` is any number smaller than the current workflow stage. 

*Dir Modifiers:* Sometimes connectors or processors need to operate on a directory of files instead of individual files. 
In such cases, the directory modifier ``dir`` can be applied to an attribute's binding. It should be noted that this 
modifier is only supported on stage references; i.e. the only valid forms of dir modifiers are ``dir(...($n)...)`` 
where one or more dir modifiers are applied in nested fashion. ``dir`` applied once is meant to refer to the containing 
directory of its argument. 

*Local Files:* Workflows often utilize files that are local to the submission machine. For instance, the processor instance 
above bound the ``shapefile`` attribute to a local file path. If a binding is determined to be a file path that exists on the 
local filesystem, then that file is transferred over to the execution host at runtime.

.. rubric:: Footnotes

.. [#f1] Most NASA DAAC direct download URLs contain the temporal and/or spatial details 
         encoded in the URL. For instance, the URL *https://e4ftl01.cr.usgs.gov/MOTA/MCD15A3H.006/2002.08.13/MCD15A3H.A2002225.h11v05.006.2015150073820.hdf*
         contains both the date, *2002.08.13* and the MODIS grid number, *h11v05* corresponding 
         to this data product. 
.. [#f2] Indeed filter plugins can be used to construct bindings for other input, filter, or output plugins.
