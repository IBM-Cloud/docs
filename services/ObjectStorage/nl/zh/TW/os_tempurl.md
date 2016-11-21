---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 建立暫時 URL {: #create-temporary-url}

*前次更新：2016 年 10 月 19 日*
{: .last-updated}

暫時 URL 是一個很長、難以猜測的 URL，可用來在指定的時段下載物件，而無需進一步鑑別。
{: shortdesc}


1. 使用下列指令，透過列印帳戶資訊來識別您的鑑別資訊：

    ```
    swift stat
    ```
    {: pre}
    
    **附註**：找到「帳戶」欄位，並記下*帳戶*：之後的完整字串，包括 `AUTH_`。
2. 設定秘密金鑰。此金鑰可以是您選取的任何項目，但最佳做法是選取一個很長、隨機且難以猜測的字串。若要設定金鑰，請執行下列指令：

    ```
    swift post -m "Temp-URL-Key:<key>"
    ```
    {: pre}
    
3. 執行下列指令，驗證已順利設定 `Temp-URL-Key`。

    ```
    swift stat
    ```
    {: pre}
    
4. 執行下列指令，以建立暫時 URL：

    ```
    swift tempurl GET <seconds> <path> <key>
    ```
    {: pre}
    
    下表說明 Swift `tempurl` 指令所採用的位置引數。
    <table>
      <tr>
        <th> 引數</th>
        <th> 說明</th>
      </tr>
      <tr>
        <td> [method] </td>
        <td> GET 可容許下載。PUT 可容許上傳。</td>
      </tr>
      <tr>
        <td> [seconds] </td>
        <td> 暫時 URL 可供使用的時間（以秒為單位）。</td>
      </tr>
      <tr>
        <td> [path] </td>
        <td> 物件的完整路徑（以 `/v1/<auth_account>/<container_name>/<object_name>` 表示）。如需相關資訊，請參閱 [{{site.data.keyword.objectstorageshort}} URL 文件](/os_api.html#access-points)。</td>
      </tr>
      <tr>
        <td> [key] </td>
        <td> 您在步驟 2 中設定的秘密金鑰。</td>
      </tr>
    </table>
    *表 2：tempurl 位置引數*
5. （*選用*）：將傳回的 URL 附加至叢集名稱，以取得完整 URL。然後，您可以搭配使用完整 URL 與任何相容的 HTTP 用戶端（例如 cURL、wget 或 Firefox）來下載物件。
