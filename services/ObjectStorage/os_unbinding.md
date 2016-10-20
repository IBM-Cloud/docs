---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Unbinding and deprovisioning your  {{site.data.keyword.objectstorageshort}} instance {: #deprovisioning-object-storage}

*Last updated: 19 October 2016*
{: .last-updated}


### Unbinding your instance
If you no longer have a need for {{site.data.keyword.objectstorageshort}} in your Cloud Foundry app, but you want to maintain your saved data, you can unbind your instance of the service from your app.

**Attention**: If you unbind an {{site.data.keyword.objectstorageshort}} instance from a {{site.data.keyword.Bluemix_notm}} application, or delete the service key, all of your credentials for that instance are deleted and cannot be restored.

1. Open your app details in the {{site.data.keyword.Bluemix_notm}} console.
2. Select your {{site.data.keyword.objectstorageshort}} instance and click **Unbind Service**.
3. Click **REMOVE**.
4. Click **RESTAGE**.



### Deprovisioning your instance

If you have an unbound instance of {{site.data.keyword.objectstorageshort}} that you no longer need, you can delete the instance.

**Attention**: When you deprovision an {{site.data.keyword.objectstorageshort}}  instance, the cloud project is deleted. All containers and objects in the deprovisioned instance are deleted, and cannot be restored.

1. Open your app details in the {{site.data.keyword.Bluemix_notm}} console.
2. Select your {{site.data.keyword.objectstorageshort}} instance and click **Delete**.
3. Click **RESTAGE**.
