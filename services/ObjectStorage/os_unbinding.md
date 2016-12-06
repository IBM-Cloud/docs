---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Unbinding and deprovisioning your  {{site.data.keyword.objectstorageshort}} instance {: #deprovisioning-object-storage}

If you have bound {{site.data.keyword.objectstorageshort}} to a Cloud Foundry application and no longer have a need for storage, you can unbind and deprovision your instance.
{: shortdesc}


## Unbinding your instance
If you no longer have a need for {{site.data.keyword.objectstorageshort}} in your Cloud Foundry app, but you want to maintain your saved data, you can unbind the instance of the service from your app.

**Attention**: If you unbind an {{site.data.keyword.objectstorageshort}} instance from a {{site.data.keyword.Bluemix_notm}} application, or delete the service key, all of your credentials for that instance are deleted and cannot be restored. The {{site.data.keyword.objectstorageshort}} account is not deleted until the {{site.data.keyword.objectstorageshort}} instance is deprovisioned. You can generate new cloud credentials by rebinding or creating a new service key.

1. To see the services that are bound to your app, click the connections tab in your Cloud Foundry application.
2. Locate the service you want to unbind and click the menu button on the service tile.
3. Select **Unbind service**.
4. Clear the **Delete service instance** box and click **OK**.
5. Click **Restage** for your change to take effect.



## Deprovisioning your instance

If you have an instance of {{site.data.keyword.objectstorageshort}} that you no longer need, you can delete the instance.

**Attention**: When you deprovision an {{site.data.keyword.objectstorageshort}}  instance, the cloud project and Swift account are deleted. All containers and objects in the deprovisioned instance are deleted, and cannot be restored.

1. To see the services that are bound to your app, click the connections tab in your Cloud Foundry application.
2. Locate the service you want to unbind and click the menu button on the service tile.
3. Select **Delete service**.
4. Click **Delete** to confirm.
5. Click **Restage** for your change to take effect.
