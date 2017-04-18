{:new_window: target="_blank"} 


# Using {{site.data.keyword.blockstorageshort}} snapshot {: #using-block-storage-snapshot}  (Deprecated)
Last updated: 24 October 2016
{: .last-updated}

**This service is deprecated:** Existing volumes can be used until 24 December 2016. For more information, see [{{site.data.keyword.blockstorageshort}} (Beta) is deprecated](../BlockStorage/index.html).

Review the following information to create a snapshot, create a volume from a snapshot, or delete a snapshot. Alternatively, you can manage your volumes and snapshots using the OpenStackClient (OSC) command line. For more information, see [Managing block storage volumes using the OSC command line](../../virtualmachines/vm_manage_volumes.html#vm_manage_volumes).

## Creating a snapshot {: #creating-snapshot} 

To create a snapshot, follow these steps:

1.  In the Bluemix UI, select **Console > Storage**.
2.  Select the Block Storage instance you previously provisioned.
3.	Click the Manage tab.
4.	On the Manage page, click the **Volumes** tab to get a list of volumes.
5.	Select the volume that you want to create a snapshot of in the unattached volumes column. Make sure that the volume you select is   unattached. The selected volume is highlighted. 
6.	From the Actions drop-down menu, click **Create Snapshot**.
7.	Give the snapshot a name and click **Create**.

**Note:** 

* You cannot delete a volume while snapshots for the volume exist. 
* The size of the snapshot is automatically set to be the same as that of the original volume.

## Creating a volume from a snapshot {: #creating-volume-from-snapshot}

To create a volume from a snapshot, follow these steps:

1.  In the Bluemix UI, select **Console > Storage**.
2.  Select the Block Storage instance you previously provisioned.
3.	Click the Manage tab.
4.	On the Manage page, click the **Snapshots** tab to get a list of snapshots.
5.	Select the snapshot that you want to create a volume from. The selected snapshot is highlighted.
6.	From the Actions drop-down menu, click **Create Volume**.
7.	Give the new volume a name and optionally a new size and click **Create**. 

**Note:** The new volume size must be equal or greater than the snapshot size. 

## Deleting a snapshot {: #deleting-snapshot}

To delete a snapshot, follow these steps:

1.  In the Bluemix UI, select **Console > Storage**.
2.  Select the Block Storage instance you previously provisioned.
3.	Click the Manage tab.
4.	On the Manage page, click the **Snapshots** tab to get a list of snapshots.
5.	Select the snapshot that you want to delete. The selected snapshot is highlighted.
6.	From the Actions drop-down, click **Delete**. 



