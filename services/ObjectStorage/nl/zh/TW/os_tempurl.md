---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 建立暫時 URL {: #create-temporary-url}

暫時 URL 是一個很長、難以猜測的 URL，可用來在指定的時段下載物件，而無需進一步鑑別。
{: shortdesc}


1. 使用下列指令，透過列印帳戶資訊來識別您的鑑別資訊：

  ```
  swift stat
  ```
  {: pre}
  **附註**：請記下 *Account* 後的完整字串，包括 `AUTH_`。

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
      <td> <i> method </i> </td>
      <td> GET 可容許下載。PUT 可容許上傳。</td>
    </tr>
    <tr>
      <td> <i> seconds </i> </td>
      <td> 暫時 URL 可供使用的時間（以秒為單位表示）。</td>
    </tr>
    <tr>
      <td> <i> path </i> </td>
      <td> 物件的完整路徑（以 <code>/v1/<i>auth_account</i>/<i>container_name</i>/<i>object_name</i></code> 表示）。</td>
    </tr>
    <tr>
      <td> <i> key </i> </td>
      <td> 您在步驟 2 中設定的秘密金鑰。</td>
    </tr>
  </table>

  表 1：暫時 URL 位置引數

5. 選用：將傳回的 URL 附加至叢集名稱，以取得完整 URL。然後，您可以搭配使用完整 URL 與任何相容的 HTTP 用戶端（例如 cURL、wget 或 Firefox）來下載物件。
