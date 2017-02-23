---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-23"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# About {{site.data.keyword.objectstorageshort}}

{{site.data.keyword.objectstoragefull}} provides you a fully provisioned account, based on the Swift API, to manage your data.
{: shortdesc}


## How the service works

With {{site.data.keyword.objectstorageshort}}, your unstructured data is stored in a scalable, multi-tenant cloud environment. The service uses OpenStack Identity (Keystone) for authentication and can be accessed directly by using OpenStack Object Storage (Swift) API v1 calls. The service can be bound to a {{site.data.keyword.Bluemix_notm}} application or accessed from outside a {{site.data.keyword.Bluemix_notm}} application.

**Note**: Provider side encryption is not provided.

Both admins and developers can store and access objects as shown in the following diagram.


<dl>
  <dt> {{site.data.keyword.Bluemix_notm}} app </dt>
    <dd> You can bind the {{site.data.keyword.objectstorageshort}} service to a {{site.data.keyword.Bluemix_notm}} app. You must encrypt your data before uploading when using {{site.data.keyword.Bluemix_notm}} Public {{site.data.keyword.objectstorageshort}}. </dd>
  <dt> Client app </dt>
    <dd> You can access {{site.data.keyword.objectstorageshort}} directly from your application through a firewall on a private network. Provider side encryption is not provided. </dd>
  <dt> Keystone </dt>
    <dd> You authenticate your service with Keystone and receive an authorization token. </dd>
  <dt> OpenStack Swift API </dt>
    <dd> After you authenticate your instance, you can read and write to your stored objects by using the Swift API. </dd>
  <dt> Storage nodes </dt>
    <dd> The service maintains three copies of your data that it <a href="http://docs.openstack.org/developer/swift/overview_replication.html">replicates across multiple storage nodes</a>. </dd>
</dl>

![How {{site.data.keyword.objectstorageshort}} works as written above, shown in a diagram.](/images/OS_howitworks.png)
<caption> Figure 1. How {{site.data.keyword.Bluemix_notm}} Public {{site.data.keyword.objectstorageshort}} works </caption>
