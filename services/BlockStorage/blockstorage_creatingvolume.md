{:new_window: target="_blank"}


# Creating {{site.data.keyword.blockstorageshort}} volumes (Deprecated)
{: #creating-block-storage-volume}

Last updated: 24 October 2016
{: .last-updated}

**This service is deprecated:** Existing volumes can be used until 24 December 2016. For more information, see [{{site.data.keyword.blockstorageshort}} (Beta) is deprecated](../BlockStorage/index.html).

To create a volume, follow these steps:

1.  In the Bluemix UI, select **Console > Storage**.
2.  Select the Block Storage instance you previously provisioned.
3.	Click **Create** to start the **Create Volume** dialog.
4.	Provide the size of the volume that you want. 
    
    **Note**: Decimal numbers are not accepted. The size is limited by the quota that is assigned to your     organization.
5.	Provide a name. 

    **Note**: The name is for display purposes only.
    
6.	Optionally, provide a more detailed description of the volume.
7.	Click **Create** to submit the information and close the dialog.

Creating a volume can take a few moments. 

Alternatively, you can use the OpenStackClient command line to create a volume. For more information, see [Creating a block storage volume by using the OSC client](../../virtualmachines/vm_manage_volumes.html#vm_create_volume_cli).

What's next?

After the volume is created, attach it to a virtual server. For more information, see [Attaching volumes to a virtual server](../BlockStorage/blockstorage_attachingvolume.html).
