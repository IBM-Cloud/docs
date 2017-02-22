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

# 下載物件

您可以下載已儲存的物件以進行檢閱，或透過使用者介面或 CLI 進行編輯。
{: shortdesc}


## 從使用者介面下載物件 {: #downloading-ui}

1. 為了避免意外覆寫所造成的資料毀損，請[設定物件版本化](/docs/services/ObjectStorage/os_versioning.html)。若不想要物件版本化，請視需要重新命名目錄或檔案，然後才進行下載。
2. 在服務實例儀表板中，選取具有您要下載之檔案的容器。
3. 選取檔案。
4. 在**動作**下拉功能表中，選取**下載檔案**。


## 使用 Swift CLI 下載物件 {: #downloading-cli}

1.  如果您未登入 {{site.data.keyword.Bluemix_notm}}，請登入包含 {{site.data.keyword.objectstorageshort}} 實例的組織和空間。

```
cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
```
{: pre}

2. 為了避免意外覆寫所造成的資料毀損，請[設定物件版本化](/docs/services/ObjectStorage/os_versioning.html)。若不想要物件版本化，請列出儲存庫中的現有檔案，並視需要重新命名目錄或檔案，然後才進行下載。

3. 執行下列指令來下載檔案：

```
swift download <container_name> <file_name>
```
{: pre}
