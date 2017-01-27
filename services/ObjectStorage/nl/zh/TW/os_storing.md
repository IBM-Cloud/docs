---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 儲存物件

您可以利用使用者介面或 CLI 將物件上傳至儲存空間。上傳物件時受限於 5 GB 的單次上傳大小上限。不過，您可以將較大的物件分解成較小的物件，來上傳它們。
{: shortdesc}


## 透過 UI 將物件儲存至容器 {: #storing-ui}

**附註**：當您上傳同名的檔案時，{{site.data.keyword.objectstorageshort}} 會將儲存的檔案取代為新的檔案。如果您下載檔案，並進行編輯，請務必將檔案指定為其他名稱，或者在上傳之前[設定物件版本化](/docs/services/ObjectStorage/os_versioning.html)，以保留檔案的兩個版本。


1. 從您的服務實例儀表板的**動作**下拉功能表新增容器。
2. 為容器命名，然後按一下**建立**。
3. 從**動作**下拉功能表，選取**新增檔案**。即會開啟對話框。
4. 選取一個以上要上傳的檔案，然按一下**開啟**。



## 透過 CLI 將物件儲存至容器 {: #storing-cli}

1. 如果您未登入 {{site.data.keyword.Bluemix_notm}}，請登入包含 {{site.data.keyword.objectstorageshort}} 實例的組織和空間。

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. 執行下列指令，以建立 {{site.data.keyword.objectstorageshort}} 容器。您現在可以設定 *container_name* 變數。

  ```
  swift post <container_name>
  ```
  {: pre}

**附註**：如果收到錯誤訊息，請確認已安裝[必備軟體](/docs/services/ObjectStorage/os_configuring.html#install-swift-client)。

3. 選用：若要驗證已建立容器，請執行下列指令來列出容器。

  ```
  swift list
  ```
  {: pre}

4. 為了避免意外覆寫所造成的資料毀損，請[設定物件版本化](/docs/services/ObjectStorage/os_versioning.html)。若不想要物件版本化，請列出儲存庫中的現有檔案，並視需要重新命名目錄或檔案，然後才進行上傳。

5. 執行下列指令，以將檔案上傳至容器。

  ```
  swift upload <container_name> <file_name>
  ```
  {: pre}

  **附註**：若要上傳超過 5 GB 的檔案，[需要額外的步驟](/docs/services/ObjectStorage/os_large_files.html)。

6. 選用：若要驗證上傳成功，請執行下列指令來檢視容器內容。

  ```
  swift list <container_name>
  ```
  {: pre}
