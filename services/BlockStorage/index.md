{:new_window: target="_blank"} 

# Getting started with {{site.data.keyword.blockstorageshort}} (Beta)

Last updated: 29 July 2016
{: .last-updated}

{{site.data.keyword.blockstoragefull}} provides access to block level storage for transaction intensive workloads and runtimes in need of persistent storage.

You can use IBM {{site.data.keyword.blockstorageshort}} to create volumes and attach them to virtual servers. To have persistent storage, a virtual server requires IBM {{site.data.keyword.blockstorageshort}}. Otherwise, when you restart the virtual server, it resets to the default image. The data in block storage volumes persists beyond the lifecycle of your virtual servers. IBM {{site.data.keyword.blockstorageshort}} uses OpenStack Cinder to manage the volume lifecycle.

{{site.data.keyword.blockstorageshort}} volumes are created through an IBM {{site.data.keyword.blockstorageshort}} service instance. You can attach the volumes to a virtual server in the following ways:
  * Specify a particular device that you provide. 
  * Specify that the system automatically selects an available device name. 

The virtual server performs its I/O operations directly with the specified device independent of the {{site.data.keyword.blockstorageshort}} service.

You can also create block-level snapshots of volumes. The {{site.data.keyword.blockstorageshort}} service does not allow you to create snapshots while the volume is attached, so the resulting snapshots will be crash-consistent. 

Complete these steps to get started with IBM {{site.data.keyword.blockstorageshort}}:

1. Create a {{site.data.keyword.blockstorageshort}} service instance.
   To create an instance of the {{site.data.keyword.blockstorageshort}} service in your space, follow these steps:
 
   a.	Go to the {{site.data.keyword.Bluemix_notm}} **Catalog** tab and enter **{{site.data.keyword.blockstorageshort}}** into the search box, or go to **Services** and select **Storage**. Click the **{{site.data.keyword.blockstorageshort}}** service. 
 
   b.	Enter a space and service name. Select the plan and click **Create**.
 	
   The {{site.data.keyword.blockstorageshort}} service is only supported in an unbound context. 

   An instance of {{site.data.keyword.blockstorageshort}} service is created in your space. You can open the {{site.data.keyword.blockstorageshort}} UI to manage volumes anytime by clicking the service instance icon.

2. Create a volume.
   
   a. Open the {{site.data.keyword.blockstorageshort}} service.

   b. Click **Create** to start the **Create Volume** dialog.

   c.	Provide the size of the volume that you want. Decimal numbers are not accepted. The size is limited by the quota that is assigned to    your organization.
   
   d.	Provide a name. The name is for display purposes only.
   
   e.	Optionally, provide a more detailed description of the volume.
   
   f.	Click **Create** to submit the information and close the dialog.

  Creating a volume can take a few moments.

3. Attach a volume to a virtual server.

   a.	Open the {{site.data.keyword.blockstorageshort}} service.
   
   b. Select a volume from the list of available volumes.
   
   c.	Click **Attach**.
   
   d.	In the Attach dialog, select an instance of a virtual server from the drop-down list. 
   
   e.	Optionally, specify the device to be used to attach this volume. If you do not specify the device, the system automatically selects the first available device on the virtual server.
   
   f.	Click **Attach** to submit the information and close the dialog.
   
   The volume is listed in the table of attached volumes with the information about the virtual server instance. The virtual server can now use the device to persist data. 
 
What's next?

Prepare the volume for use. For more information, see [Preparing Block Storage volumes](../BlockStorage/blockstorage_preparingvolume.html).

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


