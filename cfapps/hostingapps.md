---

 

copyright:

  years: 2015，2016

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Hosting apps in {{site.data.keyword.Bluemix_notm}}

*Last updated: 9 May 2016*

<!--The whole topic is staging only -->

With {{site.data.keyword.Bluemix}}, you can create applications, as well as host your existing applications. You can migrate your apps to {{site.data.keyword.Bluemix_notm}} as long as it is cloud-ready. {{site.data.keyword.Bluemix_notm}} provides various ways for you to run your applications, for example, Cloud Foundry, IBM Containers, and Virtual Machines.

##Making your apps Cloud-ready
{: #cloud-readyapps}

A cloud-ready application follows the cloud platform principles when the application is designed and built. A cloud-ready application can use the capabilities that are provided by the cloud platform.

If all of the following principles are observed in your application, the application is cloud-ready and can be migrated to {{site.data.keyword.Bluemix_notm}}. If a principle is violated in your application, you can usually modify your application to adhere to the principles.

* Do not code your application directly to a specific topology.

  In a non-cloud environment, the application might use a particular deployment topology. However, the application topology might change in cloud applications, because the cloud-ready applications and services allow immediate scalability changes. The scalability changes include dynamic scaling and manually resizing the number of instances of an application.

  Build your application to be as generic and stateless as possible to keep your application from being affected by scalability changes.

* Do not assume that the local file system is permanent.

  Because an application instance can be moved, deleted, or duplicated at any time on cloud, do not rely on the files that are written to the file system. If an application uses the local file system as a cache of frequently used information including application logs, the information is lost when the instance is shut down and restarted at a different location or a different VM.

  You can store information in a service, such as an SQL or NoSQL database instead of the local file system. In a dynamic cloud environment, it's also critical to have your logs available on a service that outlives the application instances where the logs are generated.

* Do not store session state in your application.

  The state of your system is defined by your databases and shared storage, and not by each individual running application instance. Statefulness of any sort limits the scalability of an application. Try to minimize the impact of session state by storing it in a centralized location on the server.

  If you can't eliminate session state entirely, push it out to a highly available store that is external to your application server. The stores include IBM WebSphere Extreme Scale, Redis, or Memcached, or an external database.

* Do not use specific infrastructure dependency.

  This is a general principle that has several manifestations. For example, do not assume that the services your application uses are allocated particular host names or IP addresses. Because the services might be relocated or regenerated in your cloud environment, the host names and IP addresses can also change.

  Extracting environment-specific dependencies into a set of property files is an improvement, but it is still inadequate. The best practice is to use an external service registry to resolve service endpoints, or delegate the entire routing function to a service bus or a load balancer with a virtual name.

* Do not use infrastructure APIs in your application.

  If you rely on a specific infrastructure API in your application, changing the infrastructure is more challenging, because an infrastructure API can refer to many different layers in your software stack.

  You can rely on existing open source or commercial products instead, and leave PaaS solutions in the PaaS layer to keep them out of your application code.

* Do not use obscure protocols.

  Do not use obscure protocols that require extra configuration for resiliency.

  Applications based on standard protocols are more resilient with the configuration items delegated to the platform. The standard protocols include HTTP, SSL, standard database, queuing, and web service connections.

* Do not rely on OS-specific features

  If you have already used OS-specific features, you can fix this issue by using compatibility libraries, for example, Cygwin and Mono. Cygwin is a compatibility library that provides a set of Linux tools in a Windows environment. Mono is a compatibility library that provides Windows .NET capabilities in Linux.

  Avoid the OS-specific dependencies; instead, use services that are provided by the middleware infrastructure or service providers.

* Do not manually install your application.

  Your application might be installed frequently on-demand on the dynamic cloud environment. The installation process must be scripted and reliable, and the configuration data must be externalized from the scripts.

  At a minimum, capture your application installation as a uniform set of scripts that are independent of the operating system. Keep your application installation small and portable to adapt to different automation techniques. Also, minimize the dependencies that are required by the application installation.

For more information about cloud-ready applications, see [The 12-factor application](http://12factor.net/){:new_window}.

##Migrating your apps
{: #ht_hostapp}

You can migrate your applications to {{site.data.keyword.Bluemix_notm}} in an incremental way, instead of shifting the application completely to the cloud environment. You can migrate a portion of your application first and connect to the existing data or system of records by using the Cloud Integration service.

In your cloud applications, you might need to access the backend data or services, for example, a system of record. In {{site.data.keyword.Bluemix_notm}}, you can use the Secure Gateway service to establish a secured tunnel between a {{site.data.keyword.Bluemix_notm}} organization and the enterprise backend network. The service enables the applications on {{site.data.keyword.Bluemix_notm}} to access the backend network’s data and services. For details, see [Reaching enterprise backend with Bluemix Secure Gateway via console](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){:new_window}.

To deploy your application to {{site.data.keyword.Bluemix_notm}} as a Cloud Foundry application, select a runtime from the {{site.data.keyword.Bluemix_notm}} Catalog. The runtime contains a starter Hello World application that you can replace with your own application. If you cannot find a starter that provides the runtime you want, you can bring a custom, Cloud Foundry-compatible buildpack to {{site.data.keyword.Bluemix_notm}} by using the –b option with the cf push command. For details, see [Using community buildpacks](../cfapps/byob.html).

You can use the following tools and services that {{site.data.keyword.Bluemix_notm}} provides:

*Table 1. {{site.data.keyword.Bluemix_notm}} tools*

| Tool	| Method |
|:------|:--------|
|Cloud Foundry command line interface (cf cli)	|Manage your code on local client and use Cloud Foundry command line interface to push your application to {{site.data.keyword.Bluemix_notm}} manually. For more information, see [Uploading your apps](../starters/upload_app.html).|
|Eclipse	|Manage your code in Eclipse and use the IBM Eclipse tools for {{site.data.keyword.Bluemix_notm}} to push your application.|
|Git integration	|Manage your code on GitHub and integrate Git into {{site.data.keyword.Bluemix_notm}}. You can collaborate with other developers. Your application is deployed to {{site.data.keyword.Bluemix_notm}} automatically when you commit changes in the code. You do not need to push the application manually.|
|{{site.data.keyword.Bluemix_notm}} DevOps Delivery Pipeline	|Manage your code on DevOps GitHub repository and deploy your application to {{site.data.keyword.Bluemix_notm}} by using the DevOps Delivery Pipeline.|


If the Cloud Foundry platform does not support your application requirements, you can use a container or VM where the runtime is set up, configured, and maintained with more customized options.

##Uploading your apps by using cf cli
{: #ht_cfcli}

You can manage your code on local client and use Cloud Foundry command line interface to upload your application to {{site.data.keyword.Bluemix_notm}} manually. If you change the code, you must push your application to {{site.data.keyword.Bluemix_notm}} again to run the updated code.

Take the following steps to migrate your application:

<ol>
<li>Install the Cloud Foundry command line interface. Ensure that you use the latest version of the cf command line interface.
<ol>
<li>Download the installation program for your operating system.</li>
<li>Follow the tool wizard to install the command line.</li>
<li>Use the following command to verify the version of the cf command line interface:
<pre>cf -v</pre></li>
</ol>
</li>

<li>Optional: If you want to specify and save the deployment details before you push an application to {{site.data.keyword.Bluemix_notm}}, you can add the application manifest by taking the following steps:
<ol>
<li>Go to the working directory of your application and create a file entitled manifest.yml, which is the default name.</li>
<li>Specify deployment details in the manifest file. The following example shows a manifest file for a Java™ application.
<pre class="pre codeblock"><code>applications:
- disk_quota: 1024M
  host: myjavatest
  name: MyJavaTest
  path: webStarterApp.war
  domain: mybluemix.net
  instances: 1
  memory: 512M</code></pre>
<p>For more information about the supported options that you can use in this file, see [Application manifest](../manageapps/depapps.html#appmanifest).

</p></li></ol>
</li>

<li>Push your application. You can upload your application by using the cf push command.
<ol>
<li>Connect and log in to {{site.data.keyword.Bluemix_notm}} by running the following command. Select your organization and space when prompted.
<pre>cf login -a https://api.ng.bluemix.net</pre></li>
<li>From your application directory, enter the cf push command with the application name. The application name must be unique in the {{site.data.keyword.Bluemix_notm}} environment.
<pre>cf push appname</pre></li>
<li>Optional: If you use an external buildpack, you must use the -b option with the cf push command. For example:
<pre>cf push appname -b buildpack_URL</pre>
<p>See Using community buildpacks for details.</p>
</li></ol>
</li>

<li>Optional: If you change your application, you must upload those changes by entering the cf push command again. The cf command line interface uses your previous options and your responses to the prompts to update any running instances of your application with the new bits of code.</li>
</ol>

**Notes:**

* When you use the cf push command, the cf command line interface copies all of the files and directories from your current directory to {{site.data.keyword.Bluemix_notm}}. Ensure that you have only the required files in your application directory.
* Ensure that your organization has enough memory for all instances of your application. To view the memory quota for your org, use cf org org_name.
* For more information about cf push, see [cf commands](../cli/reference/cfcommands/index.html).

##Migrating your data and using services
{: #ht_service}

After you upload your application to {{site.data.keyword.Bluemix_notm}}, select the service that your application is connected to from the {{site.data.keyword.Bluemix_notm}} Catalog, create a service instance, bind the instance to your application, and then restart your application.

The VCAP_SERVICES environment variable of your application is a JSON object that contains information about how to interact with a service instance in {{site.data.keyword.Bluemix_notm}}. The information includes the service instance name, credentials, and the connection URL to the service instance.

To run your code in {{site.data.keyword.Bluemix_notm}}, you must add the code logic for parsing the VCAP_SERVICES variable to obtain information about service connection. Modify your application to get the dynamically assigned host and port of the service instance through the environment variables. The following example shows how to get the credentials of a Postgre SQL service instance in a Ruby application:

```
services = JSON.parse(ENV['VCAP_SERVICES'], :symbolize_names => true)
        url = services.values.map do |srvs|
          srvs.map do |srv|
            if srv[:credentials][:uri] =~ /^postgres/
              srv[:credentials][:uri]
            else
              []
            end
          end
        end.flatten!.first
```		
{:codeblock}

To ensure that your application can run in a local environment after you modify the application for {{site.data.keyword.Bluemix_notm}}, check for the presence of the VCAP_SERVICES environment variable, which is set for all {{site.data.keyword.Bluemix_notm}} Cloud Foundry applications.


# Related Links
{: #rellinks}

## Related Links
{: #general}

* [IBM Containers](../containers/container_cli_ov.html)
* [Virtual Machines](../virtualmachines/vm_index.html)
* [Getting started with Delivery Pipeline](../services/DeliveryPipeline/index.html)
* [Deploying apps with IBM Eclipse Tools for Bluemix](../manageapps/eclipsetools/eclipsetools.html)
* [The twelve-factor app](http://12factor.net/){:new_window}
* [Reaching enterprise backend with Bluemix Secure Gateway via console](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){:new_window}
