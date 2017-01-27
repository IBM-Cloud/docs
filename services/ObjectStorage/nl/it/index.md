---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-05"

---
{:new_window: target="blank"}
{:shortdesc: .shortdesc}



# Getting started with {{site.data.keyword.objectstorageshort}} {: #getting-started-with-object-storage}


{{site.data.keyword.objectstoragefull}} provides unstructured cloud data storage. You can store and access your content as well as interactively compose and connect to apps and services.
{: shortdesc}

Some common use cases for the {{site.data.keyword.objectstorageshort}} service are:

* Backing up volume data from your instances
* Using as an intermediary location when you transfer large amounts of data
* Transferring data between environments that are not directly connected
* Acting as a central repository


{{site.data.keyword.Bluemix_notm}} Public {{site.data.keyword.objectstorageshort}} provides you with access to a fully provisioned Swift {{site.data.keyword.objectstorageshort}} account to manage your data. Provider side encryption is not provided.


1.	Provision your service instance from the {{site.data.keyword.Bluemix_notm}} catalog. Configure your instance and click **Create**. If you initially choose the **Leave Unbound** option for the **App** field, you can still bind the service instance to your {{site.data.keyword.Bluemix_notm}} app later.
2. In your service instance dashboard, create a container to start storing objects.
3. Add a file to your container from the **Actions** drop-down menu.
4. To test access to your objects, click **Download** and review the file.
5. When you're ready to connect your instance to an application, set up your service credentials and [bind the service](/docs/services/reqnsi.html#add_service).



# Related Links
{: #rellinks}

## API Reference
{: #api}
* [OpenStack {{site.data.keyword.objectstorageshort}} (Swift) API v1](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}
* [OpenStack Identity (Keystone) API v3.0](http://developer.openstack.org/api-ref-identity-v3.html){: new_window}

## SDK
{: #sdk}
* [OpenStack Software Development Kits (SDK)](https://wiki.openstack.org/wiki/SDKs){: new_window}

## Tutorials and Samples
{: #samples}
* [Connecting to IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} with Java](https://developer.ibm.com/recipes/tutorials/connecting-to-ibm-object-storage-for-bluemix-with-java/){: new_window}
* [Use Python to access your {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}}](https://developer.ibm.com/recipes/tutorials/use-python-to-access-your-bluemix-object-storage/){: new_window}
* [Use PHP to leverage {{site.data.keyword.objectstorageshort}}](https://developer.ibm.com/recipes/tutorials/use-php-to-leverage-object-storage-for-bluemix/){: new_window}

## Compatible Runtimes
{: #buildpacks}
* [Liberty for Java](https://www.ng.bluemix.net/docs/runtimes/liberty/index.html){: new_window}
* [SDK for Node.js](https://www.ng.bluemix.net/docs/runtimes/nodejs/index.html){: new_window}
* [Go](https://www.ng.bluemix.net/docs/runtimes/go/index.html){: new_window}
* [PHP](https://www.ng.bluemix.net/docs/runtimes/php/index.html){: new_window}
* [Python](https://www.ng.bluemix.net/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://www.ng.bluemix.net/docs/runtimes/ruby/index.html){: new_window}
* [Community buildpacks](https://www.ng.bluemix.net/docs/starters/byob.html){: new_window}


## Related Links
{: #general}
* [IBM {{site.data.keyword.Bluemix_notm}} Pricing Sheet](https://www.ng.bluemix.net/#/pricing){: new_window}
* [IBM {{site.data.keyword.Bluemix_notm}} Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
