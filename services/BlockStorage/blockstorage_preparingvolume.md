{:new_window: target="_blank"}


# Preparing {{site.data.keyword.blockstorageshort}} volumes (Deprecated)
{: #preparing-block-storage-volume}

Last updated: 24 October 2016
{: .last-updated}

**This service is deprecated:** Existing volumes can be used until 24 December 2016. For more information, see [{{site.data.keyword.blockstorageshort}} (Beta) is deprecated](../BlockStorage/index.html).

  After you create your volume and attach it to a virtual server, you must mount and prepare the volume to be used.
  
  **Note**: Relevant commands may vary depending on your specific operating system. For more information, see your operating system documentation. The following steps were tested using a CentOS virtual server.
  
  To prepare a volume, follow these steps:

1. Log in to the virtual server.  

   <pre><code>ssh -i security_key_name.pem ibmcloud@xxx.xx.xx.xx</pre></code>

   **Note:** To find the default user ID, security key name and your public IP address, view the overview tab of the virtual server. The default user ID is *ibmcloud*. For information about logging in to the virtual server using SSH, see [Logging in to a virtual server instance from a Linux terminal](../../virtualmachines/vm_manage_instances.html#vm_login). 

2. Verify that the volume is attached.  

   <pre><code>sudo su -</pre></code>
   
   **Note:** If the *sudo su* command does not work for your operating system, use *sudo* before each command. For example, *sudo fdisk -l*.
   
   <pre><code>fdisk -l</pre></code>

   The volume information is listed towards the bottom of the informational text. For example, *Disk /dev/vdb: 10.7 GB, 10737418240 bytes*. The disk device relates to the device that was requested or automatically selected at the time of attachment.

3. Partition the disk.

   a. Start fdisk and create a new partition.
    
     <pre><code>fdisk /dev/vdb</pre></code>

   b. Enter **n** to create a new partition.
   
   c. Enter **p** to specify the primary partition.
   
   d. To create one partition, enter **1**.
   
   e. Unless you have specific requirements, select default values on the remaining prompts and press Enter.

   f. Enter **w** to write the partition.
   
   g. Verify the new disk is created.
   
     <pre><code>fdisk -l</pre></code>

     **Note:** The new disk name is usually the name of the partition it was created on, plus an incremental number, such as 1. For example, *vdb1*.

4. Format the volume. 

   You must format the volume for it to store information. This example uses ext4; however, you can use whatever file system is supported.

   <pre><code>mkfs -t ext4 /dev/vdb1</pre></code>

    **Note:** The step to write superblocks and filesystem accounting information might take extra time to complete. When the process is finished, you will see *done* listed as the status.

5. Mount the volume. 

   a. You must mount the volume to use it.

      <pre><code>mkdir -p /mnt/myvolume</pre></code>
      
      <pre><code>mount /dev/vdb1 /mnt/myvolume</pre></code>

      where *myvolume* is a folder name of your choice.

   b. Check that your volume is listed and ready.

      <pre><code>df -h</pre></code>

6. (Optional) Mount the volume permanently. 

   You might want to mount the volume permanently, so you do not need to repeat the mount after a reboot.

   a. Locate the UUID for your volume.

      <pre><code>blkid</pre></code>

   b. Copy the UUID that is listed.

   c. Edit the file systems table information.

      <pre><code>nano /etc/fstab</pre></code>      

   d. Paste the following line, including your specific UUID, to the bottom of the file and save.
   
      <pre><code>UUID=xxxxxx /mnt/myvolume ext4 defaults  0 2</pre></code>

   e. To test that the volume is permanently mounted, reboot the virtual server.

      <pre><code>reboot</pre></code>

  When the virtual server is running again, log in to the virtual server and change directories to the new folder you created. For example, navigate to **cd /mnt/myvolume**.

  You can now use the volume.
