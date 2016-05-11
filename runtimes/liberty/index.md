---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty for Java
{: #liberty_runtime}

*Last updated: 23 March 2016*

Liberty for Java applications on {{site.data.keyword.Bluemix}} are powered by the liberty-for-java buildpack. The liberty-for-java buildpack provides a complete runtime environment for running Java EE 7 and OSGi applications on top of Liberty profile. It supports popular frameworks like Spring and includes the IBM JRE. WebSphere Liberty enables rapid application development that is well suited to the cloud.
{: shortdesc}

## Detection
{: #detection}
The Liberty buildpack is used when the following kinds of applications are deployed:
* [WAR files](optionsForPushing.html#stand_alone_apps)
* [EAR files](optionsForPushing.html#stand_alone_apps)
* [Liberty server directory](optionsForPushing.html#server_directory)
* [Liberty packaged server](optionsForPushing.html#packaged_server)
* Java main
* [Distzip](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/container-distZip.md)

## Starter application
{: #starter_application}
{{site.data.keyword.Bluemix}} provides several Liberty starter applications.  The Liberty starter applications are simple Liberty apps that provide a template that you can use. You can experiment with the starter apps, and make and push changes to the Bluemix environment.  See [Using the starter applications](../../cfapps/starter_app_usage.html) for help with using the starter applications.

# rellinks
## general
* [Liberty Profile Overview](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
* [Managing Liberty apps](../../manageapps/app_mng.html#Utilities)
* [Deploying apps with IBM Eclipse Tools for Bluemix](../../manageapps/eclipsetools/eclipsetools.html#eclipsetools)
* [Getting started with IBM Monitoring and Analytics for Bluemix Service](../../services/monana/index.html#monana_oview)
## samples
* [Cloud Foundry Architecture Labs](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/)
