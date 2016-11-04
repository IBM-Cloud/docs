---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用物件版本化 {: #work-with-object-versioning}

*前次更新：2016 年 10 月 19 日*
{: .last-updated}

使用物件版本化，您可以保留物件的不同版本，而不需要重新命名檔案。這可讓您查看每一個物件的歷程，並追蹤進行變更的時間。
{: shortdesc}


### 設定物件版本化 {: #setting-up-versioning}

您可以使用 `X-Versions-Location` 參數來設定容器中每一個物件的版本。如果要這麼做，請另外建立一個容器，以存放舊版本的物件，如下所示。

您可以透過 Swift 用戶端或使用 cURL 指令來設定物件版本化。
* 如果您使用 Swift 用戶端，請執行下列指令：

    ```
    swift post <container_name> -H "X-Versions-Location:<backup_container_name>"
    ```
    {: pre}
    
* 如果您使用 cURL，則可以如下進行設定：

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<backup_container_name>" https://<object-storage_url>/<container_name>
    ```
    {: pre}
    
**附註**：備份容器中的物件將自動使用下列格式命名：`<Length><Object_name>/<Timestamp>`。
<table>
  <tr>
    <th> 屬性</th>
    <th> 說明</th>
  </tr>
  <tr>
    <td> `Length` </td>
    <td> 物件名稱的長度。這是 3 個字元並填補零的十六進位數。</td>
  </tr>
  <tr>
    <td> `Object_name` </td>
    <td> 物件的名稱。</td>
  </tr>
  <tr>
    <td> `Timestamp` </td>
    <td> 物件的這個版本最初上傳時的時間戳記。</td>
  </tr>
</table>

### 停用物件版本化 {: #disabling-versioning}

您可以透過 Swift 用戶端或使用 cURL 指令來停用版本化。

* 若要使用 Swift 用戶端，請執行下列指令：

    ```
    swift post <container_name> -H "X-Remove-Versions-Location:"
    ```
    {: pre}
    
* 執行下列 cURL 指令，以停用版本化：

    ```
    cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/<container_name>
    ```
    {: pre}


### 物件版本化指導教學 {: #versioning-tutorial}
<!--- SHAWNA: This needs more background information. What are they doing? Why are they doing it? What is the outcome? --->

您可以使用下列指導教學來瞭解物件版本化的完整生命週期。

1. 建立名為 `container_one` 的容器。

    ```
    swift post container_one
    ```
    {: pre}
    
3. 使用名稱 `container_two` 來建立第二個容器。

    ```
    swift post container_two
    ```
    {: pre}
    
2. 設定版本化。

    ```
    swift post container_one -H "X-Versions-Location:container_two"
    ```
    {: pre}
    
4. 第一次將物件上傳至主要容器。

    ```
    swift upload container_one object
    ```
    {: pre}
    
7. 將物件的新版本上傳至 container_one。當您上傳檔案的新版本時，舊版本會自動移至您在設定版本化時指定的備份容器。

    ```
    swift upload container_one object
    ```
    {: pre}
    
8. 若要查看容器中檔案的新版本，請列出 container_one 中的物件。

    ```
    swift list container_one
    ```
    {: pre}
    
9. 列出 container_two 中的物件。您將會看到檔案的舊版本將儲存至此容器中。

    ```
    swift list container_two
    ```
    {: pre}
    
10. 刪除 container_one 中的物件。當您刪除物件時，備份容器中的舊版本將會自動移至主要容器。

    ```
    swift delete container_one object
    ```
    {: pre}
    
11. 列出這兩個容器。您將會在 `container_one` 中看到原始檔案，而 `container_two` 將會是空的。

    ```
    swift list container_one
    swift list container_two
    ```
    {: pre}
