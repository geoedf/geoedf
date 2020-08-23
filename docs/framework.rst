GeoEDF Framework
================

GeoEDF workflows compose together instances of connector or processor plugin classes represented in YAML syntax. 
The GeoEDF framework provides both the interface for connector and processor plugins and the necessary scripts and 
Python classes for executing these plugins as workflow jobs in a manner that is agnostic to the specific logic being 
implemented. 

Plugin attribute bindings can reference filter variables or the outputs of prior workflow stages. For example, consider 
the workflow below:

.. literalinclude:: mcd15.yml
  :language: yaml

The *NASAInput* plugin has an *url* attribute that receives bindings at runtime for the the *filename* variable. The 
*PathFilter* plugin that provides values for the *filename* variable on execution itself receives bindings for the *dtstring* 
variable at runtime. Similarly, the outputs of the connector are passed as inputs to the *HDFEOSShapefileMask* processor via 
the *$1* stage reference.

The GeoEDF engine is responsible for determining the order of execution of the plugins based on the binding references. Once a 
certain plugin is ready for execution (i.e. all its references are bound), the framework is then responsible for executing the 
plugin with the appropriate attribute bindings. The GeoEDF engine passes the YAML workflow file, plugin identifier, and key-value 
bindings for the various kinds of references (prior stage or filter variable) to a workflow job executing the top-level framework 
execution script. This framework script then performs the necessary plugin class instantiation using the attribute bindings before 
executing a standard connector or processor method. These key framework scripts and Python classes are described below.


run-workflow-stage Script
-------------------------
This is the top-level shell script that is executed in a workflow job for any connector or processor plugin. This simple script 
checks to see that sufficient arguments have been provided and then in-turn invokves a top-level connector or processor script 
based on the kind of plugin being executed. 

run-connector-plugin Script
---------------------------
This is the script used for executing any input, filter, or output connector plugin. This script is responsible for performing 
certain key pre-processing operations on the workflow job's arguments to extract bindings for certain special attributes. Two such 
attributes in the workflow example above are the *password* attribute to *NASAInput* and the *shppfile* attribute to *HDFEOSShapefileMask*.

The *password* attribute is left empty in a workflow file for security reasons; the GeoEDF engine identifies such attributes and 
prompts the user to provide a value at run-time. Furthermore, instead of transferring the raw value over the wire, public key encryption 
is used to transfer an encrypted version of such attributes which are then decrypted by this script. As part of a GeoEDF workflow's 
execution, a public-private keypair is first generated on the execution site and the public key is transferred to the submission site 
where the engine can use it for encrypting such sensitive attributes. The private key available on the execution site (in a workflow 
specific directory) is used by this script to decrypt all such sensitive attributes. One of the arguments to the workflow job is a 
JSON-formatted set of attribute-encrypted value bindings for such sensitive attributes. 

In the same workflow file above,  the *shppfile* attribute is provided the path to a file local to the submission site as its binding. 
Since the execution site typically differs from the submission site, such local files need to be transferred over to the execution site 
before executing this plugin. The Pegasus workflow management system provides a way to manage such data transfers and reference both the 
logical and physical file paths without explicitly implementing these in the GeoEDF engine. If a plugin contains such references to 
local files, a set of overrides for such attributes are provided as workflow job arguments. These overrides provide the actual physical 
filepath on the execution site. This script processes such overrides and prepares a dictionary consisting of attribute and override 
value mappings.

run-processor-plugin Script
---------------------------
This script is virtually identical to the *run-connector-plugin* script except for the indices of the workflow job arguments. Processors 
jobs typically require fewer arguments since processor instances cannot contain filter variables, and there is only one kind of processor 
plugin unlike the three kinds in connectors.

GeoEDFExecutor Class
--------------------
Both the *run-connector-plugin* and *run-processor-plugin* scripts turn over the instantiation of the plugin class and its execution to 
the *GeoEDFExecutor* class after the requisite workflow job argument preprocessing. This class is responsible for constructing an 
instance of the specific plugin class, binding the various class attributes, applying the necessary overrides, and finally executing the 
standard method implementing the plugin's business logic; i.e. the *get* method in input plugins, the *filter* method in filter plugins, 
and the *process* method in processor plugins.

An important thing to note here is the reasoning behind the standardized interface and package structure for connector and processor 
plugins. By standardizing the package structure for these plugins, we can use the Python *importlib* package to import the plugin's 
module and instantiate the plugin class to obtain a plugin class object. Once the object is obtained, the *GeoEDFExecutor* class can 
simply execute the standard method from this class object. 

GeoEDFPlugin Class
------------------
*GeoEDFPlugin* is a parent class that each connector (input, filter, or output) or processor plugin must inherit. This class 
provides the methods for binding variables or stage references in a plugin's attribute values and also helps set certain execution-time 
attributes such as the output path where the plugin must place its outputs. When the *GeoEDFExecutor* class invokes methods on the plugin 
class object that it constructs to bind variables or stage references, these inherited parent class methods are executed, providing the 
same, necessary binding logic for any plugin class that a GeoEDF contributor implements. 

Framework Package and Installation
----------------------------------
Each connector or processor plugin is installed as Python package in a Singularity container along with the framework package. This ensures 
that *GeoEDFExecutor* is able to import the plugin's module using *importlib*.

