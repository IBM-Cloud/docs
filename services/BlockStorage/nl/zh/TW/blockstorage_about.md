{:new_window: target="_blank"}


# 關於 {{site.data.keyword.blockstorageshort}}
{: #about-block-storage}

前次更新：2016 年 8 月 1 日
{: .last-updated}

## 磁區 
{: #using-volumes-concept}

您可以使用 IBM {{site.data.keyword.blockstorageshort}} 來建立磁區，並將它們連接至虛擬伺服器。IBM {{site.data.keyword.virtualmachinesshort}} 預設不會有持續性儲存空間，並會在重新啟動時回復為預設映像。{{site.data.keyword.blockstorageshort}} 提供虛擬伺服器的持續性儲存空間。Block Storage 磁區中保存資料的時間超過虛擬伺服器的生命週期。{{site.data.keyword.blockstorageshort}} 使用 OpenStack Cinder 來管理磁區生命週期。

{{site.data.keyword.blockstorageshort}} 磁區是透過 {{site.data.keyword.blockstorageshort}} 服務實例所建立。您可以使用下列方式來連接磁區與虛擬伺服器：
  

* 指定您所提供的特定裝置。 
* 指定系統會自動選取可用的裝置名稱。 

虛擬伺服器直接利用指定的裝置來執行其 I/O 作業，與 {{site.data.keyword.blockstorageshort}} 服務無關。

## Snapshot 
{: #using-snapshots-concept}

您也可以建立磁區的區塊層 Snapshot。您無法在連接磁區時建立 Snapshot，因此產生的 Snapshot 將完全損毀。 

下一步為何？

建立磁區。如需相關資訊，請參閱[建立磁區](../BlockStorage/blockstorage_creatingvolume.html)。
