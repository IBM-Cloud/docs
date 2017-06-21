---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-26"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# API 閘道
{: #openwhisk_apigateway}

透過 API Management 進行管理，有利於 OpenWhisk 動作。

「API 閘道」用來作為 [Web 動作](webactions.md)的 Proxy，並提供它們其他特性，包括 HTTP 方法遞送、用戶端 ID/密碼、比率限制、CORS、檢視 API 用量及回應日誌，以及定義 API 共用原則。
如需「API 閘道」特性的相關資訊，您可以閱讀 [API Management 文件](/docs/apis/management/manage_openwhisk_apis.html#manage_openwhisk_apis)。

## 使用瀏覽器從 OpenWhisk Web 動作建立 API。

使用「API 閘道」，您可以將 OpenWhisk 動作公開為 API。在您定義 API 之後，可以套用安全及比率限制原則、檢視 API 用量及回應日誌，以及定義 API 共用原則。在「OpenWhisk 儀表板」中，按一下 [API](https://console.ng.bluemix.net/openwhisk/apimanagement) 標籤。


## 使用 CLI 從 OpenWhisk Web 動作建立 API

### OpenWhisk CLI 配置

使用 apihost `wsk property set --apihost openwhisk.ng.bluemix.net` 配置 OpenWhisk CLI
若要可以使用 `wsk api`，CLI 配置檔 `~/.wskprops` 需要包含「Bluemix 存取記號」。
若要取得存取記號，請使用 CLI 指令 `wsk bluemix login`。如需該指令的相關資訊，請執行 `wsk bluemix login -h`

**附註：**如果發生需要單一登入 (sso) 的指令錯誤，則這目前不予支援。暫行解決方法是搭配使用 Bluemix CLI 與 `bluemix login` 進行登入，然後將「存取記號」從 HOME 目錄配置檔 `~/.bluemix/.cf/config.json` 複製到 `~/.wskprops` 檔案，以作為內容 `APIGW_ACCESS_TOKEN="value of AccessToken`。複製存取記號字串時，請移除字首 `Bearer`。

**附註：**您使用 `wsk api-experimental` 所建立的 API 將會繼續運作一小段期間，但您應該要開始將 API 移轉至 Web 動作，並使用新的 CLI 指令 `wsk api` 來重新配置現有 API。

### 使用 CLI 建立第一個 API

1. 建立含有下列內容的 JavaScript 檔。在此範例中，檔名是 'hello.js'。
  ```javascript
  function main({name:name='Serverless API'}) {
      return {payload: `Hello world ${name}`};
  }
  ```
  {: codeblock}
  
2. 從下列 JavaScript 函數建立 Web 動作。在此範例中，動作稱為 'hello'。請一定要新增旗標 `--web true`
  
  ```
  wsk action create hello hello.js --web true
  ```
  {: pre}
  ```
  ok: created action hello
  ```
  
3. 搭配使用基礎路徑 `/hello`、路徑 `/world` 及方法 `get` 與回應類型 `json` 來建立 API
  
  ```
  wsk api create /hello /world get hello --response-type json
  ```
  ```
  ok: created API /hello/world GET for action /_/hello
  https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/hello/world
  ```
  會產生新的 URL，透過 **GET** HTTP 方法公開 `hello` 動作。
  
4. 讓我們將 HTTP 要求傳送至 URL 來試試。
  
  ```
  $ curl https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/hello/world?name=OpenWhisk
  ```
  ```json
  {
     "payload": "Hello world OpenWhisk"
  }
  ```
  已呼叫 Web 動作 `hello`，並傳回 JSON 物件，包括透過查詢參數所傳送的 `name` 參數。您可以透過簡單查詢參數或透過要求內文，以將參數傳遞給動作。Web 動作可讓您公開呼叫動作，而不使用 OpenWhisk 授權 API 金鑰。
  
### HTTP 回應的完整控制
  
  `--response-type` 旗標控制要透過「API 閘道」進行 Proxy 處理之 Web 動作的目標 URL。如上使用 `--response-type json`，會傳回 JSON 格式的完整動作結果，並將 Content-Type 標頭自動設定為 `application/json`，以讓您輕鬆開始使用。 
  
  開始使用之後，您要具有 HTTP 回應內容的完整控制（例如 `statusCode`、`headers`），並在 `body` 中傳回不同內容類型。作法是使用 `--response-type http`，這樣會使用 `http` 延伸來配置 Web 動作的目標 URL。

  您可以選擇使用 `http` 延伸來變更動作的程式碼以符合 Web 動作的傳回，或包括一連串的動作可將其結果傳遞給新動作，以將結果轉換為 HTTP 回應的正確格式。您可以在 [Web 動作](webactions.md)文件中深入閱讀回應類型及 Web 動作延伸。

  變更傳回 JSON 內容 `body`、`statusCode` 及 `headers` 之 `hello.js` 的程式碼
  ```javascript
  function main({name:name='Serverless API'}) {
      return { 
    body: new Buffer(JSON.stringify({payload:`Hello world ${name}`})).toString('base64'), 
        statusCode:200, 
        headers:{ 'Content-Type': 'application/json'}
      };
  }
  ```
  {: codeblock}
  請注意，需要傳回以 `base64` 編碼的內文，而非字串。
  
  使用修改過的結果來更新動作
  ```
  wsk action update hello hello.js --web true
  ```
  {: pre}
  使用 `--response-type http` 來更新 API
  ```
  wsk api create /hello /world get hello --response-type http
  ```
  {: pre}
  呼叫更新過的 API
  ```
  curl https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/hello/world
  ```
  {: pre}
  ```json
  {
     "payload": "Hello world Serverless API"
  }
  ```
  現在，您已完整控制 API、可以控制內容（例如傳回 HTML），或設定事項的狀態碼，例如「找不到」(404)、「未獲授權」(401) 、甚至「內部錯誤」(500)。

### 公開多個 Web 動作

假設您要公開好友讀書會的一組動作。
您有一系列的動作，以實作您的讀書會後端：

| 動作 | HTTP 方法 (HTTP method) | 說明 |
| ----------- | ----------- | ------------ |
| getBooks    | GET | 取得書籍詳細資料  |
| postBooks   | POST | 新增書籍 |
| putBooks    | PUT | 更新書籍詳細資料 |
| deleteBooks | DELETE | 刪除書籍 |

請使用 `/club` 作為其 HTTP URL 基本路徑、`books` 作為其資源，建立讀書會的 API（名為 `Book Club`）。
```
wsk api create -n "Book Club" /club /books get getBooks --response-type http
wsk api create /club /books post postBooks              --response-type http
wsk api create /club /books put putBooks                --response-type http
wsk api create /club /books delete deleteBooks          --response-type http
```

請注意，以基本路徑 `/club` 公開的第一個動作會取得名為 `Book Club` 的 API 標籤。在 `/club` 下公開的任何其他動作都會與 `Book Club` 相關聯。

讓我們列出所有剛剛公開的動作。

```
wsk api list -f
```
```
ok: APIs
Action: getBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: get
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: postBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: post
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: putBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: put
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: deleteBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: delete
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```

現在，讓我們使用 HTTP **POST** 來新增 `JavaScript: The Good Parts` 書籍－好玩而已。
```
curl -X POST -d '{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}' https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
```
{
  "result": "success"
}
```

透過 HTTP **GET**，使用我們的動作 `getBooks` 來取得書籍清單。
```
curl -X GET https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
```
{
  "result": [{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}]
}
```

### 匯出配置
將名為 `Book Club` 的 API 匯出至檔案，我們可以用它為基礎，使用檔案作為輸入來重建 API。 
```
wsk api get "Book Club" > club-swagger.json
```

讓我們先刪除一般基本路徑下的所有已公開 URL，來測試 Swagger 檔案。
您可以使用基本路徑 `/club` 或 API 名稱標籤 `"Book Club"` 刪除所有已公開 URL：
```
wsk api delete /club
```
```
ok: deleted API /club
```
### 變更配置

您可以在「OpenWhisk 儀表板」中編輯配置，按一下 [API](https://console.ng.bluemix.net/openwhisk/apimanagement) 標籤來設定安全、比率限制及其他特性。

### 匯入配置

現在，讓我們使用檔案 `club-swagger.json` 來還原名為 `Book Club` 的 API。
```
wsk api create --config-file club-swagger.json
```
```
ok: created api /books delete for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books get for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books post for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books put for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```

我們可以驗證已重建 API。
```
wsk api list /club
```
```
ok: apis
Action                    Verb         API Name        URL
getBooks                   get         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
postBooks                 post         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
putBooks                   put         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
deleteBooks             delete         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
