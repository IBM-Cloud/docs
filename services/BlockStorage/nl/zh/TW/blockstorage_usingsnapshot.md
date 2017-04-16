{:new_window: target="_blank"} 


# 使用 {{site.data.keyword.blockstorageshort}} Snapshot {: #using-block-storage-snapshot} 
前次更新：2016 年 9 月 7 日
{: .last-updated}

若要使用 Snapshot，請遵循下列步驟：

## 建立 Snapshot {: #creating-snapshot} 

1.  在 Bluemix 使用者介面中，選取**主控台 > 儲存空間**。
2.  選取您先前佈建的 Block Storage 實例。
3.	按一下「管理」標籤。
4.	在「管理」頁面上，按一下**磁區**標籤，以取得磁區清單。
5.	在不相連的磁區直欄中，選取您要建立 Snapshot 的磁區。請確定選取的磁區是不相連的。強調顯示選取的磁區。 
6.	從「動作」下拉功能表，按一下**建立 Snapshot**。
7.	指定 Snapshot 的名稱，然後按一下**建立**。

**附註：** 

* 磁區有 Snapshot 存在時，您無法刪除此磁區。 
* Snapshot 的大小會自動設為與原始磁區的大小相同。

## 從 Snapshot 建立磁區 {: #creating-volume-from-snapshot}

1.  在 Bluemix 使用者介面中，選取**主控台 > 儲存空間**。
2.  選取您先前佈建的 Block Storage 實例。
3.	按一下「管理」標籤。
4.	在「管理」頁面上，按一下 **Snapshot** 標籤，以取得 Snapshot 清單。
5.	選取您要從中建立磁區的 Snapshot。強調顯示選取的 Snapshot。
6.	從「動作」下拉功能表，按一下**建立磁區**。
7.	指定新磁區的名稱，並選擇性地指定新的大小，然後按一下**建立**。 

**附註：** 新的磁區大小必須等於或大於 Snapshot 的大小。 

## 刪除 Snapshot {: #deleting-snapshot}

1.  在 Bluemix 使用者介面中，選取**主控台 > 儲存空間**。
2.  選取您先前佈建的 Block Storage 實例。
3.	按一下「管理」標籤。
4.	在「管理」頁面上，按一下 **Snapshot** 標籤，以取得 Snapshot 清單。
5.	選取您要刪除的 Snapshot。強調顯示選取的 Snapshot。
6.	從「動作」下拉功能表，按一下**刪除**。 



