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


# 設定物件版本化 {: #setting-up-versioning}

您可以設定物件版本化，來自動保留舊版物件。使用版本化，您可以查看每一個物件的歷程。
{: shortdesc}

當您將檔案的新版本上傳至主要容器時，舊版本會自動移至備份容器。如果您從主要容器刪除檔案，最新的版本會自動從備份容器移到主要容器，以取代已刪除的檔案。

1. 建立容器，並為它命名。將變數 *container_name* 取代為您要提供給容器的名稱。

    ```
    swift post <container_name>
    ```
    {: pre}

2. 建立第二個容器以充當您的備份儲存空間，並加以命名。

    ```
    swift post <backup_container_name>
    ```
    {: pre}

3. 設定版本化。

    Swift 指令：

    ```
    swift post <container_name> -H "X-Versions-Location:<backup_container_name>"
    ```
    {: pre}

    cURL 指令：

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<backup_container_name>" https://<object-storage_url>/<container_name>
    ```
    {: pre}

4. 第一次將物件上傳至主要容器。

    ```
    swift upload <container_name> <object>
    ```
    {: pre}

5. 變更您的物件。

6. 將物件的新版本上傳至您的主要容器。

    ```
    swift upload <container_name> <object>
    ```
    {: pre}

7.  備份容器中的物件將自動使用下列格式命名：`<Length><Object_name>/<Timestamp>`。
  <table>
  <caption> 表 1. 說明的命名屬性</caption>
    <tr>
      <th> 屬性</th>
      <th> 說明</th>
    </tr>
    <tr>
      <td> <i>Length</i> </td>
      <td> 物件名稱的長度。這是 3 個字元並填補零的十六進位數。</td>
    </tr>
    <tr>
      <td> <i>Object_name</i> </td>
      <td> 物件的名稱。</td>
    </tr>
    <tr>
      <td> <i>Timestamp</i> </td>
      <td> 物件的這個版本最初上傳時的時間戳記。</td>
    </tr>
  </table>


6. 列出主要容器中的物件，以查看新版本的檔案。

    ```
    swift list --lh <container_name>
    ```
    {: pre}

7. 列出備份容器中的物件。您會看到儲存在此容器中的舊版檔案。請注意，時間戳記會新增至您的檔案。

    ```
    swift list --lh <backup_container_name>
    ```
    {: pre}

8. 刪除主要容器中的物件。當您刪除物件時，備份容器中的最新版本會自動移回主要容器。

    ```
    swift delete <container_name> <object>
    ```
    {: pre}

9. 選用：停用物件版本化。

    Swift 指令：

    ```
    swift post <container_name> -H "X-Remove-Versions-Location:"
    ```
    {: pre}

    cURL 指令：

    ```
    cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/<container_name>
    ```
    {: pre}
