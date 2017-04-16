
{:new_window: target="_blank"}


# Attaching {{site.data.keyword.blockstorageshort}} volumes to a virtual server (Deprecated)
{: #attaching-block-storage-volume}

Last updated: 24 October 2016
{: .last-updated}

**This service is deprecated:** Existing volumes can be used until 24 December 2016. For more information, see [{{site.data.keyword.blockstorageshort}} (Beta) is deprecated](../BlockStorage/index.html).

Volumes are attached and detached from virtual servers as devices with a specific device name. For a virtual server to be able to persist data on a volume, you must attach the volume to the virtual server.

To attach a volume, follow these steps:

1.  In the Bluemix UI, select **Console > Storage**.
2.  Select the Block Storage instance you previously provisioned.
3.	Select a volume from the list of available volumes.
4.	Click **Attach**.
5.	In the Attach dialog, select an instance of a virtual server from the drop-down list.
6.	Optionally, specify the device to be used to attach this volume. 
    
    **Note**: If you do not specify the device, the system automatically selects the first available device on the virtual server.

7.	Click **Attach** to submit the information and close the dialog.

The volume is listed in the table of attached volumes with the information about the virtual server instance.
The virtual server can now use the device to persist data. 

What's next?

After the volume is created and you attach it to a virtual server, see [Preparing volumes](../BlockStorage/blockstorage_preparingvolume.html) to prepare it for use.
