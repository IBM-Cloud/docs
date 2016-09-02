{:new_window: target="_blank"} 

# Getting started with {{site.data.keyword.blockstorageshort}} (Beta)

Last updated: 29 July 2016
{: .last-updated}

{{site.data.keyword.blockstoragefull}} provides access to block level storage for transaction-intensive workloads and runtimes that need persistent storage. You can use the {{site.data.keyword.blockstorageshort}} service to manage volume lifecycles, attach volumes to your IBM Virtual Servers, and create snapshots of your block storage volumes.

Before you begin, review the following information.

* Ensure that you created an instance of the {{site.data.keyword.blockstorageshort}} service in your space. For more information on how to add a new service instance, see [Requesting a new service instance](../../services/reqnsi.html#req_instance).
* The {{site.data.keyword.blockstorageshort}} service is supported only in an unbound context. 
* You must have IBM {{site.data.keyword.virtualmachinesshort}} created to attach block storage volumes. To learn more about using block storage volumes with IBM {{site.data.keyword.virtualmachinesshort}}, see [Block storage volumes and IBM Virtual Servers](../../virtualmachines/vm_create.html#storage_BS). 

Complete these steps to get started with {{site.data.keyword.blockstorageshort}}:

1. Create a volume.
   
   a. In the Bluemix UI, select **Console > Storage > Block Storage**.

   b. On the Manage page, click **Create volume** to start the Create Volume dialog.

   c.	Provide a name. 
   
      **Note:** The name is for display purposes only.
   
   d. Provide the size of the volume that you want. 
   
      **Note:** Decimal numbers are not accepted. The size is limited by the quota that is assigned to your organization.
   
   e.	Optionally, provide a more detailed description of the volume.
   
   f.	Click **Create** to submit the information and close the dialog.

  Creating a volume can take a few moments.

2. Attach a volume to a virtual server.

   a. In the Bluemix UI, select Console > Storage > Block Storage.

   b. Select a volume from the list of available volumes.
   
   c.	Click **Attach**.
   
   d.	In the Attach dialog, select an instance of a virtual server from the drop-down list. 
   
   e.	Optionally, specify the device to be used to attach this volume. 
   
      **Note:** If you do not specify the device, the system automatically selects the first available device on the virtual server.
   
   f.	Click **Attach** to submit the information and close the dialog.
   
   The volume is listed in the table of attached volumes with the information about the virtual server instance. The virtual server can now use the device to persist data. 
 
What's next?

Prepare the volume for use. For more information, see [Preparing volumes](../BlockStorage/blockstorage_preparingvolume.html).

# Related Links
{: #rellinks}

## Tutorials and Samples
{:id="samples"}

* [How to Use IBM Block Storage for Bluemix with IBM Virtual Servers](https://developer.ibm.com/bluemix/2016/02/24/use-block-storage-for-bluemix-with-virtual-servers/){: new_window}
* [Getting Started with IBM Block Storage for Bluemix](https://developer.ibm.com/bluemix/2016/02/15/getting-started-with-block-storage/){: new_window}
* [IBM Block Storage for Bluemix Demo](https://www.youtube.com/watch?v=3gCIHYKU1rE&list=PLzpeuWUENMK2d3L5qCITo2GQEt-7r0oqm&index=45){: new_window}

## API Reference
{: #api}
* [OpenStack Block Storage (Cinder) API v2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}

