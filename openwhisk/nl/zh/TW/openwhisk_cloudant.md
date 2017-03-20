---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用 Cloudant 套件
{: #openwhisk_catalog_cloudant}
`/whisk.system/cloudant` 套件可讓您使用 Cloudant 資料庫。它包括下列動作及資訊來源。

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | 套件 | dbname、host、username、password | 使用 Cloudant 資料庫 |
| `/whisk.system/cloudant/read` | 動作 (action) | dbname、id | 讀取資料庫中的文件 |
| `/whisk.system/cloudant/write` | 動作 (action) | dbname、overwrite、doc | 將文件寫入資料庫 |
| `/whisk.system/cloudant/changes` | 資訊來源 | dbname、maxTriggers | 在資料庫變更時發動觸發程式事件 |

下列各主題逐步說明如何設定 Cloudant 資料庫、配置關聯的套件，以及使用 `/whisk.system/cloudant` 套件中的動作及資訊來源。

## 在 Bluemix 中設定 Cloudant 資料庫
{: #openwhisk_catalog_cloudant_in}

如果您是從 Bluemix 使用 OpenWhisk，OpenWhisk 會自動建立 Bluemix Cloudant 服務實例的套件連結。如果您不是從 Bluemix 使用 OpenWhisk 及 Cloudant，請跳到下一步。

1. 在 Bluemix [儀表板](http://console.ng.Bluemix.net)中，建立 Cloudant 服務實例。

  請務必記住服務實例的名稱，以及您所在的 Bluemix 組織及空間。

2. 確定 OpenWhisk CLI 位於對應至前一個步驟中所使用之 Bluemix 組織及空間的名稱空間中。

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  或者，您也可以使用 `wsk property set --namespace`，從可存取的名稱空間清單中設定名稱空間。

3. 重新整理名稱空間中的套件。重新整理會自動建立您所建立之 Cloudant 服務實例的套件連結。

  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_testCloudant_Credentials-1
  ```

  ```
wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_testCloudant_Credentials-1 private binding
  ```

  您可以看到對應至 Bluemix Cloudant 服務實例的完整套件連結名稱。

4. 確認先前建立的套件連結是使用 Cloudant Bluemix 服務實例主機及認證所配置。

  ```
  wsk package get /myBluemixOrg_myBluemixSpace/Bluemix_testCloudant_Credentials-1 parameters
  ```
  {: pre}
  ```
  ok: got package /myBluemixOrg_myBluemixSpace/Bluemix_testCloudant_Credentials-1, displaying field parameters
  ```
  ```json
  [
      {
          "key": "username",
          "value": "cdb18832-2bbb-4df2-b7b1-Bluemix"
      },
      {
          "key": "host",
          "value": "cdb18832-2bbb-4df2-b7b1-Bluemix.cloudant.com"
      },
      {
          "key": "password",
          "value": "c9088667484a9ac827daf8884972737"
      }
      ]
  ```

## 在 Bluemix 外部設定 Cloudant 資料庫
{: #openwhisk_catalog_cloudant_outside}

如果您不是在 Bluemix 中使用 OpenWhisk，或者要在 Bluemix 外部設定 Cloudant 資料庫，則必須手動建立 Cloudant 帳戶的套件連結。您需要 Cloudant 帳戶主機名稱、使用者名稱及密碼。

1. 建立針對 Cloudant 帳戶所配置的套件連結。

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username MYUSERNAME -p password MYPASSWORD -p host MYCLOUDANTACCOUNT.cloudant.com
  ```
  {: pre}

2. 驗證套件連結已存在。

  ```
wsk package list
  ```
  {: pre}
  ```
packages
  /myNamespace/myCloudant private binding
  ```


## 接聽 Cloudant 資料庫的變更
{: #openwhisk_catalog_cloudant_listen}

您可以使用 `changes` 資訊來源，配置服務在每次變更 Cloudant 資料庫時發動觸發程式。參數如下所示：

- `dbname`：Cloudant 資料庫的名稱。
- `maxTriggers`：在達到此限制時停止發動觸發程式。預設值為無限。


1. 使用您先前建立的套件連結中的 `changes` 資訊來源，來建立觸發程式。請務必將 `/myNamespace/myCloudant` 取代為套件名稱。

  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
  ```
  {: pre}
  ```
  ok: created trigger feed myCloudantTrigger
  ```

2. 輪詢啟動。

  ```
  wsk activation poll
  ```
  {: pre}

3. 在 Cloudant 儀表板中，修改現有文件，或建立新文件。

4. 觀察每一個文件變更的 `myCloudantTrigger` 觸發程式的新啟動。
  
  **附註**：如果您無法觀察到新啟動，請參閱有關在 Cloudant 資料庫中讀取及寫入的後續各節。測試下列讀取及寫入步驟，有助於驗證 Cloudant 認證正確無誤。
  
  您現在可以建立規則，並將它們關聯至可反應文件更新的動作。
  
  所產生事件的內容具有下列參數：
  
  - `id`：文件 ID。
  - `seq`：Cloudant 所產生的序列 ID。
  - `changes`：物件陣列，各物件有包含文件修訂 ID 的 `rev` 欄位。
  
  觸發程式事件的 JSON 表示法如下所示：
  
  ```json
  {
      "id": "6ca436c44074c4c2aa6a40c9a188b348",
      "seq": "2-g1AAAAL9aJyV-GJCaEuqx4-BktQkYp_dmIfC",
      "changes": [
          {
              "rev": "2-da3f80848a480379486fb4a2ad98fa16"
          }
      ]
  }
  ```
  
## 寫入 Cloudant 資料庫
{: #openwhisk_catalog_cloudant_write}

您可以使用動作，將文件儲存至稱為 `testdb` 的 Cloudant 資料庫。請確定此資料庫存在於 Cloudant 帳戶中。

1. 使用您先前建立的套件連結中的 `write` 動作，來儲存文件。請務必將 `/myNamespace/myCloudant` 取代為套件名稱。

  ```
  wsk action invoke /myNamespace/myCloudant/write --blocking --result --param dbname testdb --param doc "{\"_id\":\"heisenberg\",\"name\":\"Walter White\"}"
  ```
  {: pre}
  ```
  ok: invoked /myNamespace/myCloudant/write with id 62bf696b38464fd1bcaff216a68b8287
  ```
  ```json
  {
    "id": "heisenberg",
    "ok": true,
    "rev": "1-9a94fb93abc88d8863781a248f63c8c3"
  }
  ```

2. 在 Cloudant 儀表板中瀏覽到文件，以驗證文件已存在。

  `testdb` 資料庫的儀表板 URL 可能與下面類似：`https://MYCLOUDANTACCOUNT.cloudant.com/dashboard.html#database/testdb/_all_docs?limit=100`。


## 讀取 Cloudant 資料庫
{: #openwhisk_catalog_cloudant_read}

您可以使用動作，從稱為 `testdb` 的 Cloudant 資料庫中提取文件。請確定此資料庫存在於 Cloudant 帳戶中。

- 使用您先前建立的套件連結中的 `read` 動作，來提取文件。請務必將 `/myNamespace/myCloudant` 取代為套件名稱。

  ```
  wsk action invoke /myNamespace/myCloudant/read --blocking --result --param dbname testdb --param id heisenberg
  ```
  {: pre}
  ```json
  {
    "_id": "heisenberg",
    "_rev": "1-9a94fb93abc88d8863781a248f63c8c3",
    "name": "Walter White"
  }
  ```

## 使用動作序列及變更觸發程式來處理 Cloudant 資料庫中的文件
{: #openwhisk_catalog_cloudant_read_change notoc}
您可以在規則中使用動作序列，來提取及處理與 Cloudant 變更事件相關聯的文件。

以下是可處理文件的動作的範例程式碼：
```javascript
function main(doc){
  return { "isWalter:" : doc.name === "Walter White"};
}
```

建立動作來處理 Cloudant 中的文件：
```
wsk action create myAction myAction.js
```
{: pre}

若要從資料庫中讀取文件，您可以使用 Cloudant 套件中的 `read` 動作。
可以使用 `myAction` 來組合 `read` 動作，以建立動作序列。
```
wsk action create sequenceAction --sequence /myNamespace/myCloudant/read,myAction
```
{: pre}

動作 `sequenceAction` 可以用於規則中，在新的 Cloudant 觸發程式事件上啟動動作。
```
wsk rule create myRule myCloudantTrigger sequenceAction
```
{: pre}

**附註**：Cloudant `changes` 觸發程式用來支援不再受支援的參數 `includeDoc`。
  您需要重建先前使用 `includeDoc` 所建立的觸發程式。請遵循下列步驟來重建觸發程式：
  ```
  wsk trigger delete myCloudantTrigger
  ```
  {: pre}
  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
  ```
  {: pre}

  上述範例可以用來建立動作序列，以讀取已變更的文件以及呼叫您的現有動作。
  請記得停用所有可能不再有效的規則，並且使用動作序列型樣來建立新規則。

