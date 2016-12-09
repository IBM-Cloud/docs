---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-09"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Constructing your {{site.data.keyword.objectstorageshort}} URL to use the Swift REST API

You can use the Swift REST API with a command-line client interface, such as cURL, or call the API from your application.
{: shortdesc}


For a comprehensive list of the {{site.data.keyword.objectstorageshort}} REST API options and examples, see the [OpenStack Swift API complete reference](http://developer.openstack.org/api-ref-objectstorage-v1.html).

When you authenticated your service instance with Keystone, you took note of the catalog response. It should look similar to the following example.

```
{
  "id" : "4207049680fa4effbecd044c7448a8cb",
  "region" : "dallas",
  "region_id" : "dallas",
  "url" : "https://dal.objectstorage.open.softlayer.com/v1/AUTH_4abf7d7bac2c4eda89c03dd3afa7a0a3",
  "interface" : "public"
},
```
{: codeblock}


Add the namespace of your container and object to the end of your {{site.data.keyword.objectstorageshort}} URL as shown in the following image.

![{{site.data.keyword.objectstorageshort}} URL pieces shown in an example image](images/Swift_URL.png)
  
Figure 1: {{site.data.keyword.objectstorageshort}} URL example
