---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with Cloudant
{: #getting-started-with-cloudant}
Last updated: 12 October 2016
{: .last-updated}

{{site.data.keyword.cloudant}} on Bluemix is a document database as a service (DBaaS) that stores data in JSON.
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

For more information on all the {{site.data.keyword.cloudant}} offerings,
see the main [Cloudant](http://www.ibm.com/analytics/us/en/technology/cloud-data-services/cloudant/) site.
For more details on {{site.data.keyword.cloudant}} concepts,
tasks and techniques,
see the [API Reference](https://docs.cloudant.com).

You can launch the {{site.data.keyword.cloudant}} on Bluemix console from the service launch page on the Bluemix dashboard.

To use the service, follow these steps:
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
and the list of <a href="http://docs.cloudant.com/libraries.html">Client Libraries</a>.
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

More information about authenticating to the database and making requests is available in the [API reference](https://docs.cloudant.com/api.html).

# Related Links
{: #rellinks}

* [Cloudant website and dashboard](https://cloudant.com/)
* [Cloudant Blog](https://cloudant.com/blog)

## Tutorials and Samples
{: #samples}

* [Cloudant client libraries](https://docs.cloudant.com/libraries.html)
* [Using Cloudant with Liberty on Bluemix](https://developer.ibm.com/bluemix/2014/07/08/cloudant_on_bluemix/)
* [Cloudant Guides](https://docs.cloudant.com/guides.html)

## API Reference
{: #api}

* [Cloudant API reference](https://docs.cloudant.com/api.html)
