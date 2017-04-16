{:new_window: target="_blank"} 

# Using {{site.data.keyword.blockstorageshort}} volume (Deprecated)
{: #using-block-storage-volume} 
Last updated: 24 October 2016
{: .last-updated}

**This service is deprecated:** Existing volumes can be used until 24 December 2016. For more information, see [{{site.data.keyword.blockstorageshort}} (Beta) is deprecated](../BlockStorage/index.html).

Review the following information to delete, extend, attach or detach your volumes. Alternatively, you can manage your volumes and snapshots using the OpenStackClient (OSC) command line. For more information, see [Managing block storage volumes using the OSC command line](../../virtualmachines/vm_manage_volumes.html#vm_manage_volumes).

## Deleting a volume {: #deleting-volume}

You cannot delete a volume that is attached to a virtual server. You must detach the volume first. Deleting the volume makes the volume inaccessible for future use and the data in it is lost. Also, you cannot delete volumes that have associated snapshots.

To delete a volume, follow these steps:

1.  In the Bluemix UI, select **Console > Storage**.
2.  Select the Block Storage instance you previously provisioned.
3.	Select the volume that you want to delete.
4.	From the Actions drop-down menu, click **Delete**.
5.	Confirm the deletion of this volume.


## Extending a volume {: #extending-volume}
You can increase the volume in size to up to ten times the original size through the **Extend** action. You cannot reduce the size of a volume.

To be extended, a volume must be in **Available** state. After you extend the volume, you must notify the filesystem (such as ext4) that the disk has been extended by resizing the filesystem to the new size.

To extend a volume, follow these steps:

1.  In the Bluemix UI, select **Console > Storage**.
2.  Select the Block Storage instance you previously provisioned.
3.	Select the volume to be extended.
4.	From the Actions drop-down menu, click **Extend**.
5.	Select the new size of the volume. Provide the new total size of the volume.
6.	Click **Extend** to submit the information and close the dialog. 


## Attaching and detaching a volume to a virtual server {: #attaching-detaching-volume}
Volumes are attached and detached from virtual servers as devices with a specific device name. For a virtual server to be able to persist data on a volume, you must attach the volume to the virtual server.

To attach a volume, follow these steps: 

1.  In the Bluemix UI, select **Console > Storage**.
2.  Select the Block Storage instance you previously provisioned.
3.	Select a volume from the list of available volumes.
4.	From the Actions drop-down menu, click **Attach**.
5.	In the Attach dialog, select an instance of a virtual server from the drop-down list. 
6.	Optionally, specify the device to be used to attach this volume. If you do not specify the device, the system automatically selects the first available device on the virtual server.
7.	Click **Attach** to submit the information and close the dialog.

The volume is listed in the table of attached volumes with the information about the virtual server instance. 
The virtual server can now use the device to persist data. 

When you are ready to detach a volume, you must prepare the virtual server for detachment. For example, stop any applications that are using the filesystem. Also, unmount the device from within the virtual server instance.

To detach a volume, follow these steps: 

1.  In the Bluemix UI, select **Console > Storage**.
2.  Select the Block Storage instance you previously provisioned.
3.	Select a volume from the list of attached volumes. 
4.	From the Actions drop-down menu, click **Detach**.
5.	Confirm the detachment in the dialog. 

After it is detached, the volume is no longer available for I/O operations in the virtual server instance. In the {{site.data.keyword.blockstorageshort}} service UI, the volume is now available to be attached to other virtual servers.
