{:new_window: target="_blank"} 

# 開始使用 {{site.data.keyword.blockstorageshort}}（測試版）

前次更新：2016 年 7 月 29 日
{: .last-updated}

{{site.data.keyword.blockstoragefull}} 可讓您針對需要持續性儲存空間的交易密集型工作負載和運行環境，存取其區塊層儲存空間。您可以使用 {{site.data.keyword.blockstorageshort}} 服務來管理磁區生命週期、連接磁區與 IBM Virtual Servers，以及建立 Block Storage 磁區的 Snapshot。

開始之前，請檢閱下列資訊。

* 只有在未連結的環境定義中才支援 {{site.data.keyword.blockstorageshort}} 服務。 
* 您必須建立 IBM {{site.data.keyword.virtualmachinesshort}}，才能連接 Block Storage 磁區。若要進一步瞭解如何搭配使用 Block Storage 磁區與 IBM {{site.data.keyword.virtualmachinesshort}}，請參閱 [Block Storage 磁區及 IBM Virtual Servers](../../virtualmachines/vm_create.html#storage_BS)。 

請完成下列步驟，以開始使用 {{site.data.keyword.blockstorageshort}}：

1. 建立磁區。
   
   a. 開啟 {{site.data.keyword.blockstorageshort}} 服務。

   b. 按一下**建立**，以啟動**建立磁區**對話框。

   c.	提供您想要的磁區大小。不接受十進位數。此大小受限於指派給您的組織的配額。
   
   d.	提供名稱。名稱僅供顯示使用。
   
   e.	選擇性地提供磁區的其他詳細說明。
   
   f.	按一下**建立**，以提交資訊並關閉此對話框。

  建立磁區可能需要一些時間。

2. 連接磁區與虛擬伺服器。

   a. 開啟 {{site.data.keyword.blockstorageshort}} 服務。
   
   b. 從可用磁區清單中，選取一個磁區。
   
   c.	按一下**連接**。
   
   d.	在「連接」對話框中，從下拉清單中選取一個虛擬伺服器實例。 
   
   e.	選擇性地指定要用來連接此磁區的裝置。如果您未指定裝置，系統會自動選取虛擬伺服器上的第一個可用裝置。
   
   f.	按一下**連接**，以提交資訊並關閉此對話框。
   
   此磁區即會列在連接磁區表格中，其中包含虛擬伺服器實例的相關資訊。虛擬伺服器現在即可使用此裝置來持續保存資料。 
 
下一步為何？

請準備要使用的磁區。如需相關資訊，請參閱[準備磁區](../BlockStorage/blockstorage_preparingvolume.html)。

# 相關鏈結
{: #rellinks}

## 指導教學及範例
{:id="samples"}

* [如何搭配使用 IBM Block Storage for Bluemix 與 IBM Virtual Servers](https://developer.ibm.com/bluemix/2016/02/24/use-block-storage-for-bluemix-with-virtual-servers/){: new_window}
* [開始使用 IBM Block Storage for Bluemix](https://developer.ibm.com/bluemix/2016/02/15/getting-started-with-block-storage/){: new_window}
* [IBM Block Storage for Bluemix 展示](https://www.youtube.com/watch?v=3gCIHYKU1rE&list=PLzpeuWUENMK2d3L5qCITo2GQEt-7r0oqm&index=45){: new_window}

## API 參考資料
{: #api}
* [OpenStack Block Storage (Cinder) API 第 2 版](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}

