---

copyright:
  years: 2014, 2016

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Unbinding and deprovisioning your  {{site.data.keyword.objectstorageshort}} instance {: #deprovisioning-object-storage}

*Last updated: 25 October 2016*
{: .last-updated}

### Unbinding your instance
If you no longer have a need for {{site.data.keyword.objectstorageshort}} in your Cloud Foundry app, but you want to maintain your saved data, you can unbind your instance of the service from your app.

**Attention**: If you unbind an {{site.data.keyword.objectstorageshort}} instance from a {{site.data.keyword.Bluemix_notm}} application, or delete the service key, all of your credentials for that instance are deleted and cannot be restored. The {{site.data.keyword.objectstorageshort}} account is not deleted until the {{site.data.keyword.objectstorageshort}} instance is deprovisioned. You can generate new cloud credentials by rebinding or creating a new service key.

1. To see the services bound to your app, click on the connections tab in your Cloud Foundry application.
2. Locate the service you want to unbind and click the menu button on the service tile.
3. Select **Unbind service**.
4. Uncheck **Delete service instance** and click **OK**.
5. Click **Restage** for your change to take effect.



### Deprovisioning your instance

If you have an unbound instance of {{site.data.keyword.objectstorageshort}} that you no longer need, you can delete the instance.

**Attention**: When you deprovision an {{site.data.keyword.objectstorageshort}}  instance, the cloud project and Swift account are deleted. All containers and objects in the deprovisioned instance are deleted, and cannot be restored.

1. To see the services bound to your app, click on the connections tab in your Cloud Foundry application.
2. Locate the service you want to unbind and click the menu button on the service tile.
3. Select **Delete service**.
4. Click **Delete** to confirm.
5. Click **Restage** for your change to take effect.

