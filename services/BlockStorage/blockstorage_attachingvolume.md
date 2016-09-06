
{:new_window: target="_blank"}


# Attaching {{site.data.keyword.blockstorageshort}} volumes to a virtual server
{: #attaching-block-storage-volume}

Last updated: 02 September 2016
{: .last-updated}

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

What's next?

After the volume is created and you attach it to a virtual server, see [Preparing volumes](../BlockStorage/blockstorage_preparingvolume.html) to prepare it for use.
