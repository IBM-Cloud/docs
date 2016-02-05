{:new_window: target="_blank"} 

# 開始使用 {{site.data.keyword.blockstorageshort}}（測試版）

{{site.data.keyword.blockstoragefull}} 可讓您針對需要持續性儲存體的交易密集型工作量和執行時期，存取其區塊層儲存體。

您可以使用 IBM {{site.data.keyword.blockstorageshort}} for {{site.data.keyword.Bluemix_notm}} 來建立可連接至虛擬機器的 {{site.data.keyword.blockstorageshort}} 磁區。Block Storage 磁區中保存資料的時間超過虛擬機器的生命週期。IBM {{site.data.keyword.blockstorageshort}} 使用 OpenStack Cinder 來管理磁區生命週期。

{{site.data.keyword.blockstorageshort}} 磁區是透過 IBM {{site.data.keyword.blockstorageshort}} 服務實例而建立的。您可以將磁區連接至特定裝置下的虛擬機器，該特定裝置由您所提供或是由系統自動選取的可用裝置名稱。虛擬機器直接利用指定的裝置來執行其 I/O 作業，與 {{site.data.keyword.blockstorageshort}} 服務無關。

您也可以建立磁區的區塊層 Snapshot。{{site.data.keyword.blockstorageshort}} 服務不容許在連接磁區時建立 Snapshot，因此產生的 Snapshot 將完全損毀。 

## 如何建立 {{site.data.keyword.blockstorageshort}} 服務實例
若要在您的空間中建立 {{site.data.keyword.blockstorageshort}} 服務實例，請遵循下列步驟：
 
1.	移至 {{site.data.keyword.Bluemix_notm}} **型錄**標籤，然後在搜尋框中輸入 **{{site.data.keyword.blockstorageshort}}**，或移至**服務**，然後選取**儲存體**。按一下 **{{site.data.keyword.blockstorageshort}}** 服務。 
2.	輸入空間和服務名稱。選取方案，然後按一下**建立**。
 	
僅未連結的環境定義才支援 {{site.data.keyword.blockstorageshort}} 服務。 

即會在您的空間中建立一個 {{site.data.keyword.blockstorageshort}} 服務實例。您隨時可以按一下服務實例圖示，以開啟 {{site.data.keyword.blockstorageshort}} 使用者介面來管理磁區。

## {{site.data.keyword.blockstorageshort}} 使用者介面 (UI)
{{site.data.keyword.blockstorageshort}} 圖形使用者介面在視窗頂端為磁區和 Snapshot 提供有關儲存磁區、Snapshot 和總儲存體耗用量的進階概觀。 

標頭中包括前次使用者介面重新整理的日期和時間。必要的話，您可以使用重新整理圖示（圓形箭頭圖示）手動重新整理使用者介面。 

使用搜尋列，根據您輸入的字串尋找磁區。您鍵入時即會過濾表格，只顯示符合所輸入搜尋字串的磁區。

以下概述兩個標籤，分別為：磁區和 Snapshot。依預設，會選取磁區標籤。此標籤上的表格列出有關可用磁區和連接磁區的詳細資訊。表格中的每一列都顯示磁區的最重要內容。當您展開某列時可看見更多內容。連接的磁區還會顯示虛擬機器實例，以及磁區所連接的裝置。 

Snapshot 標籤顯示含有類似內容和行為的 Snapshot 表格。 

使用表格上方的「建立」圖示，可建立新的磁區或操作現有磁區。如果您是從 Snapshot 建立磁區，則也可以使用「動作」下拉清單。


## 磁區動作

### 建立磁區

1.	按一下**建立**，以開啟**建立磁區**對話框。
2.	提供您想要的磁區大小。不接受十進位數。此大小受限於指派給您的組織的配額。
3.	提供名稱。名稱僅供顯示使用。
4.	選擇性地提供磁區的其他詳細說明。 
5.	按一下**建立**，以提交資訊並關閉此對話框。 

建立磁區可能需要一些時間。 

### 刪除磁區

1.	選取您要刪除的磁區。
2.	按一下**刪除**。
3.	確認刪除此磁區。

您無法刪除已連接至虛擬機器的磁區。您必須先分離該磁區。

### 擴充磁區
您可以透過**擴充**動作來增加磁區大小。您無法縮減磁區大小。

1.	選取要擴充的磁區。
2.	按一下**擴充**。
3.	選取磁區的新的大小。提供磁區的新的大小總計。
4.	按一下**擴充**，以提交資訊並關閉此對話框。 

若要擴充，磁區必須處於**可用**狀態。 

### 連接及分離磁區與虛擬機器
利用特定的裝置名稱，將磁區作為裝置來與虛擬機器連接及分離。若要讓虛擬機器能夠將資料持續保存在磁區上，您必須將磁區連接至虛擬機器。

若要連接磁區，請遵循下列步驟： 

1.	從可用磁區清單中，選取一個磁區。
2.	按一下**連接**。
3.	在「連接」對話框中，從下拉清單中選取一個虛擬機器實例。 
4.	選擇性地指定用來連接此磁區的裝置。如果您未指定裝置，系統會自動選取虛擬機器上的第一個可用裝置。
5.	按一下**連接**，以提交資訊並關閉此對話框。

此磁區即會列在連接磁區表格中，其中包含虛擬機器實例的相關資訊。
虛擬機器現在即可使用此裝置來持續保存資料。 

若要分離磁區，請遵循下列步驟： 

1.	從連接磁區清單中，選取一個磁區。 
2.	按一下**分離**。
3.	在對話框中確認分離。 

分離之後，磁區即無法再用於虛擬機器實例中的 I/O 作業。在 {{site.data.keyword.blockstorageshort}} 服務使用者介面中，此磁區現在可用來連接至其他虛擬機器。

## Snapshot 動作

### 建立 Snapshot

1.	選取**磁區**標籤，以取得磁區清單。
2.	在不相連的磁區直欄中，選取您要建立 Snapshot 的磁區。請確定選取的磁區是不相連的。強調顯示選取的磁區。 
3.	按一下**動作**，然後從下拉清單中選取**建立 Snapshot**。
4.	指定 Snapshot 的名稱，然後按一下**建立**。

**附註：** 磁區有 Snapshot 存在時，您無法刪除此磁區。 

### 從 Snapshot 建立磁區

1.	選取 **Snapshot** 標籤，以取得 Snapshot 清單。
2.	選取您要從中建立磁區的 Snapshot。強調顯示選取的 Snapshot。
3.	按一下**動作**，然後從下拉清單中選取**建立磁區**。
4.	指定新磁區的名稱，並選擇性地指定新的大小，然後按一下**建立**。 

**附註：** 新的磁區大小必須等於或大於 Snapshot 的大小。 

### 刪除 Snapshot

1.	選取 **Snapshot** 標籤，以取得 Snapshot 清單。
2.	選取您要刪除的 Snapshot。強調顯示選取的 Snapshot。
3.	按一下**動作**，然後選取**刪除**。 



># 相關鏈結{:class="linklist"}
>## API 參考資料{:id="api"}
>* [OpenStack 區塊儲存體 (Cinder) API 第 2 版](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}
>
>{:elementKind="article" id="rellinks"}
