---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with Cloudant
{: #getting-started-with-cloudant}

{{site.data.keyword.cloudantfull}} is a document-oriented DataBase as a Service (DBaaS).
It stores data as documents in JSON format.
It's built with scalability,
high availability,
and durability in mind.
It comes with a wide variety of indexing options including map-reduce,
Cloudant Query,
full-text indexing,
and geospatial indexing.
The replication capabilities make it easy to keep data in sync between database clusters,
desktop PCs,
and mobile devices.
{:shortdesc}

For more information on all the {{site.data.keyword.cloudant_short_notm}} offerings,
see the main [{{site.data.keyword.cloudant_short_notm}} ![External link icon](images/launch-glyph.svg "External link icon")](http://www.ibm.com/analytics/us/en/technology/cloud-data-services/cloudant/){:new_window} site.
For more details on {{site.data.keyword.cloudant_short_notm}} concepts,
tasks and techniques,
see the [{{site.data.keyword.cloudant_short_notm}} documentation](cloudant.html).

You can launch the {{site.data.keyword.cloudant_short_notm}} console from the service launch page on the
[{{site.data.keyword.Bluemix_notm}} dashboard](https://console.ng.bluemix.net/catalog/services/cloudant-nosql-db/).

To use the service,
follow these steps:

1.  Create a service instance using the
    [{{site.data.keyword.Bluemix_notm}} dashboard](https://console.ng.bluemix.net/catalog/services/cloudant-nosql-db/).
2.  Review the service instance access credentials,
    similar to the following example:
    ```json
    {
        "cloudantNoSQLDB": {
            "name": "Cloudant-3s",
            "label": "cloudantNoSQLDB",
            "plan": "shared",
            "credentials": {
                "username": "someusername",
                "password": "secret",
                "host": "myhost-bluemix.cloudant.com",
                "port": 443,
                "url": "https://someusername:secret@myhost-bluemix.cloudant.com"
            }
        }
    }
    ```
    {:codeblock}
3.  Create applications that connect to the service instance,
    and which use the service credentials.
    These applications can be created by using various environments,
    including:
    -   [Mobile platforms](libraries/supported.html#mobile)
    -   [Java](libraries/supported.html#java)
    -   [Node.js](libraries/supported.html#node-js)
    -   [Python](libraries/supported.html#python)
    -   [Swift](libraries/supported.html#swift)

    For more information,
    see the [Cloudant homepage ![External link icon](images/launch-glyph.svg "External link icon")](http://www.ibm.com/analytics/us/en/technology/cloud-data-services/cloudant/){:new_window}
    and the list of [Client Libraries](libraries/index.html).

Tutorials are [available](tutorials/index.html) that describe these tasks in more detail.
More information about tasks such as authenticating with database instances,
and querying data,
is available in the [API reference](api/index.html).

<!--

<ol>
<li>Create a service instance by using either the Bluemix dashboard,
or the CloudFoundry command line interface.
<p>To create an instance by using the dashboard,
follow these steps:
<ol>
<li>Log on to Bluemix.</li>
<li>On the dashboard,
click the '<code>Work With Data</code>' link on the Data &amp; Analytics panel.</li>
<li>Click the '<code>New Service</code>' button.</li>
<li>In the list of services,
click the {{site.data.keyword.cloudant}} button.</li>
<li>On the {{site.data.keyword.cloudant}} information page,
click the '<code>Choose {{site.data.keyword.cloudant}}</code>' button.</li>
<li>On the {{site.data.keyword.cloudant}} catalog page,
complete the details for the service you require.
Click the '<code>Create</code>' button when you are ready to proceed.</li>
<li>When the Cloudant instance has been created,
you are presented with the dashboard for that instance.
Click the '<code>Service Credentials</code>' link to see all the details you require to access your instance.</li>
</ol>
</p>
<p>To create an instance by using the CloudFoundry command line interface,
follow these steps:
<ol>
<li>Install the CloudFoundry <code>cf</code> tool on your system.
Instructions on how to do that can be found in the <a href="https://console.ng.bluemix.net/docs/cli/index.html">Bluemix CLI and dev tools guide</a>.</li>
<li>Create a new service instance using the command:<br/>
<pre><code>cf create-service</code></pre></li>
<li>You are presented with a list of available services.
Choose one of the services.
Enter a unique instance name and plan for the service.
A random name is suggested for the instance,
but you can change it to something else if you prefer.</li>
<li>After creating the service,
you can get a list of all the services created:<br/>
<pre><code>cf services</code></pre></li>
<li>You must bind a service to your application before you can use the service.
Do this using the command:<br/>
<pre><code>cf bind-service</code></pre>
From the resulting list,
select one of the applications,
and one of the services.
The <code>cf</code> command notifies you when the binding action succeeds.</li>
</ol>
</p>
</li>
<li><p>After creating a service instance, JSON data similar to the following example is displayed.
The data can also be viewed in the Bluemix dashboard.<br/>
<pre><code>{
  "cloudantNoSQLDB": {
    "name": "Cloudant-3s",
    "label": "cloudantNoSQLDB",
    "plan": "shared",
    "credentials": {
      "username": "someusername",
      "password": "secret",
      "host": "myhost-bluemix.cloudant.com",
      "port": 443,
      "url": "https://someusername:secret@myhost-bluemix.cloudant.com"
    }
  }
}</code></pre></p>
{: screen}
<p>The data is also added to the <code>VCAP_SERVICES</code> environment variable of any Bluemix application the service is bound to.</p>
<p>Service credentials are stored in a JSON object that contains the following fields:
<ul>
<li><code>key</code>: The name of the service (cloudantNoSQLDB)</li>
<li><code>name</code>: The user provided name of the service instance</li>
<li><code>host</code>: The host name of the server</li>
<li><code>port</code>: The port number the service is running on, usually 443</li>
<li><code>username</code>: The user name for authentication</li>
<li><code>password</code>: The password for authentication</li>
<li><code>url</code>: The URL of the service instance</li>
</ul></li>
<li><p>In your Bluemix applications, read the credentials from the <code>VCAP_SERVICES</code> environment variable.</p>
<p>In applications that run outside of Bluemix or in a different geographical region within Bluemix,
you can retrieve the credentials
from the Bluemix dashboard and add them to your application's configuration.</p>
</li>
<li>To access the database, the basic mechanism is to send requests to the host and port via HTTPS.
Each request must include the user name and password to enable authentication.
Your requests can be sent by using various application languages and platforms,
including:
<ul>
<li><a href="https://github.com/cloudant/sync-android">Android</a></li>
<li><a href="https://github.com/cloudant/CDTDatastore">Apple iOS</a></li>
<li><a href="https://github.com/cloudant/java-cloudant">Java</a></li>
<li><a href="https://github.com/cloudant/objective-cloudant">Objective C and Swift</a></li>
<li><a href="https://github.com/cloudant/python-cloudant">Python</a></li>
</ul>
... and many others.
For more information,
see the <a href="http://www.ibm.com/analytics/us/en/technology/cloud-data-services/cloudant/">Cloudant homepage</a>
and the list of <a href="libraries/index.html">Client Libraries</a>.
</li>
<li>When your application is ready,
you can deploy it to the Bluemix environment for verification.
To deploy an application,
use the command:<br/>
<pre><code>cf push</code></pre></li>
<li>To unbind a service instance from an application,
use the command:<br/>
<pre><code>cf unbind-service</code></pre></li>
<li>To delete a service instance,
use the command:<br/>
<pre><code>cf delete-service</code></pre></li>
</ol>

More information about authenticating to the database and making requests is available
in the [API reference](api/index.html).

-->

# Related Links
{: #rellinks notoc}

## Tutorials and Samples
{: #samples notoc}

*   [Tutorial overview](tutorials/index.html)
*   [Creating a {{site.data.keyword.cloudant_short_notm}} instance on {{site.data.keyword.Bluemix_notm}}](tutorials/create_service.html)
*   [Creating and populating a simple {{site.data.keyword.cloudant_short_notm}} database](tutorials/create_database.html)
*   [Creating a {{site.data.keyword.Bluemix_notm}} application to access a {{site.data.keyword.cloudant_short_notm}} database](tutorials/create_bmxapp.html)

## API Reference
{: #api notoc}

*   [{{site.data.keyword.cloudant_short_notm}} API reference](api/index.html)

## Related Links
{: #general notoc}

*   [{{site.data.keyword.cloudant_short_notm}} Guides ![External link icon](images/launch-glyph.svg "External link icon")](guides/index.html)
*   [{{site.data.keyword.cloudant_short_notm}} website and dashboard ![External link icon](images/launch-glyph.svg "External link icon")](https://cloudant.com/){:new_window}
*   [{{site.data.keyword.cloudant_short_notm}} Blog ![External link icon](images/launch-glyph.svg "External link icon")](https://cloudant.com/blog){:new_window}
*   [Using {{site.data.keyword.cloudant_short_notm}} with Liberty on {{site.data.keyword.Bluemix_notm}} ![External link icon](images/launch-glyph.svg "External link icon")](https://developer.ibm.com/bluemix/2014/07/08/cloudant_on_bluemix/){:new_window}
