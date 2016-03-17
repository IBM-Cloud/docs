{:new_window: target="_blank"} 

# Getting started with {{site.data.keyword.blockstorageshort}} (BETA)

{{site.data.keyword.blockstoragefull}} provides access to block level storage for transaction intensive workloads and runtimes in need of persistent storage.

You can use IBM {{site.data.keyword.blockstorageshort}} for {{site.data.keyword.Bluemix_notm}} to create {{site.data.keyword.blockstorageshort}} volumes that can be attached to virtual servers. The data in block storage volumes persists beyond the lifecycle of your virtual servers. IBM {{site.data.keyword.blockstorageshort}} uses OpenStack Cinder to manage the volume lifecycle.

{{site.data.keyword.blockstorageshort}} volumes are created through an IBM {{site.data.keyword.blockstorageshort}} service instance. You can attach the volumes to a virtual server under a particular device that you provide or the system can automatically select an available device name. The virtual server performs its I/O operations directly with the specified device independent of the {{site.data.keyword.blockstorageshort}} service.

You can also create block-level snapshots of volumes. {{site.data.keyword.blockstorageshort}} service does not allow the creation of snapshots while the volume is attached, so the resulting snapshots will be crash-consistent. 


## How to create a {{site.data.keyword.blockstorageshort}} service instance
To create an instance of the {{site.data.keyword.blockstorageshort}} service in your space, follow these steps:
 
1.	Go to the {{site.data.keyword.Bluemix_notm}} **Catalog** tab and enter **{{site.data.keyword.blockstorageshort}}** into the search box, or go to **Services** and select **Storage**. Click the **{{site.data.keyword.blockstorageshort}}** service. 
2.	Enter a space and service name. Select the plan and click **Create**.
 	
The {{site.data.keyword.blockstorageshort}} service is only supported in an unbound context. 

An instance of {{site.data.keyword.blockstorageshort}} service is created in your space. You can open the {{site.data.keyword.blockstorageshort}} UI to manage volumes anytime by clicking the service instance icon.



## Using {{site.data.keyword.blockstorageshort}} user interface (UI) {: #using-block-storage-ui}
The {{site.data.keyword.blockstorageshort}} graphical user interface provides a high-level overview of your storage volumes, snapshots, and total storage consumption for both volumes and snapshots at the top of the window. 

The header includes the date and time of the last UI refresh. You can use the refresh icon (a circular arrow icon) to refresh the UI manually, if needed. 

Use the search bar to find volumes based on the string that you enter. The tables are filtered as you type to show only the volumes that match the entered search string.

Below the overview are two tabs for volumes and snapshots. The volume tab is selected by default. The tables on this tab list detailed information about available and attached volumes. Each row in a table shows the most important properties of a volume. More properties are visible when you expand a row. Attached volumes also show the virtual server instance and the device that the volume is attached to. 

The snapshot tab shows a table of snapshots with similar properties and behavior. 

Use the Create icon above the tables to create a new volume or to manipulate existing ones. If you are creating a volume from a snapshot, you can also use the Actions drop-down list.




## Attaching a volume to a virtual server {: #attaching-detaching-volume}
Volumes are attached and detached from virtual servers as devices with a specific device name. For a virtual server to be able to persist data on a volume, you must attach the volume to the virtual server.

To attach a volume, follow these steps: 

1.	Select a volume from the list of available volumes.
2.	Click **Attach**.
3.	In the Attach dialog, select an instance of a virtual server from the drop-down list. 
4.	Optionally, specify the device to be used to attach this volume. If you do not specify the device, the system automatically selects the first available device on the virtual server.
5.	Click **Attach** to submit the information and close the dialog.

The volume is listed in the table of attached volumes with the information about the virtual server instance. 
The virtual server can now use the device to persist data. 



># Related Links {:class="linklist"}
>## API Reference {:id="api"}
>* [OpenStack Block Storage (Cinder) API v2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}
>
>{:elementKind="article" id="rellinks"}
