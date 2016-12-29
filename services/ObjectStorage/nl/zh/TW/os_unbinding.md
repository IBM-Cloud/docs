---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 取消連結及取消佈建 {{site.data.keyword.objectstorageshort}} 實例 {: #deprovisioning-object-storage}

如果您已將 {{site.data.keyword.objectstorageshort}} 連結至 Cloud Foundry 應用程式且不再需要儲存空間，可以取消連結並取消佈建您的實例。
{: shortdesc}


## 取消連結實例
如果 Cloud Foundry 應用程式中不再需要 {{site.data.keyword.objectstorageshort}}，但您要維護已儲存的資料，則可以取消服務實例與應用程式的連結。

**注意**：如果您取消 {{site.data.keyword.objectstorageshort}} 實例與 {{site.data.keyword.Bluemix_notm}} 應用程式的連結，或刪除服務金鑰，則會刪除該實例的所有認證，而且無法還原。在取消佈建 {{site.data.keyword.objectstorageshort}} 實例之前，不會刪除 {{site.data.keyword.objectstorageshort}} 帳戶。重新連結或建立新的服務金鑰，即可產生新的雲端認證。

1. 若要查看已連結至您應用程式的服務，請按一下 Cloud Foundry 應用程式的連線標籤。
2. 找到您要取消連結的服務，然後按一下服務磚上的功能表按鈕。
3. 選取**取消連結服務**。
4. 清除**刪除服務實例**方框，然後按一下**確定**。
5. 按一下**重新編譯打包**，讓變更生效。



## 取消佈建實例

如果您有不再需要的 {{site.data.keyword.objectstorageshort}} 實例，則可以刪除該實例。

**注意**：當您取消佈建 {{site.data.keyword.objectstorageshort}} 實例時，會刪除雲端專案及 Swift 帳戶。會刪除已取消佈建實例中的所有容器及物件，而且無法還原。

1. 若要查看已連結至您應用程式的服務，請按一下 Cloud Foundry 應用程式的連線標籤。
2. 找到您要取消連結的服務，然後按一下服務磚上的功能表按鈕。
3. 選取**刪除服務**。
4. 按一下**刪除**以進行確認。
5. 按一下**重新編譯打包**，讓變更生效。
