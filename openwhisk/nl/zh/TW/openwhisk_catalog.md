---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 使用已啟用 {{site.data.keyword.openwhisk_short}} 功能的服務 
{: #openwhisk_ecosystem}
*前次更新：2016 年 3 月 28 日*

在 {{site.data.keyword.openwhisk}} 中，套件的型錄可讓您輕鬆地使用有用的功能來加強應用程式，以及在生態系統中存取外部服務。已啟用 {{site.data.keyword.openwhisk_short}} 功能的外部服務範例包括 Cloudant、The Weather Company、Slack 及 GitHub。
{: shortdesc}

在 `/whisk.system` 名稱空間中，型錄可當作套件使用。如需如何使用指令行工具來瀏覽型錄的相關資訊，請參閱[瀏覽套件](./openwhisk_packages.html#openwhisk_packagedisplay)。

下列各主題記載型錄中的一些套件。

## 使用 Cloudant 套件
{: #openwhisk_catalog_cloudant}
`/whisk.system/cloudant` 套件可讓您使用 Cloudant 資料庫。它包括下列動作及資訊來源。

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | 套件 | {{site.data.keyword.Bluemix_notm}}ServiceName、host、username、password、dbname、includeDoc、overwrite | 使用 Cloudant 資料庫 |
| `/whisk.system/cloudant/read` | 動作 | dbname、includeDoc、id | 讀取資料庫中的文件 |
| `/whisk.system/cloudant/write` | 動作 | dbname、overwrite、doc | 將文件寫入資料庫 |
| `/whisk.system/cloudant/changes` | 資訊來源 | dbname、includeDoc | 在資料庫變更時發動觸發程式事件 |

下列各主題逐步說明如何設定 Cloudant 資料庫、配置關聯的套件，以及使用 `/whisk.system/cloudant` 套件中的動作及資訊來源。

### 在 {{site.data.keyword.Bluemix_notm}} 中設定 Cloudant 資料庫

如果您是從 {{site.data.keyword.Bluemix}} 使用 {{site.data.keyword.openwhisk_short}}，則 {{site.data.keyword.openwhisk_short}} 會自動建立 {{site.data.keyword.Bluemix_notm}} Cloudant 服務實例的套件連結。如果您不是從 {{site.data.keyword.Bluemix_notm}} 使用 {{site.data.keyword.openwhisk_short}} 及 Cloudant，請跳到下一步。

1. 在 {{site.data.keyword.Bluemix_notm}} [儀表板](http://console.ng.{{site.data.keyword.Bluemix_notm}}.net)中，建立 Cloudant 服務實例。

  請務必記住服務實例名稱，以及您所在的 {{site.data.keyword.Bluemix_notm}} 組織及空間。

2. 確定 {{site.data.keyword.openwhisk_short}} CLI 位於對應至前一個步驟中所使用之 {{site.data.keyword.Bluemix_notm}} 組織及空間的名稱空間中。

  ```
  wsk property set --namespace my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space
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
  {{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1 private binding
  ```
  {: screen}

  您應該會看到對應至 {{site.data.keyword.Bluemix_notm}} Cloudant 服務實例的套件連結的完整名稱。

4. 確認先前建立的套件連結是使用 Cloudant {{site.data.keyword.Bluemix_notm}} 服務實例主機及認證所配置。

  ```
  wsk package get /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1
  ```
  {: pre}
  ```
  ok: got package /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1, projecting parameters
  [
      ...
      {
          "key": "username",
          "value": "cdb18832-2bbb-4df2-b7b1-{{site.data.keyword.Bluemix_notm}}"
      },
      {
          "key": "host",
          "value": "cdb18832-2bbb-4df2-b7b1-{{site.data.keyword.Bluemix_notm}}.cloudant.com"
      },
      {
          "key": "password",
          "value": "c9088667484a9ac827daf8884972737"
      }
      ...
  ]
  ```
  {: screen}

### 在 {{site.data.keyword.Bluemix_notm}} 外部設定 Cloudant 資料庫

如果您不是在 {{site.data.keyword.Bluemix_notm}} 中使用 {{site.data.keyword.openwhisk_short}}，或者要在 {{site.data.keyword.Bluemix_notm}} 外部設定 Cloudant 資料庫，則必須手動建立 Cloudant 帳戶的套件連結。您需要 Cloudant 帳戶主機名稱、使用者名稱及密碼。

1. 建立針對 Cloudant 帳戶所配置的套件連結。

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username 'MYUSERNAME' -p password 'MYPASSWORD' -p host 'MYCLOUDANTACCOUNT.cloudant.com'
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
  {: screen}


### 接聽 Cloudant 資料庫的變更

您可以使用 `changes` 資訊來源，配置服務在每次變更 Cloudant 資料庫時發動觸發程式。

1. 使用您先前建立的套件連結中的 `changes` 資訊來源，來建立觸發程式。請務必將 `/myNamespace/myCloudant` 取代為套件名稱。

  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb --param includeDocs true
  ```
  {: pre}
  ```
  ok: created trigger feed myCloudantTrigger
  ```
  {: screen}

2. 輪詢啟動。

  ```
  wsk activation poll
  ```
  {: pre}

3. 在 Cloudant 儀表板中，修改現有文件，或建立新文件。

4. 觀察每一個文件變更的 `myCloudantTrigger` 觸發程式的新啟動。

**附註**：如果您無法觀察到新啟動，請參閱有關在 Cloudant 資料庫中讀取及寫入的後續各節。測試下面的讀取及寫入步驟，有助於驗證 Cloudant 認證正確無誤。

您現在可以建立規則，並將它們關聯至可反應文件更新的動作。

所產生事件的內容取決於建立觸發程式時的 `includeDocs` 參數值。如果設為 true，發動的每一個觸發程式事件都會包括已修改的 Cloudant 文件。例如，請考量下列已修改的文件：

  ```
  {
    "_id": "6ca436c44074c4c2aa6a40c9a188b348",
    "_rev": "3-bc4960fc13aa368afca8c8427a1c18a8",
    "name": "Heisenberg"
  }
  ```
  {: screen}

此範例中的程式碼會使用對應的 `_id`、`_rev` 及 `name` 參數來產生觸發程式事件。事實上，觸發程式事件的 JSON 表示法與文件相同。

否則，如果 `includeDocs` 是 false，則事件包括下列參數：

- `id`：文件 ID。
- `seq`：Cloudant 所產生的序列 ID。
- `changes`：物件陣列，各物件有包含文件修訂 ID 的 `rev` 欄位。

觸發程式事件的 JSON 表示法如下所示：

  ```
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


### 寫入 Cloudant 資料庫

您可以使用動作，將文件儲存至稱為 `testdb` 的 Cloudant 資料庫。請確定此資料庫存在於 Cloudant 帳戶中。

1. 使用您先前建立的套件連結中的 `write` 動作，來儲存文件。請務必將 `/myNamespace/myCloudant` 取代為套件名稱。

  ```
  wsk action invoke /myNamespace/myCoudant/write --blocking --result --param dbname testdb --param doc '{"_id":"heisenberg", "name":"Walter White"}'
  ```
  {: pre}
  ```
  ok: invoked /myNamespace/myCoudant/write with id 62bf696b38464fd1bcaff216a68b8287
  response:
  {
    "id": "heisenberg",
    "ok": true,
    "rev": "1-9a94fb93abc88d8863781a248f63c8c3"
  }
  ```
  {: screen}

2. 在 Cloudant 儀表板中瀏覽到文件，以驗證文件已存在。

  `testdb` 資料庫的儀表板 URL 可能與下面類似：`https://MYCLOUDANTACCOUNT.cloudant.com/dashboard.html#database/testdb/_all_docs?limit=100`。


### 讀取 Cloudant 資料庫

您可以使用動作，從稱為 `testdb` 的 Cloudant 資料庫中提取文件。請確定此資料庫存在於 Cloudant 帳戶中。

1. 使用您先前建立的套件連結中的 `read` 動作，來提取文件。請務必將 `/myNamespace/myCloudant` 取代為套件名稱。

  ```
  wsk action invoke /myNamespace/myCoudant/read --blocking --result --param dbname testdb --param id heisenberg
  ```
  {: pre}
  ```
  {
    "_id": "heisenberg",
    "_rev": "1-9a94fb93abc88d8863781a248f63c8c3"
    "name": "Walter White"
  }
  ```
  {: screen}


## 使用警示套件
{: #openwhisk_catalog_alarm}

`/whisk.system/alarms` 套件可以用來依指定的頻率發動觸發程式。這適用於設定循環工作或作業（例如，每個小時呼叫系統備份動作）。

該套件包括下列資訊來源。

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | 套件 | - | 警示及定期公用程式 |
| `/whisk.system/alarms/alarm` | 資訊來源 | cron、trigger_payload、maxTriggers | 定期發動觸發程式事件 |


### 定期發動觸發程式事件

`/whisk.system/alarms/alarm` 資訊來源會配置「警示」服務依指定的頻率發動觸發程式事件。參數如下所示：

- `cron`：指出何時發動觸發程式的字串（根據 Unix crontab 語法）（世界標準時間 (UTC)）。字串是六個連串的欄位，以空格區隔：`X X X X X X `。如需使用 cron 語法的詳細資料，請參閱：https://github.com/ncb000gt/node-cron。

- `trigger_payload`：每次發動觸發程式時，此參數的值都會變成觸發程式的內容。

- `maxTriggers`：在達到此限制時停止發動觸發程式。預設值為 1000。

以下範例使用觸發程式事件中的 `name` 及 `place` 值來建立每 20 秒發動一次的觸發程式。

  ```
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron '/20 * * * * *' --param trigger_payload '{"name":"Odin","place":"Asgard"}'
  ```
  {: pre}

每一個產生的事件都會併入為參數，即 `trigger_payload` 值所指定的內容。在此情況下，每一個觸發程式事件都會有參數 `name=Odin` 及 `place=Asgard`。


## 使用 Weather 套件
{: #openwhisk_catalog_weather}

`/whisk.system/weather` 套件提供一種簡便的方式來呼叫 The Weather Company API。

該套件包括下列動作。

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/weather` | 套件 | apiKey | The Weather Company 的服務 |
| `/whisk.system/weather/forecast` | 動作 | apiKey、latitude、longitude | Weather.com 10 天預報 |

儘管不是必要的，但是建議您使用 `apiKey` 值建立套件連結。如此，您就不需要每次在呼叫套件中的動作時都指定金鑰。

### 取得某個位置的天氣預報

`/whisk.system/weather/forecast` 動作會從 The Weather Company 呼叫 API，以傳回某個位置的 10 天天氣預報。參數如下所示：

- `apiKey`：獲授權呼叫 10 天預報 API 的 The Weather Company 的 API 金鑰。
- `latitude`：位置的緯度座標。
- `longitude`：位置的經度座標。

以下範例說明如何建立套件連結，然後取得 10 天預報。

1. 使用 API 金鑰建立套件連結。

  ```
  wsk package bind /whisk.system/weather myWeather --param apiKey 'MY_WEATHER_API'
  ```
  {: pre}

2. 在套件連結中呼叫 `forecast` 動作，以取得天氣預報。

  ```
  wsk action invoke myWeather/forecast --blocking --result --param latitude '43.7' --param longitude '-79.4'
  ```
  {: pre}

  ```
  {
      "forecasts": [
          {
              "dow": "Wednesday",
              "max_temp": -1,
              "min_temp": -16,
              "narrative": "Chance of a few snow showers. Highs -2 to 0C and lows -17 to -15C.",
              ...
          },
          {
              "class": "fod_long_range_daily",
              "dow": "Thursday",
              "max_temp": -4,
              "min_temp": -8,
              "narrative": "Mostly sunny. Highs -5 to -3C and lows -9 to -7C.",
              ...
          },
          ...
      ],
  }
  ```
  {: screen}


## 使用 Watson 套件
{: #openwhisk_catalog_watson}

`/whisk.system/watson` 套件提供一種簡便的方來呼叫各種 Watson API。

該套件包括下列動作。

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/watson` | 套件 | username、password | Watson 分析 API 的動作 |
| `/whisk.system/watson/translate` | 動作 | translateFrom、translateTo、translateParam、username、password | 翻譯文字 |
| `/whisk.system/watson/languageId` | 動作 | payload、username、password | 識別語言 |

儘管不是必要的，但是建議您使用 `username` 及 `password` 值建立套件連結。如此，您就不需要每次在呼叫套件中的動作時都指定這些認證。

### 翻譯文字

`/whisk.system/watson/translate` 動作會將文字從某種語言翻譯成另一種語言。參數如下所示：

- `username`：Watson API 使用者名稱。
- `password`：Watson API 密碼。
- `translateParam`：要翻譯的輸入參數。例如，如果 `translateParam=payload`，則會翻譯傳遞給動作的 `payload` 參數值。
- `translateFrom`：兩位數的來源語言代碼。
- `translateTo`：兩位數的目標語言代碼。

下列範例說明如何建立套件連結以及翻譯一些文字。

1. 使用 Watson 認證建立套件連結。

  ```
  wsk package bind /whisk.system/watson myWatson --param username 'MY_WATSON_USERNAME' --param password 'MY_WATSON_PASSWORD'
  ```
  {: pre}

2. 在套件連結中呼叫 `translate` 動作，以將一些文字從英文翻譯成法文。

  ```
  wsk action invoke myWatson/translate --blocking --result --param payload 'Blue skies ahead' --param translateParam 'payload' --param translateFrom 'en' --param translateTo 'fr'
  ```
  {: pre}

  ```
  {
      "payload": "Ciel bleu a venir"
  }
  ```
  {: screen}


### 識別一些文字的語言

`/whisk.system/watson/languageId` 動作識別一些文字的語言。參數如下所示：

- `username`：Watson API 使用者名稱。
- `password`：Watson API 密碼。
- `payload`：要識別的文字。

以下範例說明如何建立套件連結以及識別一些文字的語言。

1. 使用 Watson 認證建立套件連結。

  ```
  wsk package bind /whisk.system/watson myWatson -p username 'MY_WATSON_USERNAME' -p password 'MY_WATSON_PASSWORD'
  ```
  {: pre}

2. 在套件連結中呼叫 `languageId` 動作，以識別語言。

  ```
  wsk action invoke myWatson/languageId --blocking --result --param payload 'Ciel bleu a venir'
  ```
  {: pre}
  ```
  {
    "payload": "Ciel bleu a venir",
    "language": "fr",
    "confidence": 0.710906
  }
  ```
  {: screen}


## 使用 Slack 套件
{: #openwhisk_catalog_slack}

`/whisk.system/slack` 套件提供一種簡便的方式來使用 [Slack API](https://api.slack.com/)。

該套件包括下列動作：

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/slack` | 套件 | url、channel、username | 與 Slack API 互動 |
| `/whisk.system/slack/post` | 動作 | text、url、channel、username | 將訊息張貼至 Slack 通道 |

儘管不是必要的，但是建議您使用 `username`、`url` 及 'channel' 值建立套件連結。使用連結，您就不需要每次在呼叫套件中的動作時都指定值。

### 將訊息張貼至 Slack 通道

`/whisk.system/slack/post` 動作會將訊息張貼至指定的 Slack 通道。參數如下所示：

- `url`：Slack Webhook URL。
- `channel`：要將訊息張貼至其中的 Slack 通道。
- `username`：用來張貼訊息的名稱。
- `text`：要張貼的訊息。

下列範例說明如何配置 Slack、建立套件連結，以及將訊息張貼至通道。

1. 針對您的團隊配置 Slack [送入的 Webhook](https://api.slack.com/incoming-webhooks)。

  配置 Slack 之後，您應該取得與下列類似的 Webhook URL：`https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`。在下一步中，您需要此項目。

2. 使用 Slack 認證、要張貼至其中的通道，以及用來進行張貼的使用者名稱，來建立套件連結。

  ```
  wsk package bind /whisk.system/slack mySlack --param url 'https://hooks.slack.com/services/...' --param username 'Bob' --param channel '#MySlackChannel'
  ```
  {: pre}

3. 在套件連結中呼叫 `post` 動作，以將訊息張貼至 Slack 通道。

  ```
  wsk action invoke mySlack/post --blocking --result --param text 'Hello from OpenWhisk!'
  ```
  {: pre}


## 使用 GitHub 套件
{: #openwhisk_catalog_github}

`/whisk.system/github` 套件提供一種簡便的方來使用 [GitHub API](https://developer.github.com/)。

該套件包括下列資訊來源：

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/github` | 套件 | username、repository、accessToken | 與 GitHub API 互動 |
| `/whisk.system/github/webhook` | 資訊來源 | events、username、repository、accessToken | 在 GitHub 活動時發動觸發程式事件 |

儘管不是必要的，但是建議您使用 `username`、`repository` 及 `accessToken` 值建立套件連結。使用連結，您就不需要每次使用套件中的資訊來源時都指定值。

### 發動 GitHub 活動的觸發程式事件

`/whisk.system/github/webhook` 資訊來源會配置服務在指定 GitHub 儲存庫中有活動時發動觸發程式。參數如下所示：

- `username`：GitHub 儲存庫的使用者名稱。
- `repository`：GitHub 儲存庫。
- `accessToken`：GitHub 個人存取記號。[建立記號](https://github.com/settings/tokens)時，請務必選取 repo:status 及 public_repo 範圍。同時，請確定您尚未定義儲存庫的任何 Webhook。
- `events`：感興趣的 [GitHub 活動類型](https://developer.github.com/v3/activity/events/types/)。

下列範例說明如何建立在每次 GitHub 儲存庫有新確定時將發動的觸發程式。

1. 產生 GitHub [個人存取記號](https://github.com/settings/tokens)。

  下一步將會使用存取記號。


2. 使用存取記號，建立針對 GitHub 儲存庫所配置的套件連結。

  ```
  wsk package bind /whisk.system/github myGit --param username myGitUser --param repository myGitRepo --param accessToken aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}

3. 使用 `myGit/webhook` 資訊來源，以建立 GitHub `push` 事件類型的觸發程式。

  ```
  wsk trigger create myGitTrigger --feed myGit/webhook --param events push
  ```
  {: pre}

