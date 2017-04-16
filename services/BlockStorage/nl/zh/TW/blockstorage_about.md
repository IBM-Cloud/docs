{:new_window: target="_blank"}


# 關於 {{site.data.keyword.blockstorageshort}}
{: #about-block-storage}

前次更新：2016 年 9 月 7 日
{: .last-updated}

IBM {{site.data.keyword.blockstorageshort}} 服務容許您將持續性儲存空間連接至虛擬伺服器。若要使用儲存空間，請將 Block Storage 磁區連接至虛擬伺服器。Block Storage 磁區中保存資料的時間超過虛擬伺服器的生命週期。這表示您可以從伺服器實例分離磁區，然後重新連接至另一個伺服器實例，而不需要變更資料。{{site.data.keyword.blockstorageshort}} 使用 OpenStack Cinder 來管理磁區生命週期。 

儲存空間在區塊裝置上存取，您可以對此裝置進行分割、格式化及裝載（例如裝載到 /dev/vdb）。資料會持續保存，直到您刪除它為止。 

## 磁區 
{: #using-volumes-concept}

{{site.data.keyword.blockstorageshort}} 磁區是透過 {{site.data.keyword.blockstorageshort}} 服務實例所建立。您可以使用下列方式來連接磁區與虛擬伺服器：
  

* 指定您所提供的特定裝置。 
* 指定系統會自動選取可用的裝置名稱。 

虛擬伺服器直接利用指定的裝置來執行其 I/O 作業，與 {{site.data.keyword.blockstorageshort}} 服務無關。

## Snapshot 
{: #using-snapshots-concept}

您也可以建立磁區的區塊層 Snapshot。Snapshot 會擷取 Block Storage 磁區在特定復原點的資料。您可以使用 Snapshot 執行資料的增量備份。那表示，Snapshot 會存在於與原始磁區相同的儲存空間。因此，Snapshot 不是足夠的災難回復策略。

**附註**：磁區連接至伺服器實例時無法建立 Snapshot。 

當您從 Snapshot 建立磁區時會建立新磁區，它會以您取得 Snapshot 當時原始磁區的相同狀態存在。 

從 Snapshot 建立磁區有下列影響：

* 不會移除現有磁區。
* 在取得相關 Snapshot 之後建立、修改或刪除的資料，不會包含在新磁區中。

下一步為何？

建立磁區。如需相關資訊，請參閱[建立磁區](../BlockStorage/blockstorage_creatingvolume.html)。
