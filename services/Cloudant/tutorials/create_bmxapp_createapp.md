---

copyright:
  years: 2017
lastupdated: "2017-01-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Acrolinx: 2017-01-11 -->

# Creating a simple Bluemix application to access a Cloudant database: the code

This section of the tutorial describes the code
for an {{site.data.keyword.Bluemix}} application.
{:shortdesc}

<div id="theApp"></div>

## Creating your application

The following components are now in place,
ready to begin creating the application:

-   [The Python programming language](create_bmxapp_prereq.html#python).
-   [A {{site.data.keyword.cloudant_short_notm}} database instance](create_bmxapp_prereq.html#csi).
-   [A {{site.data.keyword.Bluemix_notm}} application environment](create_bmxapp_appenv.html#creating).
-   A [connection](create_bmxapp_appenv.html#connecting) between the {{site.data.keyword.cloudant_short_notm}} database instance
    and the {{site.data.keyword.Bluemix_notm}} application environment.
-   The [toolkits](create_bmxapp_appenv.html#toolkits) for managing Cloud Foundry-based {{site.data.keyword.Bluemix_notm}} applications.
-   A ['starter' application pack](create_bmxapp_appenv.html#starter), containing initial configuration and code template files.

>   **Note**: No attempt was made to create _efficient_ Python code for this tutorial.
    The intention is to show simple and easy-to-understand working code
    that you can learn from and apply for your own applications.
    Also,
    no attempt was made to address all possible checks or error conditions.
    Some example checks are included to illustrate some of the techniques.
    In your applications,
    check for,
    and deal with,
    all warnings or error conditions.

### Essential files

Your application requires three configuration files and one source file,
all available in the ['starter' application pack](create_bmxapp_appenv.html#starter):
 
-   ['`Procfile`'](create_bmxapp_appenv.html#procfile)
-   ['`manifest.yml`'](create_bmxapp_appenv.html#manifest)
-   ['`requirements.txt`'](create_bmxapp_appenv.html#requirements)
-   The application source file, which is described in this section of the tutorial.

Modify your configuration files as follows:

1.  Edit the '`Procfile`' file so that it contains the following text:
    ```
    web: python server.py
    ```
    {:codeblock}

2.  Edit the '`manifest.yml`' file so that it contains the following text:
    ```
    applications:
    - path: .
      memory: 128M
      instances: 1
      domain: <your domain>
      name: <your application name>
      host: <your application host>
      disk_quota: 1024M
      services:
      - <your database instance>
    ```
    {:codeblock}
    >   **Note**: Ensure that you modify the '`domain`', '`name`', '`host`', and '`services`' values. They are the values that were entered when you created your [{{site.data.keyword.Bluemix_notm}} application environment](create_bmxapp_appenv.html#creating) and your [{{site.data.keyword.cloudant_short_notm}} database instance](create_bmxapp_prereq.html#csi).

3.  Edit the '`requirements.txt`' file so that it contains the following text:
    ```
    cloudant==2.3.1
    ```
    {:codeblock}

### The application code

The next step is to work on the application code.
Each section is described and the code is presented.
A [complete listing](#complete-listing) of the application code
is at the end of this section of the tutorial.

#### Getting started

The Python application requires some basic components to function.
They are imported as follows:

```python
# Make Python modules available.
import os
import json

# It is helpful to have access to tools
# for formatting date and time values.
from time import gmtime, strftime
```
{:codeblock}

The application operates as a simple webserver,
showing only one page:
a log containing the results of connecting to the {{site.data.keyword.cloudant_short_notm}} database instance
and creating a database.

The application requires components for serving a web page:

```python
# Simplify access to basic Python web server tools.
try:
    from SimpleHTTPServer import SimpleHTTPRequestHandler as Handler
    from SocketServer import TCPServer as Server
except ImportError:
    from http.server import SimpleHTTPRequestHandler as Handler
    from http.server import HTTPServer as Server
```
{:codeblock}

>   **Note**: This code segment is provided as part of the ['starter' application pack](create_bmxapp_appenv.html#starter).

The application connects to the {{site.data.keyword.cloudant_short_notm}} database instance,
so it must import the {{site.data.keyword.cloudant_short_notm}} Library components:

```python
# Enable the required Python libraries for working with Cloudant.
from cloudant.client import Cloudant
from cloudant.error import CloudantException
from cloudant.result import Result, ResultByKey
```
{:codeblock}

The application creates a database within the {{site.data.keyword.cloudant_short_notm}} database instance.
A name is required for the database:

```python
# This is the name of the database we intend to create.
databaseName = "databasedemo"
```
{:codeblock}

The application records progress as it connects to the
{{site.data.keyword.cloudant_short_notm}} database instance
and creates the database.
The record takes the form of a log file,
which is stored in a folder accessible by the Python web server.

Create a folder (called '`static`' in the application),
and get ready to store a file in it:

```python
# Change current directory to avoid exposure of control files
try:
    os.mkdir('static')
except OSError:
    # The directory already exists,
    # no need to create it.
    pass
os.chdir('static')
```
{:codeblock}

Next,
create a simple HTML file.
The file is going to contain the log of each activity as the application creates the database:

```python
# Begin creating a very simple web page.
filename = "index.html"
target = open(filename, 'w')
target.truncate()
target.write("<html><head><title>Cloudant Python Demo</title></head><body><p>Log of Cloudant Python steps...</p><pre>")
```
{:codeblock}

The first part of the log is a record of the current date and time.
This record helps confirm that the database really is being freshly created:

```python
# Put a clear indication of the current date and time at the top of the page.
target.write("====\n")
target.write(strftime("%Y-%m-%d %H:%M:%S", gmtime()))
target.write("\n====\n\n")
```
{:codeblock}

#### Working with the Cloudant database instance

The Python application runs within a {{site.data.keyword.Bluemix_notm}} application environment.
The environment provides all the necessary information for the application to access connected services.
The information is provided within an environment variable,
called '`VCAP_SERVICES`'.
This variable can be accessed by the application,
and used to determine the connection details.

The first task is to ensure that the application is running within
a {{site.data.keyword.Bluemix_notm}} application environment.
Check by testing for the presence of the '`VCAP_SERVICES`' environment variable:

```python
# Check that we are running in a Bluemix application environment.
if 'VCAP_SERVICES' in os.environ:
```
{:codeblock}

>   **Note**: The next sections of code are run only if the environment variable was found.
    In Python,
    this code is indented to indicate that it is the body of the test.
    In this tutorial,
    indentation is omitted from the code segments to save space.
    However,
    the [full listing](#complete-listing) shows the indentation correctly.

Assuming that the variable is found,
proceed to use the information.
Start by loading the JSON data that is stored within the variable,
and recording the event in the new 'log file':

```python
# Yes we are, so get the service information.
vcap_servicesData = json.loads(os.environ['VCAP_SERVICES'])
# Log the fact that we successfully found some service information.
target.write("Got vcap_servicesData\n")
```
{:codeblock}

Next,
look for information about the connected {{site.data.keyword.cloudant_short_notm}} database instance.
Again,
record the event in the 'log file':

```python
# Look for the Cloudant service instance.
cloudantNoSQLDBData = vcap_servicesData['cloudantNoSQLDB']
# Log the fact that we successfully found some Cloudant service information.
target.write("Got cloudantNoSQLDBData\n")
```
{:codeblock}

Several {{site.data.keyword.Bluemix_notm}} services might be connected to the application environment.
The credentials for each service are listed as array elements.
In this tutorial,
only one [service connection was created](create_bmxapp_appenv.html#connecting).
Therefore,
the application accesses the first element (element 'zero').
Each service element contains the credentials for that service,
expressed as a list indexed by the essential field names that are needed to access the service.
More information about the field names is provided in the
[tutorial](create_database.html#a-cloudant-service-instance-on-bluemix) that describes a simple database creation task.

```python
# Get a list containing the Cloudant connection information.
credentials = cloudantNoSQLDBData[0]
# Get the essential values for our application to talk to the service.
credentialsData = credentials['credentials']
# Log the fact that we successfully found the Cloudant values.
target.write("Got credentialsData\n\n")
```
{:codeblock}

Next,
inspect the list and retrieve the essential values:

```python
# Get the username ...
serviceUsername = credentialsData['username']
target.write("Got username: ")
target.write(serviceUsername)
target.write("\n")
# ... the password ...
servicePassword = credentialsData['password']
target.write("Got password: ")
target.write(servicePassword)
target.write("\n")
# ... and the URL of the service within Bluemix.
serviceURL = credentialsData['url']
target.write("Got URL: ")
target.write(serviceURL)
target.write("\n")
```
{:codeblock}

The application now has all the details necessary to create a database within the
{{site.data.keyword.cloudant_short_notm}} database instance.
This task is described in more detail in the
[tutorial](create_database.html#a-cloudant-service-instance-on-bluemix) that describes simple database creation.

The application must do these tasks:

1.  Establishes a connection to the database instance.
2.  Creates a database with the name provided [earlier](#getting-started).
3.  Creates a JSON document that contains the current date and time.
4.  Stores the JSON document in the database.
5.  Confirms that the document was stored safely.
6.  Closes the connection to the database instance.

The code for these tasks is as follows:

```python
# We now have all the details we need to work with the Cloudant service instance.
# Connect to the service instance.
client = Cloudant(serviceUsername, servicePassword, url=serviceURL)
client.connect()
# Create a database within the instance.
myDatabaseDemo = client.create_database(databaseName)
if myDatabaseDemo.exists():
    target.write("'{0}' successfully created.\n".format(databaseName))
    # Create a very simple JSON document with the current date and time.
    jsonDocument = {
        "rightNow": strftime("%Y-%m-%d %H:%M:%S", gmtime())
    }
    # Store the JSON document in the database.
    newDocument = myDatabaseDemo.create_document(jsonDocument)
    if newDocument.exists():
        target.write("Document successfully created.\n")
# All done - disconnect from the service instance.
client.disconnect()
```
{:codeblock}

#### Closing the log file

The next step is to finish the log file,
ready to serve it using a simple Python web server within the application:

```python
# Put another clear indication of the current date and time at the bottom of the page.
target.write("\n====\n")
target.write(strftime("%Y-%m-%d %H:%M:%S", gmtime()))
target.write("\n====\n")
# Finish creating the web page.
target.write("</pre></body></html>")
target.close()
```
{:codeblock}

#### Serving the log file

The final task is to start the web server within the Python application.
The sole purpose of the server is to return the log file on request.
This log file confirms that the Python application successfully completed the following tasks:

1.  Ran successfully within the {{site.data.keyword.Bluemix_notm}} application environment.
2.  Determined the details for service connections.
3.  Connected to a {{site.data.keyword.cloudant_short_notm}} database instance.
4.  Created a database.
5.  Created a document within the database.
6.  Replied with the log of events when requested.

The code for starting the Python web server is included as part of the
['starter' application pack](create_bmxapp_appenv.html#starter):

```python
# Start up the simple Python web server application,
# so that it can 'serve' our newly created web page.
PORT = int(os.getenv('PORT', 8000))
httpd = Server(("", PORT), Handler)
try:
  print("Start serving at port %i" % PORT)
  httpd.serve_forever()
except KeyboardInterrupt:
  pass
httpd.server_close()
```
{:codeblock}

## The next step

The next step in the tutorial is to [upload the application](create_bmxapp_upload.html) for testing purposes.

## Complete listing

The following code is the complete Python program to access a
{{site.data.keyword.cloudant_short_notm}} service instance on {{site.data.keyword.Bluemix_notm}}:

```python
# Make Python modules available.
import os
import json

# It is helpful to have access to tools
# for formatting date and time values.
from time import gmtime, strftime

# Simplify access to basic Python web server tools.
try:
    from SimpleHTTPServer import SimpleHTTPRequestHandler as Handler
    from SocketServer import TCPServer as Server
except ImportError:
    from http.server import SimpleHTTPRequestHandler as Handler
    from http.server import HTTPServer as Server

# Enable the required Python libraries for working with Cloudant.
from cloudant.client import Cloudant
from cloudant.error import CloudantException
from cloudant.result import Result, ResultByKey

# This is the name of the database we intend to create.
databaseName = "databasedemo"

# Change current directory to avoid exposure of control files
try:
    os.mkdir('static')
except OSError:
    # The directory already exists,
    # no need to create it.
    pass
os.chdir('static')

# Begin creating a very simple web page.
filename = "index.html"
target = open(filename, 'w')
target.truncate()
target.write("<html><head><title>Cloudant Python Demo</title></head><body><p>Log of Cloudant Python steps...</p><pre>")

# Put a clear indication of the current date and time at the top of the page.
target.write("====\n")
target.write(strftime("%Y-%m-%d %H:%M:%S", gmtime()))
target.write("\n====\n\n")

# Start working with the Cloudant service instance.

# Check that we are running in a Bluemix application environment.
if 'VCAP_SERVICES' in os.environ:
    # Yes we are, so get the service information.
    vcap_servicesData = json.loads(os.environ['VCAP_SERVICES'])
    # Log the fact that we successfully found some service information.
    target.write("Got vcap_servicesData\n")
    # Look for the Cloudant service instance.
    cloudantNoSQLDBData = vcap_servicesData['cloudantNoSQLDB']
    # Log the fact that we successfully found some Cloudant service information.
    target.write("Got cloudantNoSQLDBData\n")
    # Get a list containing the Cloudant connection information.
    credentials = cloudantNoSQLDBData[0]
    # Get the essential values for our application to talk to the service.
    credentialsData = credentials['credentials']
    # Log the fact that we successfully found the Cloudant values.
    target.write("Got credentialsData\n\n")
    # Get the username ...
    serviceUsername = credentialsData['username']
    target.write("Got username: ")
    target.write(serviceUsername)
    target.write("\n")
    # ... the password ...
    servicePassword = credentialsData['password']
    target.write("Got password: ")
    target.write(servicePassword)
    target.write("\n")
    # ... and the URL of the service within Bluemix.
    serviceURL = credentialsData['url']
    target.write("Got URL: ")
    target.write(serviceURL)
    target.write("\n")

    # We now have all the details we need to work with the Cloudant service instance.
    # Connect to the service instance.
    client = Cloudant(serviceUsername, servicePassword, url=serviceURL)
    client.connect()
    # Create a database within the instance.
    myDatabaseDemo = client.create_database(databaseName)
    if myDatabaseDemo.exists():
        target.write("'{0}' successfully created.\n".format(databaseName))
        # Create a very simple JSON document with the current date and time.
        jsonDocument = {
            "rightNow": strftime("%Y-%m-%d %H:%M:%S", gmtime())
        }
        # Store the JSON document in the database.
        newDocument = myDatabaseDemo.create_document(jsonDocument)
        if newDocument.exists():
            target.write("Document successfully created.\n")
    # All done - disconnect from the service instance.
    client.disconnect()

# Put another clear indication of the current date and time at the bottom of the page.
target.write("\n====\n")
target.write(strftime("%Y-%m-%d %H:%M:%S", gmtime()))
target.write("\n====\n")
# Finish creating the web page.
target.write("</pre></body></html>")
target.close()

# Start up the simple Python web server application,
# so that it can 'serve' our newly created web page.
PORT = int(os.getenv('PORT', 8000))
httpd = Server(("", PORT), Handler)
try:
  print("Start serving at port %i" % PORT)
  httpd.serve_forever()
except KeyboardInterrupt:
  pass
httpd.server_close()
```
{:codeblock}
