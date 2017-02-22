---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Unbinding and deprovisioning your  {{site.data.keyword.objectstorageshort}} instance {: #deprovisioning-object-storage}

If the {{site.data.keyword.objectstorageshort}} service is bound to your Cloud Foundry App, but you no longer need storage, you can unbind and deprovision your instance.
{: shortdesc}


## Unbinding your instance

You can maintain your saved data and unbind the service from your Cloud Foundry app. The {{site.data.keyword.objectstorageshort}} account is not deleted until the service is deprovisioned.

**Attention**: If you unbind an {{site.data.keyword.objectstorageshort}} instance from a {{site.data.keyword.Bluemix_notm}} application, or delete the service key, all of your credentials for that instance are deleted, and cannot be restored. You can generate new cloud credentials by rebinding your instance, or by creating a new service key.

1. To see the services that are bound to your app, click the connections tab in your Cloud Foundry application.
2. Locate the service you that you want to unbind and click the menu button on the service tile.
3. Select **Unbind service**.
4. Clear the **Delete service instance** box and click **OK**.
5. Click **Restage** for your change to take effect.



## Deprovisioning your instance

If you have an instance of {{site.data.keyword.objectstorageshort}} that you no longer need, you can delete the instance.

**Attention**: When you deprovision an {{site.data.keyword.objectstorageshort}}  instance, the cloud project and Swift account are deleted. All containers and objects in the deprovisioned instance are deleted, and cannot be restored.

1. To see the services that are bound to your app, click the connections tab in your Cloud Foundry application.
2. Locate the service you that you want to deprovision and click the menu button on the service tile.
3. Select **Delete service**.
4. Click **Delete** to confirm.
5. Click **Restage** for your change to take effect.
