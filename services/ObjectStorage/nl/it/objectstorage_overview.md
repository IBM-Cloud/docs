---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# About {{site.data.keyword.objectstorageshort}}  {: #about-object-storage}


{{site.data.keyword.objectstorageshort}} uses metadata to identify objects placed in storage so that they are easily searchable and quickly accessible even among large amounts of data.
{: shortdesc}


## How {{site.data.keyword.Bluemix_notm}} Public {{site.data.keyword.objectstorageshort}} works {: #public}

Public {{site.data.keyword.objectstorageshort}} has two separate routes a user can follow when provisioning an account. You can start within your own private network or you can access {{site.data.keyword.objectstorageshort}} through a {{site.data.keyword.Bluemix_notm}} app. Both admins and developers can store and access objects as shown in the following diagram.

<dl>
  <dt><dfn> {{site.data.keyword.Bluemix_notm}} app </dfn></dt>
    <dd> You can bind the {{site.data.keyword.objectstorageshort}} service to a {{site.data.keyword.Bluemix_notm}} app.  </dd>
  <dt><dfn> Client app </dfn></dt>
    <dd> You can access {{site.data.keyword.objectstorageshort}} directly from your application through a firewall on a private network. </dd>
  <dt><dfn> Keystone </dfn></dt>
    <dd> You use the credentials provided by the {{site.data.keyword.objectstorageshort}} service to obtain an authorization token from Keystone. </dd>
  <dt><dfn> OpenStack Swift API </dfn></dt>
    <dd> Once you have authenticated your instance, you can read and write to your stored objects using the Swift API. </dd>
  <dt><dfn> Storage nodes </dfn></dt>
    <dd> The service maintains three copies of your data that it <a href="http://docs.openstack.org/developer/swift/overview_replication.html">replicates across multiple storage nodes</a>. </dd>
</dl>

![How {{site.data.keyword.objectstorageshort}} works as written above, shown in a diagram.](images/OS_howitworks.png)

Figure 1. How {{site.data.keyword.Bluemix_notm}} Public {{site.data.keyword.objectstorageshort}} works

**Attention**: Provider side encryption is not provided. It is the responsibility of the client application to encrypt data before uploading. Disk level encryption is not currently available for {{site.data.keyword.Bluemix_notm}} Public {{site.data.keyword.objectstorageshort}}.
