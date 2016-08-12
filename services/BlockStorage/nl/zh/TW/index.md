{:new_window: target="_blank"} 

# 開始使用 {{site.data.keyword.blockstorageshort}}（測試版）

*前次更新：2016 年 7 月 15 日*
{: .last-updated}

{{site.data.keyword.blockstoragefull}} 可讓您針對需要持續性儲存空間的交易密集型工作負載和運行環境，存取其區塊層儲存空間。

您可以使用 IBM {{site.data.keyword.blockstorageshort}} for {{site.data.keyword.Bluemix_notm}} 來建立可連接至虛擬伺服器的 {{site.data.keyword.blockstorageshort}} 磁區。Block Storage 磁區中保存資料的時間超過虛擬伺服器的生命週期。IBM {{site.data.keyword.blockstorageshort}} 使用 OpenStack Cinder 來管理磁區生命週期。

{{site.data.keyword.blockstorageshort}} 磁區是透過 IBM {{site.data.keyword.blockstorageshort}} 服務實例而建立的。您可以將磁區連接至特定裝置下的虛擬伺服器，該特定裝置由您所提供或是由系統自動選取的可用裝置名稱。虛擬伺服器直接利用指定的裝置來執行其 I/O 作業，與 {{site.data.keyword.blockstorageshort}} 服務無關。

您也可以建立磁區的區塊層 Snapshot。{{site.data.keyword.blockstorageshort}} 服務不容許在連接磁區時建立 Snapshot，因此產生的 Snapshot 將完全損毀。 


## 如何建立 {{site.data.keyword.blockstorageshort}} 服務實例
若要在您的空間中建立 {{site.data.keyword.blockstorageshort}} 服務實例，請遵循下列步驟：
 
1.	移至 {{site.data.keyword.Bluemix_notm}} **型錄**標籤，然後在搜尋框中輸入 **{{site.data.keyword.blockstorageshort}}**，或移至**服務**，然後選取**儲存空間**。按一下 **{{site.data.keyword.blockstorageshort}}** 服務。 
2.	輸入空間和服務名稱。選取方案，然後按一下**建立**。
 	
僅未連結的環境定義才支援 {{site.data.keyword.blockstorageshort}} 服務。 

即會在您的空間中建立一個 {{site.data.keyword.blockstorageshort}} 服務實例。您隨時可以按一下服務實例圖示，以開啟 {{site.data.keyword.blockstorageshort}} 使用者介面來管理磁區。



## 使用 {{site.data.keyword.blockstorageshort}} 使用者介面 (UI) {: #using-block-storage-ui}
{{site.data.keyword.blockstorageshort}} 圖形使用者介面在視窗頂端為磁區和 Snapshot 提供有關儲存磁區、Snapshot 和總儲存空間耗用量的進階概觀。 

標頭中包括前次使用者介面重新整理的日期和時間。必要的話，您可以使用重新整理圖示（圓形箭頭圖示）手動重新整理使用者介面。 

使用搜尋列，根據您輸入的字串尋找磁區。您鍵入時即會過濾表格，只顯示符合所輸入搜尋字串的磁區。

以下概述兩個標籤，分別為：磁區和 Snapshot。依預設，會選取磁區標籤。此標籤上的表格列出有關可用磁區和連接磁區的詳細資訊。表格中的每一列都顯示磁區的最重要內容。當您展開某列時可看見更多內容。連接的磁區還會顯示虛擬伺服器實例，以及磁區所連接的裝置。 

Snapshot 標籤顯示含有類似內容和行為的 Snapshot 表格。 

使用表格上方的「建立」圖示，可建立新的磁區或操作現有磁區。如果您是從 Snapshot 建立磁區，則也可以使用「動作」下拉清單。




## 連接磁區與虛擬伺服器 {: #attaching-detaching-volume}
利用特定的裝置名稱，將磁區作為裝置來與虛擬伺服器連接及分離。若要讓虛擬伺服器能夠將資料持續保存在磁區上，您必須將磁區連接至虛擬伺服器。

若要連接磁區，請遵循下列步驟： 

1.	從可用磁區清單中，選取一個磁區。
2.	按一下**連接**。
3.	在「連接」對話框中，從下拉清單中選取一個虛擬伺服器實例。 
4.	選擇性地指定用來連接此磁區的裝置。如果您未指定裝置，系統會自動選取虛擬伺服器上的第一個可用裝置。
5.	按一下**連接**，以提交資訊並關閉此對話框。

此磁區即會列在連接磁區表格中，其中包含虛擬伺服器實例的相關資訊。虛擬伺服器現在即可使用此裝置來持續保存資料。 


# 相關鏈結
{: #rellinks}

## API 參考資料
{: #api}
* [OpenStack Block Storage (Cinder) API 第 2 版](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}

