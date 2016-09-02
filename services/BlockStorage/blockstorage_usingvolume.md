{:new_window: target="_blank"} 

# Using {{site.data.keyword.blockstorageshort}} volume 
{: #using-block-storage-volume} 
Last updated: 02 September 2016
{: .last-updated}

To use volumes, follow these steps:

## Deleting a volume {: #deleting-volume}

1.	In the Bluemix UI, select **Console > Storage > Block Storage**.
2.	Select the volume that you want to delete.
3.	Click **Delete**.
4.	Confirm the deletion of this volume.

You cannot delete a volume that is attached to a virtual server. You must detach the volume first.

## Extending a volume {: #extending-volume}
You can increase the volume in size to up to ten times the original size through the **Extend** action. You cannot reduce the size of a volume.

1.	In the Bluemix UI, select **Console > Storage > Block Storage**.
2.	Select the volume to be extended.
3.	Click **Extend**.
4.	Select the new size of the volume. Provide the new total size of the volume.
5.	Click **Extend** to submit the information and close the dialog. 

To be extended, a volume must be in **Available** state. 

## Attaching and detaching a volume to a virtual server {: #attaching-detaching-volume}
Volumes are attached and detached from virtual servers as devices with a specific device name. For a virtual server to be able to persist data on a volume, you must attach the volume to the virtual server.

To attach a volume, follow these steps: 

1.	In the Bluemix UI, select **Console > Storage > Block Storage**.
2.	Select a volume from the list of available volumes.
3.	Click **Attach**.
4.	In the Attach dialog, select an instance of a virtual server from the drop-down list. 
5.	Optionally, specify the device to be used to attach this volume. If you do not specify the device, the system automatically selects the first available device on the virtual server.
6.	Click **Attach** to submit the information and close the dialog.

The volume is listed in the table of attached volumes with the information about the virtual server instance. 
The virtual server can now use the device to persist data. 

To detach a volume, follow these steps: 

1.	In the Bluemix UI, select **Console > Storage > Block Storage**.
2.	Select a volume from the list of attached volumes. 
3.	Click **Detach**.
4.	Confirm the detachment in the dialog. 

After it is detached, the volume is no longer available for I/O operations in the virtual server instance. In the {{site.data.keyword.blockstorageshort}} service UI, the volume is now available to be attached to other virtual servers.
