{:new_window: target="_blank"}


# 準備 {{site.data.keyword.blockstorageshort}} 磁區 
{: #preparing-block-storage-volume}

前次更新：2016 年 7 月 29 日
{: .last-updated}

  在您建立磁區並將它連接至虛擬伺服器之後，必須裝載及準備要使用的磁區。
  
  **附註**：相關指令視特定作業系統而有所不同。如需相關資訊，請參閱作業系統文件。下列步驟已使用 CentOS 虛擬伺服器進行過測試。
  
  若要準備磁區，請遵循下列步驟：

1. 登入虛擬伺服器。  

   <pre><code>ssh -i security_key_name.pem ibmcloud@xxx.xx.xx.xx</pre></code>

   **附註：**若要尋找預設使用者 ID、安全金鑰名稱及公用 IP 位址，請檢視虛擬伺服器的概觀標籤。預設使用者 ID 是 *ibmcloud*。如需使用 SSH 登入虛擬伺服器的相關資訊，請參閱[從 Linux 終端機登入虛擬伺服器實例](../../virtualmachines/vm_manage_instances.html#vm_login)。 

2. 驗證已連接磁區。  

   <pre><code>sudo su -</pre></code>
   
   **附註：**如果 *sudo su* 指令未作用於您的作業系統，請在每一個指令之前使用 *sudo*。例如，*sudo fdisk -l*。
   
   <pre><code>fdisk -l</pre></code>

   磁區資訊會列在資訊文字的底端。例如，*Disk /dev/vdb: 10.7 GB, 10737418240 bytes*。

3. 分割磁碟。

   a. 啟動 fdisk，並建立新的分割區。
    
     <pre><code>fdisk /dev/vdb</pre></code>

   b. 輸入 **n**，以建立新的分割區。
   
   c. 輸入 **p**，以指定主要分割區。
   
   d. 若要建立一個分割區，請輸入 **1**。
   
   e. 除非您具有特定需求，否則請在其餘提示上選取預設值，然後按 Enter 鍵。

   f. 輸入 **w**，以寫入分割區。
   
   g. 驗證已建立新的磁碟。
   
     <pre><code>fdisk -l</pre></code>

     **附註：**新的磁碟名稱通常是其建立所在分割區的名稱，再加上增量數字（例如 1）。例如，*vdb1*。

4. 格式化磁區。 

   您必須格式化其磁區，才能儲存資訊。此範例使用 ext4；不過，您可以使用任何支援的檔案系統。

   <pre><code>mkfs -t ext4 /dev/vdb1</pre></code>

    **附註：**寫入超級區塊及檔案系統帳戶資訊的步驟可能需要額外的時間才能完成。程序完成時，您將會看到狀態列為 *done*。

5. 裝載磁區。 

   a. 您必須裝載磁區，才能使用磁區。

      <pre><code>mkdir -p /mnt/myvolume</pre></code>
      
      <pre><code>mount /dev/vdb1 /mnt/myvolume</pre></code>

      其中 *myvolume* 是您選擇的資料夾名稱。

   b. 檢查磁區已列出且備妥。

      <pre><code>df -h</pre></code>

6. （選用）永久地裝載磁區。 

   您可能想要永久地裝載磁區，這樣，在重新開機之後就不需要重複裝載。

   a. 尋找磁區的 UUID。

      <pre><code>blkid</pre></code>

   b. 複製所列出的 UUID。

   c. 編輯檔案系統表格資訊。

      <pre><code>nano /etc/fstab</pre></code>      

   d. 將下列這一行（包括特定 UUID）貼入檔案的底端，並儲存。
   
      <pre><code>UUID=xxxxxx /mnt/myvolume ext4 defaults  0 2</pre></code>

   e. 若要測試是否已永久地裝載磁區，請重新啟動虛擬伺服器。

      <pre><code>reboot</pre></code>

  虛擬伺服器再次執行時，請登入虛擬伺服器，並將目錄切換至您所建立的新資料夾。例如，導覽至 **cd /mnt/myvolume**。

  您現在可以使用該磁區。
