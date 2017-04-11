---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 刪除物件

當您不再需要它們時，可以從儲存空間實例刪除物件和容器。您可以手動刪除，也可以[排定時間](/docs/services/ObjectStorage/os_deletion.html#schedule-object-deletion)讓物件到期。
{: shortdesc}

**附註**：如果您刪除容器，則會刪除該容器內所儲存的任何物件。


## 透過 UI 刪除物件及容器 {: #deleting-ui}

1. 在服務實例儀表板中，選取具有您不再需要之檔案的容器。
2. 從**動作**下拉功能表中，選取**刪除檔案**。
3. 如果您不再需要使用容器，請從**動作**下拉功能表選取**刪除容器**。



## 透過 CLI 刪除物件及容器 {: #deleting-cli}

1.  如果您未登入 {{site.data.keyword.Bluemix_notm}}，請登入包含 {{site.data.keyword.objectstorageshort}} 實例的組織和空間。
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. 選用項目：確認您已備份物件，然後才刪除檔案及容器。

3. 執行下列指令，以刪除檔案：
  ```
  swift delete <container_name> <file_name>
  ```
  {: pre}

4. 若要刪除容器，請執行下列指令：
  ```
  swift delete <container_name>
  ```
  {: pre}



## 排定物件刪除 {: #schedule-object-deletion}


您可以使用 `X-Delete-At` 或 `X-Delete-After` 標頭，排定物件的刪除時間。
{: shortdesc}

`X-Delete-At` 標頭會接受一個代表新紀元時間的整數，將會在該時間刪除物件。`X-Delete_After` 標頭會接受一個代表秒數的整數，在該秒數之後會刪除物件。

**附註：**物件實際刪除可能不會按照指出的確切時間發生。不過，物件會在指定的時間到期。屆時，再也無法聯繫該物件。實際的刪除將在 Swift 叢集中配置的 swift-object-expirer 常駐程式下次執行時發生。

#### 使用 Swift 指令：

* 若要設定在特定日期和時間刪除物件，請執行下列指令：

    ```
    swift post -H "X-Delete-At:<epoch_time>" <container_name> <object_name>
    ```
    {: pre}

    範例：
    若要設定在 "2016/04/01 08:00:00" 刪除物件，請執行下列指令：

    ```
    swift post -H "X-Delete-At:1459515600" container1 file7
    ```
    {: screen}

* 若要設定在特定時間量之後刪除物件，請使用下列指令：

    ```
    swift post -H "X-Delete-After:<number_of_seconds>" <container_name> <object_name>
    ```
    {: pre}

    範例：
    若要設定將在現在起的一小時後刪除物件，請執行下列指令：

    ```
    swift post -H "X-Delete-After:3600" container1 file7
    ```
    {: screen}

* 若要移除物件的有效期限，請使用下列指令：

    ```
    swift post -H "X-Remove-Delete-After:<number_of_seconds>" <container_name> <object_name>
    ```
    {: pre}



#### 使用 cURL 指令：

* 若要設定將在 "2016/04/01 08:00:00" 刪除物件，請使用下列指令：

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

* 若要設定將在現在起的一小時後刪除物件，請使用下列指令：

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:<number_of_seconds>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

* 若要檢查物件是否有標頭，請使用下列指令：

    ```
    cURL -I -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

* 若要移除有效期限，請使用下列指令：

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}
