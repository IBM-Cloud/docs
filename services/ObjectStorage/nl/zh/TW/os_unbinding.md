---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 取消連結及取消佈建 {{site.data.keyword.objectstorageshort}} 實例 {: #deprovisioning-object-storage}

*前次更新：2016 年 10 月 19 日*
{: .last-updated}


### 取消連結實例
如果 Cloud Foundry 應用程式中不再需要 {{site.data.keyword.objectstorageshort}}，但您要維護已儲存的資料，則可以取消服務實例與應用程式的連結。

**注意**：如果您取消 {{site.data.keyword.objectstorageshort}} 實例與 {{site.data.keyword.Bluemix_notm}} 應用程式的連結，或刪除服務金鑰，則會刪除該實例的所有認證，而且無法還原。

1. 在 {{site.data.keyword.Bluemix_notm}} 主控台中，開啟應用程式詳細資料。
2. 選取 {{site.data.keyword.objectstorageshort}} 實例，然後按一下**取消連結服務**。
3. 按一下**移除**。
4. 按一下**重新編譯打包**。



### 取消佈建實例

如果您有不再需要且已取消連結的 {{site.data.keyword.objectstorageshort}} 實例，則可以刪除該實例。

**注意**：當您取消佈建 {{site.data.keyword.objectstorageshort}} 實例時，會刪除雲端專案。會刪除已取消佈建實例中的所有容器及物件，而且無法還原。

1. 在 {{site.data.keyword.Bluemix_notm}} 主控台中，開啟應用程式詳細資料。
2. 選取 {{site.data.keyword.objectstorageshort}} 實例，然後按一下**刪除**。
3. 按一下**重新編譯打包**。
