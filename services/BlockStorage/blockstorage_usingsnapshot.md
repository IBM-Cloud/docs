{:new_window: target="_blank"} 


# Using {{site.data.keyword.blockstorageshort}} snapshot {: #using-block-storage-snapshot} 

## Creating a snapshot {: #creating-snapshot} 

1.	Select the **Volumes** tab to get a list of volumes.
2.	Select the volume that you want to create a snapshot of in the unattached volumes column. Make sure that the volume you select is unattached. The selected volume is highlighted. 
3.	Click **Actions** and select **Create Snapshot** from the drop-down list.
4.	Give the snapshot a name and click **Create**.

**Note:** You cannot delete a volume while snapshots for the volume exist. 

## Creating a volume from a snapshot {: #creating-volume-from-snapshot}

1.	Select the **Snapshots** tab to get a list of snapshots.
2.	Select the snapshot that you want to create a volume from. The selected snapshot is highlighted.
3.	Click **Actions** and select **Create Volume** from the drop-down list.
4.	Give the new volume a name and optionally a new size and click **Create**. 

**Note:** The new volume size must be equal or greater than the snapshot size. 

## Deleting a snapshot {: #deleting-snapshot}

1.	Select the **Snapshots** tab to get a list of snapshots.
2.	Select the snapshot that you want to delete. The selected snapshot is highlighted.
3.	Click **Actions** and select **Delete**. 



