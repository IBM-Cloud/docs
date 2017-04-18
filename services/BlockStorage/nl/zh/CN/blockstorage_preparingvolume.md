{:new_window: target="_blank"}


# 准备 {{site.data.keyword.blockstorageshort}} 卷 
{: #preparing-block-storage-volume}

上次更新时间：2016 年 7 月 29 日
{: .last-updated}

  创建卷并将卷连接到虚拟服务器后，必须安装和准备卷，才能开始使用。
  
  **注**：相关命令可能会有所不同，具体取决于您的特定操作系统。有关更多信息，请参阅操作系统文档。以下步骤已使用 CentOS 虚拟服务器测试过。
  
  要准备卷，请执行以下步骤：

1. 登录到虚拟服务器。  

   <pre><code>ssh -i security_key_name.pem ibmcloud@xxx.xx.xx.xx</pre></code>

   **注：**要查找缺省用户标识、安全密钥名称和您的公共 IP 地址，请查看虚拟服务器的概述选项卡。缺省用户标识为 *ibmcloud*。有关使用 SSH 登录到虚拟服务器的信息，请参阅[从 Linux 终端登录到虚拟服务器实例](../../virtualmachines/vm_manage_instances.html#vm_login)。 

2. 验证卷是否已连接。  

   <pre><code>sudo su -</pre></code>
   
   **注：**如果 *sudo su* 命令对您的操作系统无效，请在每个命令之前使用 *sudo*。例如，*sudo fdisk -l*。
   
   <pre><code>fdisk -l</pre></code>

   卷信息会在信息性文本底部的位置列出。例如，*Disk /dev/vdb: 10.7 GB, 10737418240 bytes*。

3. 将磁盘分区。

   a. 启动 fdisk，然后创建新的分区。
    
     <pre><code>fdisk /dev/vdb</pre></code>

   b. 输入 **n** 以创建新的分区。
   
   c. 输入 **p** 以指定主分区。
   
   d. 要创建一个分区，请输入 **1**。
   
   e. 除非您有特定的需求，否则请在剩余的提示下选择缺省值，然后按 Enter 键。

   f. 输入 **w** 以写入分区。
   
   g. 验证新磁盘是否已创建。
   
     <pre><code>fdisk -l</pre></code>

     **注：**新磁盘名称通常是创建时所基于的分区的名称加上序号，例如 1。例如 *vdb1*。

4. 对卷进行格式化。 

   您必须对卷进行格式化，才能在卷中存储信息。此示例使用 ext4；不过，您可以使用任何受支持的文件系统。

   <pre><code>mkfs -t ext4 /dev/vdb1</pre></code>

    **注：**写入超级块和文件系统记帐信息的步骤可能需要额外的时间才能完成。当过程完成时，您会看到所列示的状态为*已完成*。

5. 安装卷。 

   a. 要使用卷，必须先安装卷。

      <pre><code>mkdir -p /mnt/myvolume</pre></code>
      
      <pre><code>mount /dev/vdb1 /mnt/myvolume</pre></code>

      其中，*myvolume* 是您选择的文件夹名称。

   b. 检查您的卷是否已列出且处于就绪状态。

      <pre><code>df -h</pre></code>

6. （可选）永久安装卷。 

   您可能想要永久安装卷，这样您就不需要在重新引导后重复安装。

   a. 找到您的卷的 UUID。

      <pre><code>blkid</pre></code>

   b. 复制所列出的 UUID。

   c. 编辑文件系统表信息。

      <pre><code>nano /etc/fstab</pre></code>      

   d. 将以下行（包括您的特定 UUID）粘贴到文件底部，然后保存。
   
      <pre><code>UUID=xxxxxx /mnt/myvolume ext4 defaults  0 2</pre></code>

   e. 要测试卷是否已永久安装，请重新引导虚拟服务器。

      <pre><code>reboot</pre></code>

  当虚拟服务器再次运行时，请登录到虚拟服务器，然后将目录切换到您所创建的新文件夹。例如，浏览到 **cd /mnt/myvolume**。

  您现在可以开始使用卷了。
