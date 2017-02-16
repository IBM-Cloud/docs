---

 

copyright:

  years: 2016, 2017
lastupdated: "2017-01-04"
 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 使用針對 {{site.data.keyword.openwhisk_short}} 啟用的 {{site.data.keyword.Bluemix_notm}} 服務
{: #openwhisk_ecosystem}

在 {{site.data.keyword.openwhisk}} 中，套件的型錄可讓您輕鬆地使用有用的功能來加強應用程式，以及在生態系統中存取外部服務。已啟用 {{site.data.keyword.openwhisk_short}} 功能的外部服務範例包括 Cloudant、The Weather Company、Slack 及 GitHub。
{: shortdesc}

在 `/whisk.system` 名稱空間中，型錄可當作套件使用。如需如何使用指令行工具來瀏覽型錄的相關資訊，請參閱[瀏覽套件](./openwhisk_packages.html#openwhisk_packagedisplay)。

下列各主題記載型錄中的一些套件。

## 使用 Cloudant 套件
{: #openwhisk_catalog_cloudant}
`/whisk.system/cloudant` 套件可讓您使用 Cloudant 資料庫。它包括下列動作及資訊來源。

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | 套件 | {{site.data.keyword.Bluemix_notm}}ServiceName、host、username、password、dbname、overwrite | 使用 Cloudant 資料庫 |
| `/whisk.system/cloudant/read` | 動作 | dbname、includeDoc、id | 讀取資料庫中的文件 |
| `/whisk.system/cloudant/write` | 動作 | dbname、overwrite、doc | 將文件寫入資料庫 |
| `/whisk.system/cloudant/changes` | 資訊來源 | dbname、maxTriggers | 在資料庫變更時發動觸發程式事件 |

下列各主題逐步說明如何設定 Cloudant 資料庫、配置關聯的套件，以及使用 `/whisk.system/cloudant` 套件中的動作及資訊來源。

### 在 {{site.data.keyword.Bluemix_notm}} 中設定 Cloudant 資料庫
{: #openwhisk_catalog_cloudant_in}

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

  您可以看到對應至 {{site.data.keyword.Bluemix_notm}} Cloudant 服務實例的完整套件連結名稱。

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
{: #openwhisk_catalog_cloudant_outside}

如果您不是在 {{site.data.keyword.Bluemix_notm}} 中使用 {{site.data.keyword.openwhisk_short}}，或者要在 {{site.data.keyword.Bluemix_notm}} 外部設定 Cloudant 資料庫，則必須手動建立 Cloudant 帳戶的套件連結。您需要 Cloudant 帳戶主機名稱、使用者名稱及密碼。

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
  {: screen}


### 接聽 Cloudant 資料庫的變更
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
  {: screen}

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
{: #openwhisk_catalog_cloudant_write}

您可以使用動作，將文件儲存至稱為 `testdb` 的 Cloudant 資料庫。請確定此資料庫存在於 Cloudant 帳戶中。

1. 使用您先前建立的套件連結中的 `write` 動作，來儲存文件。請務必將 `/myNamespace/myCloudant` 取代為套件名稱。

  ```
  wsk action invoke /myNamespace/myCloudant/write --blocking --result --param dbname testdb --param doc "{\"_id\":\"heisenberg\",\"name\":\"Walter White\"}"
  ```
  {: pre}
  ```
  ok: invoked /myNamespace/myCloudant/write with id 62bf696b38464fd1bcaff216a68b8287
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
{: #openwhisk_catalog_cloudant_read}

您可以使用動作，從稱為 `testdb` 的 Cloudant 資料庫中提取文件。請確定此資料庫存在於 Cloudant 帳戶中。

1. 使用您先前建立的套件連結中的 `read` 動作，來提取文件。請務必將 `/myNamespace/myCloudant` 取代為套件名稱。

  ```
  wsk action invoke /myNamespace/myCloudant/read --blocking --result --param dbname testdb --param id heisenberg
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

### 使用動作序列及變更觸發程式來處理 Cloudant 資料庫中的文件

您可以在規則中使用動作序列，來提取及處理與 Cloudant 變更事件相關聯的文件。

以下是可處理文件的動作的範例程式碼：
```
function main(doc){
  return { "isWalter:" : doc.name === "Walter White"};
}
```
{: codeblock}

建立動作來處理 Cloudant 中的文件：
```
wsk action create myAction myAction.js
```
{: pre}

若要從資料庫中讀取文件，您可以使用 Cloudant 套件中的 `read` 動作。
可以使用 `myAction` 來編寫 `read` 動作，以建立動作序列。
```
wsk action create sequenceAction --sequence /myNamespace/myCloudant/read,myAction
```
{: pre}

動作 `sequenceAction` 可以用於在新 Cloudant 觸發程式事件上啟動動作的規則。
```
wsk rule create myRule myCloudantTrigger sequenceAction
```
{: pre}

**附註** Cloudant `changes` 觸發程式用來支援不再受支援的參數 `includeDoc`。
  您需要重建先前使用 `includeDoc` 所建立的觸發程式。請遵循下列步驟來重建觸發程式：
  ```
  wsk trigger delete myCloudantTrigger
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
  ```
  {: pre}

  上述範例可以用來建立動作序列，以讀取已變更的文件以及呼叫您的現有動作。
  請記得停用所有可能不再有效的規則，並且使用動作序列型樣來建立新規則。

## 使用 Alarm 套件
{: #openwhisk_catalog_alarm}

`/whisk.system/alarms` 套件可以用來依指定的頻率發動觸發程式。這適用於設定循環工作或作業（例如，每個小時呼叫系統備份動作）。

該套件包含下列資訊來源。

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | 套件 | - | 警示及定期公用程式 |
| `/whisk.system/alarms/alarm` | 資訊來源 | cron、trigger_payload、maxTriggers | 定期發動觸發程式事件 |


### 定期發動觸發程式事件
{: #openwhisk_catalog_alarm_fire}

`/whisk.system/alarms/alarm` 資訊來源會配置 Alarm 服務依指定的頻率發動觸發程式事件。參數如下所示：

- `cron`：根據 UNIX crontab 語法，指出何時發動觸發程式的字串（世界標準時間，UTC）。字串是五個欄位的序列，以空格區隔：`X X X X X`。
如需使用 cron 語法的詳細資料，請參閱：http://crontab.org。以下是一些以該字串指出的頻率範例：

  - `* * * * *`：每分鐘整分。
  - `0 * * * *`：每小時整點。
  - `0 */2 * * *`：每 2 小時（亦即 02:00:00、04:00:00、...）
  - `0 9 8 * *`：每月 8 日上午 9:00:00 (UTC)

- `trigger_payload`：每次發動觸發程式時，此參數的值都會變成觸發程式的內容。

- `maxTriggers`：在達到此限制時停止發動觸發程式。預設值為 1,000,000。您可以將其設定為無限 (-1)。

下列範例說明如何使用觸發程式事件中的 `name` 及 `place` 值來建立每 2 分鐘發動一次的觸發程式。

  ```
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron "*/2 * * * *" --param trigger_payload "{\"name\":\"Odin\",\"place\":\"Asgard\"}"
  ```
  {: pre}

每一個產生的事件都會包含為參數，即 `trigger_payload` 值所指定的內容。在此情況下，每一個觸發程式事件都會有參數 `name=Odin` 及 `place=Asgard`。

**附註**：參數 `cron` 也支援六個欄位的自訂語法，其中第一個欄位代表秒。
如需使用此自訂 cron 語法的詳細資料，請參閱：https://github.com/ncb000gt/node-cron。
以下是使用六個欄位表示法的範例：
  - `*/30 * * * * *`：每 30 秒。

## 使用 Weather 套件
{: #openwhisk_catalog_weather}

`/whisk.system/weather` 套件提供一種簡便的方式來呼叫 Weather Company Data for IBM Bluemix API。

該套件包含下列動作。

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/weather` | 套件 | username、password | Weather Company Data for IBM Bluemix API 的服務  |
| `/whisk.system/weather/forecast` | 動作 | latitude、longitude、timePeriod | 指定時段的預報|

建議使用 `username` 及 `password` 值來建立套件連結。如此，您就不需要每次在呼叫套件中的動作時都指定認證。

### 取得某個位置的天氣預報
{: #openwhisk_catalog_weather_forecast}

`/whisk.system/weather/forecast` 動作會從 The Weather Company 呼叫 API，以傳回某個位置的天氣預報。參數如下所示：

- `username`：獲授權呼叫預報 API 的 The Weather Company Data for IBM Bluemix 的使用者名稱。
- `password`：獲授權呼叫預報 API 的 The Weather Company Data for IBM Bluemix 的密碼。
- `latitude`：位置的緯度座標。
- `longitude`：位置的經度座標。
- `timeperiod`：預報的時段。有效選項為 '10day' -（預設值）傳回 10 天的每日預報、'48hour' - 傳回 2 天的每小時預報、'current' - 傳回目前的天氣狀況、'timeseries' - 傳回目前的觀察，以及從目前日期和時間算起，過去最多 24 小時的觀察。


下列範例說明如何建立套件連結，然後取得 10 天預報。

1. 使用 API 金鑰建立套件連結。

  ```
  wsk package bind /whisk.system/weather myWeather --param username MY_USERNAME --param password MY_PASSWORD
  ```
  {: pre}

2. 在套件連結中呼叫 `forecast` 動作，以取得天氣預報。

  ```
  wsk action invoke myWeather/forecast --blocking --result --param latitude 43.7 --param longitude -79.4
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

Watson 套件提供一種簡便的方式來呼叫各種 Watson API。

下列是提供的 Watson 套件：

| 套件 | 說明 |
| --- | --- |
| `/whisk.system/watson-translator`   | 文字翻譯及語言識別的套件 |
| `/whisk.system/watson-textToSpeech` | 將文字轉換為語音的套件 |
| `/whisk.system/watson-speechToText` | 將語音轉換為文字的套件 |

**附註** 目前已淘汰套件 `/whisk.system/watson`，請移轉至上面所提及的新套件，新的動作提供相同的介面。

### 使用 Watson Translator 套件

`/whisk.system/watson-translator` 套件提供一種簡便的方式來呼叫要翻譯的 Watson API。

該套件包含下列動作。

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/watson-translator` | 套件 | username、password | 文字翻譯及語言識別的套件  |
| `/whisk.system/watson-translator/translator` | 動作 | payload、translateFrom、translateTo、translateParam、username、password | 翻譯文字 |
| `/whisk.system/watson-translator/languageId` | 動作 | payload、username、password | 識別語言 |

**附註**：已淘汰套件 `/whisk.system/watson`（包括動作 `/whisk.system/watson/translate` 及 `/whisk.system/watson/languageId`）。

#### 在 Bluemix 中設定 Watson Translator 套件

如果您是從 Bluemix 使用 OpenWhisk，則 OpenWhisk 會自動建立 Bluemix Watson 服務實例的套件連結。

1. 在 Bluemix [儀表板](http://console.ng.Bluemix.net)中，建立 Watson Translator 服務實例。

  請務必記住服務實例的名稱，以及您所在的 Bluemix 組織及空間。

2. 確定 OpenWhisk CLI 位於對應至前一個步驟中所使用之 Bluemix 組織及空間的名稱空間中。

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  或者，您也可以使用 `wsk property set --namespace`，從可存取的名稱空間清單中設定名稱空間。

3. 重新整理名稱空間中的套件。重新整理會自動建立您所建立之 Watson 服務實例的套件連結。

  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_Translator_Credentials-1
  ```
  {: screen}

  ```
wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_Translator_Credentials-1 private
  ```
  {: screen}


#### 在 Bluemix 外部設定 Watson Translator 套件

如果您不是在 Bluemix 中使用 OpenWhisk，或者要在 Bluemix 外部設定 Watson Translator，則必須手動建立 Watson Translator 服務的套件連結。您需要 Watson Translator 服務使用者名稱及密碼。

- 建立針對 Watson Translator 服務所配置的套件連結。

  ```
  wsk package bind /whisk.system/watson-translator myWatsonTranslator -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### 翻譯文字
{: #openwhisk_catalog_watson_translate}

`/whisk.system/watson-translator/translator` 動作會將文字從某種語言翻譯成另一種語言。參數如下所示：

- `username`：Watson API 使用者名稱。
- `password`：Watson API 密碼。
- `payload`：要翻譯的文字。
- `translateParam`：指出要翻譯的文字的輸入參數。例如，如果 `translateParam=payload`，則會翻譯傳遞給動作的 `payload` 參數值。
- `translateFrom`：兩位數的來源語言代碼。
- `translateTo`：兩位數的目標語言代碼。

- 在套件連結中呼叫 `translator` 動作，以將某串文字從英文翻譯成法文。

  ```
  wsk action invoke myWatsonTranslator/translator --blocking --result --param payload 'Blue skies ahead' --param translateFrom 'en' --param translateTo 'fr'
  ```
  {: pre}

  ```
  {
      "payload": "Ciel bleu a venir"
  }
  ```
  {: screen}


#### 識別某串文字的語言
{: #openwhisk_catalog_watson_identifylang}

`/whisk.system/watson-translator/languageId` 動作識別某串文字的語言。參數如下所示：

- `username`：Watson API 使用者名稱。
- `password`：Watson API 密碼。
- `payload`：要識別的文字。

- 在套件連結中呼叫 `languageId` 動作，以識別語言。

  ```
  wsk action invoke myWatsonTranslator/languageId --blocking --result --param payload 'Ciel bleu a venir'
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


### 使用 Watson Text to Speech 套件
{: #openwhisk_catalog_watson_texttospeech}

`/whisk.system/watson-textToSpeech` 套件提供一種簡便的方式來呼叫要將文字轉換為語音的 Watson API。

該套件包含下列動作。

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/watson-textToSpeech` | 套件 | username、password | 將文字轉換為語音的套件 |
| `/whisk.system/watson-textToSpeech/textToSpeech` | 動作 | payload、voice、accept、encoding、username、password | 將文字轉換為音訊 |

**附註**：已淘汰套件 `/whisk.system/watson`（包括動作 `/whisk.system/watson/textToSpeech`）。

#### 在 Bluemix 中設定 Watson Text to Speech 套件

如果您是從 Bluemix 使用 OpenWhisk，則 OpenWhisk 會自動建立 Bluemix Watson 服務實例的套件連結。

1. 在 Bluemix [儀表板](http://console.ng.Bluemix.net)中，建立 Watson Text to Speech 服務實例。

  請務必記住服務實例的名稱，以及您所在的 Bluemix 組織及空間。

2. 確定 OpenWhisk CLI 位於對應至前一個步驟中所使用之 Bluemix 組織及空間的名稱空間中。

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  或者，您也可以使用 `wsk property set --namespace`，從可存取的名稱空間清單中設定名稱空間。

3. 重新整理名稱空間中的套件。重新整理會自動建立您所建立之 Watson 服務實例的套件連結。

  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_TextToSpeech_Credentials-1
  ```
  {: screen}

  ```
wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_TextToSpeec_Credentials-1 private
  ```
  {: screen}


#### 在 Bluemix 外部設定 Watson Text to Speech 套件

如果您不是在 Bluemix 中使用 OpenWhisk，或者要在 Bluemix 外部設定 Watson Text to Speech，則必須手動建立 Watson Text to Speech 服務的套件連結。您需要 Watson Text to Speech 服務使用者名稱及密碼。

- 建立針對 Watson Speech to Text 服務所配置的套件連結。

  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonTextToSpeech -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### 將某串文字轉換為語音
{: #openwhisk_catalog_watson_speechtotext}

`/whisk.system/watson-speechToText/textToSpeech` 動作會將某串文字轉換為音訊語音。參數如下所示：

- `username`：Watson API 使用者名稱。
- `password`：Watson API 密碼。
- `payload`：要轉換為語音的文字。
- `voice`：說話者的聲音。
- `accept`：語音檔的格式。
- `encoding`：語音二進位資料的編碼。


- 在套件連結中呼叫 `textToSpeech` 動作，以轉換文字。

  ```
  wsk action invoke myWatsonTextToSpeech/textToSpeech --blocking --result --param payload 'Hey.' --param voice 'en-US_MichaelVoice' --param accept 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```
  {
        "payload": "<base64 encoding of a .wav file>"
  }
  ```
  {: screen}


### 使用 Watson Speech to Text 套件
{: #openwhisk_catalog_watson_speechtotext}

`/whisk.system/watson-speechToText` 套件提供一種簡便的方式來呼叫要將語音轉換為文字的 Watson API。

該套件包含下列動作。

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/watson-speechToText` | 套件 | username、password | 將語音轉換為文字的套件 |
| `/whisk.system/watson-speechToText/speechToText` | 動作 | payload、content_type、encoding、username、password、continuous、inactivity_timeout、interim_results、keywords、keywords_threshold、max_alternatives、model、timestamps、watson-token、word_alternatives_threshold、word_confidence、X-Watson-Learning-Opt-Out | 將音訊轉換為文字 |

**附註**：已淘汰套件 `/whisk.system/watson`（包括動作 `/whisk.system/watson/speechToText`）。

#### 在 Bluemix 中設定 Watson Speech to Text 套件

如果您是從 Bluemix 使用 OpenWhisk，則 OpenWhisk 會自動建立 Bluemix Watson 服務實例的套件連結。

1. 在 Bluemix [儀表板](http://console.ng.Bluemix.net)中，建立 Watson Speech to Text 服務實例。

  請務必記住服務實例的名稱，以及您所在的 Bluemix 組織及空間。

2. 確定 OpenWhisk CLI 位於對應至前一個步驟中所使用之 Bluemix 組織及空間的名稱空間中。

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  或者，您也可以使用 `wsk property set --namespace`，從可存取的名稱空間清單中設定名稱空間。

3. 重新整理名稱空間中的套件。重新整理會自動建立您所建立之 Watson 服務實例的套件連結。

  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_SpeechToText_Credentials-1
  ```
  {: screen}

  ```
wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_SpeechToText_Credentials-1 private
  ```
  {: screen}


#### 在 Bluemix 外部設定 Watson Speech to Text 套件

如果您不是在 Bluemix 中使用 OpenWhisk，或者要在 Bluemix 外部設定 Watson Speech to Text，則必須手動建立 Watson Speech to Text 服務的套件連結。您需要 Watson Speech to Text 服務使用者名稱及密碼。

- 建立針對 Watson Speech to Text 服務所配置的套件連結。

  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonSpeechToText -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### 將語音轉換為文字

`/whisk.system/watson-speechToText/speechToText` 動作會將音訊語音轉換為文字。參數如下所示：

- `username`：Watson API 使用者名稱。
- `password`：Watson API 密碼。
- `payload`：要轉換為文字的已編碼語音二進位資料。
- `content_type`：音訊的 MIME 類型。
- `encoding`：語音二進位資料的編碼。
- `continuous`：指出是否傳回代表以長間歇分隔之連續詞組的多個最終結果。
- `inactivity_timeout`：時間（秒），如果在所提交的音訊中只偵測到靜音，將在此期限之後結束連線。
- `interim_results`：指出服務是否要傳回臨時結果。
- `keywords`：要在音訊中標示的關鍵字清單。
- `keywords_threshold`：信任值，其為標示關鍵字的下限。
- `max_alternatives`：要傳回之替代記錄的數目上限。
- `model`：要用於識別要求的模型 ID。
- `timestamps`：指出是否要為每個單字傳回時間校準。
- `watson-token`：提供服務的鑑別記號，以作為提供服務認證的替代方案。
- `word_alternatives_threshold`：信任值，其為將假設識別為可能替代字的下限。
- `word_confidence`：指出是否要為每個單字傳回範圍從 0 到 1 之間的信任測量值。
- `X-Watson-Learning-Opt-Out`：指出是否要拒絕呼叫的資料收集。
 

- 在套件連結中呼叫 `speechToText` 動作，以轉換已編碼的音訊。

  ```
  wsk action invoke myWatsonSpeechToText/speechToText --blocking --result --param payload <base64 encoding of a .wav file> --param content_type 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```
  {
        "data": "Hello Watson"
  }
  ```
  {: screen}
 
 
## 使用 Message Hub 套件
{: #openwhisk_catalog_message_hub}

此套件可讓您建立觸發程式，以在將訊息張貼至 Bluemix 上的 [Message Hub](https://developer.ibm.com/messaging/message-hub/) 服務實例時做出反應。

### 建立接聽 Message Hub 實例的觸發程式
{: #openwhisk_catalog_message_hub_trigger}
若要建立在將訊息張貼至 Message Hub 實例時做出反應的觸發程式，您需要使用名為 `messaging/messageHubFeed` 的資訊來源。此資訊來源支援下列參數：

|名稱|類型|說明|
|---|---|---|
|kafka_brokers_sasl|JSON 字串陣列|此參數是在 Message Hub 實例中包含分配管理系統的 `<host>:<port>` 字串陣列|
|使用者|字串|您的 Message Hub 使用者名稱|
|password|字串|您的 Message Hub 密碼|
|topic|字串|您想要觸發程式接聽的主題|
|kafka_admin_url|URL 字串|Message Hub 管理 REST 介面的 URL|
|api_key|字串|您的 Message Hub API 金鑰|
|isJSONData|布林（選用 - 預設=false）|設為 `true` 時，這會導致資訊來源先嘗試將訊息內容剖析為 JSON，然後再將它傳遞為觸發程式有效負載。|

雖然此參數清單看起來令人卻步，但是使用套件重新整理 CLI 指令時會自動進行設定：

1. 在用於 OpenWhisk 的現行組織及空間下，建立 Message Hub 服務實例。

2. 驗證您要接聽的主題已存在於 Message Hub 中，或建立新主題來接聽訊息（例如 `mytopic`）。

2. 重新整理名稱空間中的套件。重新整理會自動建立您所建立之 Message Hub 服務實例的套件連結。

  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Message_Hub_Credentials-1
  ```
  {: screen}

  ```
wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1 private
  ```
  {: screen}

  您的套件連結現在包含與 Message Hub 實例相關聯的認證。

3. 您現在只需要建立「觸發程式」，以在將新訊息張貼至 Message Hub 時發動。

  ```
  wsk trigger create MyMessageHubTrigger -f /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1/messageHubFeed -p topic mytopic
  ```
  {: pre}

### 在 Bluemix 外部設定 Message Hub 套件

如果您不是在 Bluemix 中使用 OpenWhisk，或者要在 Bluemix 外部設定 Message Hub，則必須手動建立 Message Hub 服務的套件連結。您需要 Message Hub 服務認證及連線資訊。

- 建立針對 Message Hub 服務所配置的套件連結。

  ```
  wsk trigger create MyMessageHubTrigger -f /whisk.system/messaging/messageHubFeed -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p topic mytopic -p user <your Message Hub user> -p password <your Message Hub password> -p kafka_admin_url https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443 -p api_key <your API key>
  ```
  {: pre}

### 接聽 Message Hub 實例的訊息
{: #openwhisk_catalog_message_hub_listen}
建立觸發程式之後，系統將會監視傳訊服務中的指定主題。張貼新的訊息時，將會發動觸發程式。

該觸發程式的有效負載將包含 `messages` 欄位，此欄位是自上次發動觸發程式後張貼的訊息陣列。陣列中的每一個訊息物件都會包含下列欄位：
- topic
- partition
- offset
- key
- value

在 Kafka 術語中，這些欄位應該十分清楚明瞭。不過，`value` 需要特殊考量。如果 `isJSONData` 參數在建立觸發程式時設為 `false`（或根本未設定），則 `value` 欄位將是所張貼訊息的原始值。不過，如果 `isJSONData` 在建立觸發程式時設為 `true`，則系統會嘗試根據最佳效能來將此值剖析為 JSON 物件。如果剖析成功，則觸發程式有效負載中的 `value` 將是產生的 JSON 物件。

例如，如果張貼 `{"title": "Some string", "amount": 5, "isAwesome": true}` 的訊息時 `isJSONData` 設為 `true`，則觸發程式有效負載可能類似下列內容：

```
{
  "messages": [
      {
        "partition": 0,
        "key": null,
        "offset": 421760,
        "topic": "mytopic",
        "value": {
            "amount": 5,
            "isAwesome": true,
            "title": "Some string"
        }
      }
  ]
}
```

不過，如果張貼相同的訊息內容時 `isJSONData` 設為 `false`，則觸發程式有效負載會類似下列內容：

```
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421761,
      "topic": "mytopic",
      "value": "{\"title\": \"Some string\", \"amount\": 5, \"isAwesome\": true}"
    }
  ]
}
```

### 分批處理訊息
您會注意到觸發程式有效負載包含訊息陣列。這表示，如果您正在極快速地產生傳訊系統的訊息，則資訊來源會嘗試將張貼的訊息分批處理為單一發動的觸發程式。這容許將訊息更快速且更有效率地張貼至觸發程式。

請記住，使用程式碼編寫觸發程式所發動的動作時，有效負載中的訊息數目在技術上是無界限的，但一律會大於 0。


## 使用 Slack 套件
{: #openwhisk_catalog_slack}

`/whisk.system/slack` 套件提供一種簡便的方式來使用 [Slack API](https://api.slack.com/)。

該套件包含下列動作：

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/slack` | 套件 | url、channel、username | 與 Slack API 互動 |
| `/whisk.system/slack/post` | 動作 | text、url、channel、username | 將訊息張貼至 Slack 通道 |

建議使用 `username`、`url` 及 `channel` 值來建立套件連結。使用連結，您就不需要每次在呼叫套件中的動作時都指定值。

### 將訊息張貼至 Slack 通道
{: #openwhisk_catalog_slack_post}

`/whisk.system/slack/post` 動作會將訊息張貼至指定的 Slack 通道。參數如下所示：

- `url`：Slack Webhook URL。
- `channel`：要將訊息張貼至其中的 Slack 通道。
- `username`：用來張貼訊息的名稱。
- `text`：要張貼的訊息。
- `token`：（選用）Slack [存取記號](https://api.slack.com/tokens)。如需如何使用 Slack 存取記號的詳細資料，請參閱[下面](./openwhisk_catalog.html#openwhisk_catalog_slack_token)。

下列範例說明如何配置 Slack、建立套件連結，以及將訊息張貼至通道。

1. 針對您的團隊配置 Slack [送入的 Webhook](https://api.slack.com/incoming-webhooks)。

  配置 Slack 之後，您會得到與下列類似的 Webhook URL：`https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`。在下一步中，您會需要它。

2. 使用 Slack 認證、要張貼至其中的通道，以及用來進行張貼的使用者名稱，來建立套件連結。

  ```
  wsk package bind /whisk.system/slack mySlack --param url "https://hooks.slack.com/services/..." --param username Bob --param channel "#MySlackChannel"
  ```
  {: pre}

3. 在套件連結中呼叫 `post` 動作，以將訊息張貼至 Slack 通道。

  ```
  wsk action invoke mySlack/post --blocking --result --param text "Hello from OpenWhisk!"
  ```
  {: pre}

### 使用 Slack 記號型 API
{: #openwhisk_catalog_slack_token}

如果您想要的話，可以選擇性地選擇使用 Slack 的記號型 API，而不是 Webhook API。如果您選擇這麼做，則請傳入包含 Slack [存取記號](https://api.slack.com/tokens)的 `token` 參數。您接著可以使用任何 [Slack API 方法](https://api.slack.com/methods)作為 `url` 參數。例如，若要張貼訊息，您將使用 `url` 參數值 [slack.postMessage](https://api.slack.com/methods/chat.postMessage)。

## 使用 GitHub 套件
{: #openwhisk_catalog_github}

`/whisk.system/github` 套件提供一種簡便的方來使用 [GitHub API](https://developer.github.com/)。

該套件包含下列資訊來源：

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/github` | 套件 | username、repository、accessToken | 與 GitHub API 互動 |
| `/whisk.system/github/webhook` | 資訊來源 | events、username、repository、accessToken | 在 GitHub 活動時發動觸發程式事件 |

建議使用 `username`、`repository` 及 `accessToken` 值來建立套件連結。使用連結，您就不需要每次使用套件中的資訊來源時都指定值。

### 發動 GitHub 活動的觸發程式事件
{: #openwhisk_catalog_github_fire}

`/whisk.system/github/webhook` 資訊來源會配置服務在指定 GitHub 儲存庫中有活動時發動觸發程式。參數如下所示：

- `username`：GitHub 儲存庫的使用者名稱。
- `repository`：GitHub 儲存庫。
- `accessToken`：GitHub 個人存取記號。[建立記號](https://github.com/settings/tokens)時，請務必選取 repo:status 及 public_repo 範圍。同時，請確定您尚未定義儲存庫的任何 Webhook。
- `events`：感興趣的 [GitHub 事件類型](https://developer.github.com/v3/activity/events/types/)。

下列範例說明如何建立在每次 GitHub 儲存庫有新確定時將發動的觸發程式。

1. 產生 GitHub [個人存取記號](https://github.com/settings/tokens)。

  下一步將會使用存取記號。

2. 建立使用存取記號針對 GitHub 儲存庫而配置的套件連結。

  ```
wsk package bind /whisk.system/github myGit --param username myGitUser --param repository myGitRepo --param accessToken aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}

3. 使用 `myGit/webhook` 資訊來源，以建立 GitHub `push` 事件類型的觸發程式。

  ```
wsk trigger create myGitTrigger --feed myGit/webhook --param events push
  ```
  {: pre}

使用 `git push` 來確定 GitHub 儲存庫時，會導致 Webhook 發動觸發程式。如果有符合觸發程式的規則，則會呼叫相關聯的動作。
此動作會接收 GitHub Webhook 有效負載作為輸入參數。每一個 GitHub Webhook 事件的 JSON 綱目都類似，但是為其事件類型所決定的唯一有效負載物件。
如需有效負載內容的相關資訊，請參閱 [GitHub 事件和有效負載](https://developer.github.com/v3/activity/events/types/) API 文件。


## 使用 Push 套件
{: #openwhisk_catalog_pushnotifications}

`/whisk.system/pushnotifications` 套件可讓您使用 Push 服務。 

該套件包含下列動作及資訊來源：

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | 套件 | appId、appSecret  | 使用 Push 服務 |
| `/whisk.system/pushnotifications/sendMessage` | 動作 | text、url、deviceIds、platforms、tagNames、apnsBadge、apnsCategory、apnsActionKeyTitle、apnsSound、apnsPayload、apnsType、gcmCollapseKey、gcmDelayWhileIdle、gcmPayload、gcmPriority、gcmSound、gcmTimeToLive | 將推送通知傳送至一個以上的指定裝置 |
| `/whisk.system/pushnotifications/webhook` | 資訊來源 | 事件 | 在 Push 服務上產生裝置活動（裝置登錄、取消註冊、訂閱或取消訂閱）時發動觸發程式事件 |
建議使用 `appId` 及 `appSecret` 值來建立套件連結。如此，您就不需要每次在呼叫套件中的動作時都指定這些認證。

### 建立 Push 套件連結
{: #openwhisk_catalog_pushnotifications_create}

建立 Push Notifications 套件連結時，您必須指定下列參數：

-  `appId`：Bluemix 應用程式 GUID。
-  `appSecret`：Bluemix 推送通知服務 appSecret。

下列範例說明如何建立套件連結。

1. 在 [Bluemix 儀表板](http://console.ng.bluemix.net)中建立 Bluemix 應用程式。

2. 起始設定「推送通知服務」，並將該服務連結至 Bluemix 應用程式。

3. 配置 [Push Notification 應用程式](https://console.ng.bluemix.net/docs/services/mobilepush/index.html)。

  請務必記住您建立之 Bluemix 應用程式的 `App GUID` 和 `App Secret`。


4. 建立與 `/whisk.system/pushnotifications` 連結的套件。

  ```
  wsk package bind /whisk.system/pushnotifications myPush -p appId myAppID -p appSecret myAppSecret
  ```
  {: pre}

5. 驗證套件連結已存在。

  ```
wsk package list
  ```
  {: pre}

  ```
  packages
  /myNamespace/myPush private binding
  ```
  {: screen}

### 傳送推送通知
{: #openwhisk_catalog_pushnotifications_send}

`/whisk.system/pushnotifications/sendMessage` 動作會將推送通知傳送至已登錄的裝置。參數如下所示：
- `text`：要對使用者顯示的通知訊息。例如：`-p text "Hi ,OpenWhisk send a notification"`。
- `url` - 可隨著警示一起傳送的選用性 URL。例如：`-p url "https:\\www.w3.ibm.com"`。
- `deviceIds` 所指定裝置的清單。例如：`-p deviceIds "[\"deviceID1\"]"`。
- `platforms` 將通知傳送至指定平台的裝置。'A' 表示 Apple (iOS) 裝置，而 'G' 表示 google (Android) 裝置。例如 `-p platforms "[\"A\"]"`。
- `tagNames` 將通知傳送至已訂閱其中任何標籤的裝置。例如 `-p tagNames "[\"tag1\"]" `。
- `gcmPayload`：會放在通知訊息中一起傳送的自訂 JSON 有效負載。例如：`-p gcmPayload "{\"hi\":\"hello\"}"`
- `gcmSound`：當通知到達裝置時，將會嘗試播放的音效檔（在裝置上）。
- `gcmCollapseKey`：此參數可識別訊息的群組。
- `gcmDelayWhileIdle`：當此參數設為 true 時，表示要等到裝置變成作用中時才會傳送訊息。
- `gcmPriority`：設定訊息的優先順序。
- `gcmTimeToLive`：此參數指定當裝置離線時，訊息保留在 GCM 儲存空間中多久（以秒為單位）。
- `apnsBadge`：要顯示成應用程式圖示徽章的數字。
- `apnsCategory`：要用於互動式推送通知的種類 ID。
- `apnsIosActionKey`：動作鍵的標題。
- `apnsPayload`：會放在通知訊息中一起傳送的自訂 JSON 有效負載。
- `apnsType`：['DEFAULT'、'MIXED'、'SILENT']。
- `apnsSound`：應用程式組合中的音效檔名稱。將會播放此檔案的音效作為警示。

下面是從推送通知套件傳送推送通知的範例。

1. 使用您先前建立之套件連結中的 `sendMessage` 動作來傳送推送通知。請務必將 `/myNamespace/myPush` 取代成您的套件名稱。

  ```
  wsk action invoke /myNamespace/myPush/sendMessage --blocking --result  -p url https://example.com -p text "this is my message"  -p sound soundFileName -p deviceIds "[\"T1\",\"T2\"]"
  ```
  {: pre}

  ```
  {
  "result": {
          "pushResponse": "{"messageId":"11111H","message":{"message":{"alert":"this is my message","url":"http.google.com"},"settings":{"apns":{"sound":"default"},"gcm":{"sound":"default"},"target":{"deviceIds":["T1","T2"]}}}"
  },
      "status": "success",
      "success": true
  }
  ```
  {: screen}

### 發動 Push 活動的觸發程式事件
{: #openwhisk_catalog_pushnotifications_fire}

`/whisk.system/pushnotifications/webhook` 將 Push 服務配置成：當指定的應用程式中有裝置活動（例如裝置登錄/取消登錄或訂閱/取消訂閱）時，即發動觸發程式

參數如下所示：

- `appId`：Bluemix 應用程式 GUID。
- `appSecret`：Bluemix 推送通知服務 appSecret。
- `events`：支援的事件為 `onDeviceRegister`、`onDeviceUnregister`、`onDeviceUpdate`、`onSubscribe`、`onUnsubscribe`。如果所有事件都要通知，請使用萬用字元 `*`。

下列範例說明如何建立在每次有新裝置向 Push Notifications 服務應用程式登錄時即發動的觸發程式。

1. 使用 appId 和 appSecret 來建立為 Push Notifications 服務所配置的套件連結。

  ```
  wsk package bind /whisk.system/pushnotifications myNewDeviceFeed --param appID myapp --param appSecret myAppSecret --param events onDeviceRegister
  ```
  {: pre}

2. 使用 `myPush/webhook` 資訊來源，為 Push Notifications 服務的 `onDeviceRegister` 事件類型建立觸發程式。

  ```
  wsk trigger create myPushTrigger --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}
