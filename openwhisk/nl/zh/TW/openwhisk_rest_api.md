---

copyright:
  years: 2017
lastupdated: "2017-05-04"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用 OpenWhisk REST API
{: #openwhisk_rest_api}

啟用 OpenWhisk 環境之後，即可利用 REST API 呼叫來搭配使用 OpenWhisk 與 Web 應用程式或行動應用程式。

如需動作、啟動、套件、規則及觸發程式 API 的詳細資料，請參閱 [OpenWhisk API 文件](http://petstore.swagger.io/?url=https://raw.githubusercontent.com/openwhisk/openwhisk/master/core/controller/src/main/resources/apiv1swagger.json)。


系統中的所有功能都可透過 REST API 來使用。其中有動作、觸發程式、規則、套件、啟動和名稱空間的集合和實體端點。

以下是集合端點：
- `https://{APIHOST}/api/v1/namespaces`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/actions`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/triggers`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/rules`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/packages`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/activations`

`{APIHOST}` 是 OpenWhisk API 主機名稱（例如，openwhisk.ng.bluemix.net、172.17.0.1、192.168.99.100、192.168.33.13 等）。
針對 `{namespace}`，字元 `_` 可以用來指定使用者的 *預設名稱空間*。

您可以在集合端點上執行 GET 要求，以提取集合中的實體清單。

每一種實體類型都有實體端點：
- `https://{APIHOST}/api/v1/namespaces/{namespace}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/actions/[{packageName}/]{actionName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/triggers/{triggerName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/rules/{ruleName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/packages/{packageName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/activations/{activationName}`

名稱空間和啟動端點僅支援 GET 要求。動作、觸發程式、規則和套件端點可支援 GET、PUT 及 DELETE 要求。動作、觸發程式和規則的端點也可支援 POST 要求（用來呼叫動作和觸發程式，以及啟用或停用規則）。 

所有 API 都是透過 HTTP 基本鑑別進行保護。您可以使用 [wskadmin](../tools/admin/wskadmin) 工具來產生新的名稱空間及鑑別。
基本鑑別認證位於 `~/.wskprops` 檔案的 `AUTH` 內容中，以冒號區隔。您也可以使用執行 `wsk property get --auth` 的 CLI 來擷取這些認證。


下列範例說明如何使用 [cURL](https://curl.haxx.se) 指令工具來取得 `whisk.system` 名稱空間中的所有套件清單：

```bash
curl -u USERNAME:PASSWORD https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/packages
```
{: pre}

```json
  [
      {
    "name": "slack",
    "binding": false,
    "publish": true,
    "annotations": [
      {
        "key": "description",
        "value": "Package that contains actions to interact with the Slack messaging service"
      }
    ],
    "version": "0.0.1",
    "namespace": "whisk.system"
  }
]
```

在此範例中，已使用 `-u` 旗標來傳遞鑑別，您也可以將此值傳遞為 `https://$AUTH@{APIHOST}` 格式的 URL 一部分

OpenWhisk API 支援 Web 用戶端發出的「要求/回應」呼叫。OpenWhisk 會以「跨原點資源共用」標頭來回應 `OPTIONS` 要求。目前可允許所有原點（亦即，Access-Control-Allow-Origin 為 "`*`"），而 Access-Control-Allow-Header 會產生 Authorization 和 Content-Type。

**注意：**因為 OpenWhisk 目前針對每個名稱空間僅支援一個金鑰，所以不建議在簡單實驗之外使用 CORS。使用 [Web 動作](webactions.md)或 [API 閘道](apigateway.md)以將動作公開，而且不會使用需要 CORS 的用戶端應用程式的 OpenWhisk 授權金鑰。

## 使用 CLI 詳細模式
{: #openwhisk_rest_api_cli_v}
OpenWhisk CLI 是 OpenWhisk REST API 的介面。
您可以使用旗標 `-v` 以詳細模式執行 CLI，這樣會列印 HTTP 要求及回應的所有資訊。

讓我們嘗試取得現行使用者的名稱空間值。
```
wsk namespace list -v
```
{: pre}
```
REQUEST:
[GET]	https://openwhisk.ng.bluemix.net/api/v1/namespaces
Req Headers
{
  "Authorization": [
    "Basic XXXYYYY"
  ]
}
RESPONSE:Got response with code 200
Resp Headers
{
  "Content-Type": [
    "application/json; charset=UTF-8"
  ]
}
Response body size is 28 bytes
Response body received:
["john@example.com_dev"]
```

如您所見，列印的資訊提供 HTTP 要求的內容，它會使用「基本授權」標頭 `Basic XXXYYYY`，以在 URL `https://openwhisk.ng.bluemix.net/api/v1/namespaces` 上執行 HTTP 方法 `GET`。
請注意，授權值是 base64 編碼的 OpenWhisk 授權字串。
回應的內容類型為 `application/json`。

## 動作
{: #openwhisk_rest_api_actions}
若要建立或更新動作，請在 actions 集合上使用方法 `PUT` 來傳送 HTTP 要求。例如，若要使用單一檔案內容來建立名稱為 `hello` 的 `nodejs:6` 動作，請使用下列指令：
```bash
curl -u $AUTH -d '{"namespace":"_","name":"hello","exec":{"kind":"nodejs:6","code":"function main(params) { return {payload:\"Hello \"+params.name}}"}}' -X PUT -H "Content-Type: application/json" https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?overwrite=true 
```
{: pre}

若要對動作執行封鎖呼叫，並使用方法 `POST` 以及包含輸入參數 `name` 的內文來傳送 HTTP 要求，請使用下列指令：
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?blocking=true \
-X POST -H "Content-Type: application/json" \
-d '{"name":"John"}'  
```
{: pre}
您會取得下列回應：
```json
{
  "duration": 2,
  "name": "hello",
  "subject": "john@example.com_dev",
  "activationId": "c7bb1339cb4f40e3a6ccead6c99f804e",
  "publish": false,
  "annotations": [{
    "key": "limits",
    "value": {
      "timeout": 60000,
      "memory": 256,
      "logs": 10
    }
  }, {
    "key": "path",
    "value": "john@example.com_dev/hello"
  }],
  "version": "0.0.1",
  "response": {
    "result": {
          "payload": "Hello John"
    },
    "success": true,
    "status": "success"
  },
  "end": 1493327653769,
  "logs": [],
  "start": 1493327653767,
  "namespace": "john@example.com_dev"
}
```
如果您只要取得 `response.result`，請使用查詢參數 `result=true` 重新執行指令：
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?blocking=true&result=true" \
-X POST -H "Content-Type: application/json" \
-d '{"name":"John"}' 
```
{: pre}
您會取得下列回應：
```json
{
  "payload": "hello John"
}
```

## 註釋及 Web 動作
{: #openwhisk_rest_api_webactions}
若要將動作建立為 Web 動作，您需要針對 Web 動作新增 `web-export=true` 的[註釋](annotations.md)。因為 Web 動作可以公開存取，所以您應該使用註釋 `final=true` 來保護預先定義的參數（亦即，將它們視為最終）。如果您使用 CLI 旗標 `--web true` 來建立或更新動作，則此指令會同時新增 `web-export=true` 及 `final=true` 註釋。

請執行 curl 指令，以提供要在動作上設定的完整註釋清單
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"hello","exec":{"kind":"nodejs:6","code":"function main(params) { return {payload:\"Hello \"+params.name}}"},"annotations":[{"key":"web-export","value":true},{"key":"raw-http","value":false},{"key":"final","value":true}]}'
```
{: pre}
您現在可以將此動作呼叫為沒有 OpenWhisk 授權的公用 URL。例如，請使用在 URL 尾端包括選用副檔名（例如 `.json` 或 `.http`）的 Web 動作公用 URL，來嘗試進行呼叫。
```bash
curl https://openwhisk.ng.bluemix.net/api/v1/web/john@example.com_dev/default/hello.json?name=John
```
{: pre}
```json
{
  "payload": "Hello John"
}
```
請注意，此範例原始碼不會使用 `.http`，請參閱 [Web 動作](webactions.md)文件以瞭解如何修改。

## 序列
{: #openwhisk_rest_api_sequences}
若要建立動作序列，則建立方式是提供依所需順序組合序列的動作的名稱，以將第一個動作的輸出傳遞為下一個動作的輸入。

$ wsk action create sequenceAction --sequence /whisk.system/utils/split,/whisk.system/utils/sort

使用動作 `/whisk.system/utils/split` 及 `/whisk.system/utils/sort`，來建立序列。
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/sequenceAction?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"sequenceAction","exec":{"kind":"sequence","components":["/whisk.system/utils/split","/whisk.system/utils/sort"]},"annotations":[{"key":"web-export","value":true},{"key":"raw-http","value":false},{"key":"final","value":true}]}' 
```
{: pre}

請考慮何時指定動作的名稱，而且它們必須是完整的。

## 觸發程式
{: #openwhisk_rest_api_triggers}
若要建立觸發程式，您至少需要觸發程式名稱資訊。您也可以併入預設參數，以在發動觸發程式時透過規則來傳遞至動作。

使用已設定值 `webhook` 的預設參數 `type`，來建立名稱為 `events` 的觸發程式。
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/events?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"events","parameters":[{"key":"type","value":"webhook"}]}' 
```
{: pre}

現在，只要您的事件需要發動此觸發程式，您都可以搭配使用方法 `POST` 與「OpenWhisk 授權」金鑰來取得 HTTP 要求。

若要使用參數 `temperature` 來發動觸發程式 `events`，請傳送下列 HTTP 要求。

```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/events \
-X POST -H "Content-Type: application/json" \
-d '{"temperature":60}' 
```
{: pre}

### 具有資訊來源動作的觸發程式
{: #openwhisk_rest_api_triggers_feed}
您可以使用資訊來源動作而建立的一些特殊觸發程式。資訊來源動作是一種動作，可協助在發生觸發程式的事件時配置將負責發動觸發程式的資訊來源提供者。請參閱 [feeds.md] 文件，以進一步瞭解這些資訊來源提供者。

運用資訊來源動作的部分可用觸發程式為定期/警示、Slack、Github、Cloudant/Couchdb 及 messageHub/Kafka。您也可以建立自己的資訊來源動作及資訊來源提供者。

讓我們建立名稱為 `periodic` 且要依所指定頻率（每 2 小時，即 02:00:00、04:00:00、...）發動的觸發程式。

使用 CLI，這只要使用一個指令就能完成
```bash
wsk trigger create periodic --feed /whisk.system/alarms/alarm \
  --param cron "0 */2 * * *" -v
```
{: pre}
如您所見，因為我們將使用 `-v` 旗標來傳送兩個 HTTP 要求，一個會建立觸發程式 `periodic`，另一個則會使用配置資訊來源提供者每 2 小時發動觸發程式的參數來呼叫資訊來源動作 `/whisk.system/alarms/alarm`。

若要使用 REST API 來執行相同的作業，請先建立觸發程式
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/periodic?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"periodic","annotations":[{"key":"feed","value":"/whisk.system/alarms/alarm"}]}'  
```
{: pre}

如您所見，註釋 `feed` 儲存在觸發程式中。我們稍後將使用此註釋來得知在刪除觸發程式時要使用的資訊來源動作。

現在已建立觸發程式，讓我們呼叫資訊來源動作
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/actions/alarms/alarm?blocking=true&result=false" \
-X POST -H "Content-Type: application/json" \
-d "{\"authKey\":\"$AUTH\",\"cron\":\"0 */2 * * *\",\"lifecycleEvent\":\"CREATE\",\"triggerName\":\"/_/periodic\"}" 
```
{: pre}

刪除觸發程式與建立觸發程式類似，目前會刪除觸發程式，也會使用資訊來源動作來配置資訊來源提供者刪除觸發程式的處理程式。

呼叫資訊來源動作，以從資訊來源提供者刪除觸發處理程式
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/actions/alarms/alarm?blocking=true&result=false" \
-X POST -H "Content-Type: application/json" \
-d "{\"authKey\":\"$AUTH\",\"lifecycleEvent\":\"DELETE\",\"triggerName\":\"/_/periodic\"}"  
```
{: pre}

現在，使用 `DELETE` 方法來刪除具有 HTTP 要求的觸發程式
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/periodic \
-X DELETE -H "Content-Type: application/json" 
```
{: pre}

## 規則
{: #openwhisk_rest_api_rules}
若要建立可建立觸發程式與動作關聯的規則，請在要求內文中提供觸發程式及動作，以使用 `PUT` 方法來傳送 HTTP 要求。
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/rules/t2a?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"t2a","status":"","trigger":"/_/events","action":"/_/hello"}' 
```
{: pre}

可以啟用或停用規則，而且您可以更新規則的狀態內容來變更規則的狀態。例如，若要停用規則 `t2a`，請使用 `POST` 方法來傳送要求 `status: "inactive"` 的內文。
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/rules/t2a?overwrite=true \
-X POST -H "Content-Type: application/json" \
-d '{"status":"inactive","trigger":null,"action":null}'  
```
{: pre}

## 套件
{: #openwhisk_rest_api_packages}
若要在套件中建立動作，您需要先建立套件，若要建立名稱為 `iot` 的套件，請使用 `PUT` 方法來傳送 HTTP 要求。

```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/packages/iot?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"iot"}' 
```
{: pre}

## 啟動
{: #openwhisk_rest_api_activations}
若要取得最後 3 個啟動的清單，請利用 `GET` 方法來使用 HTTP 要求，並傳遞查詢參數 `limit=3`
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/activations?limit=3
```
{: pre}

若要取得啟動的所有詳細資料（包括結果及日誌），請使用 `GET` 方法來傳送 HTTP 要求，並將啟動 ID 傳遞為路徑參數
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/activations/f81dfddd7156401a8a6497f2724fec7b
```
{: pre}
