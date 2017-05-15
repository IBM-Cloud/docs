---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-24"

---

{:shortdesc: .shortdesc}
{:codeblock:.codeblock}
{:screen:.screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 系統詳細資料
{: #openwhisk_reference}


下列各節提供有關 {{site.data.keyword.openwhisk}} 系統的其他詳細資料。
{: shortdesc}

## {{site.data.keyword.openwhisk_short}} 實體
{: #openwhisk_entities}

### 名稱空間及套件
{: #openwhisk_entities_namespaces}

{{site.data.keyword.openwhisk_short}} 動作、觸發程式及規則屬於名稱空間，而且可以選擇性地屬於套件。

套件可以包含動作及資訊來源。套件不能包含另一個套件，因此不容許巢狀套件。實體也不需要包含在套件中。

在 Bluemix 中，組織+空間配對對應至 {{site.data.keyword.openwhisk_short}} 名稱空間。例如，組織 `BobsOrg` 及空間 `dev` 將對應至 {{site.data.keyword.openwhisk_short}} 名稱空間 `/BobsOrg_dev`。

如果您已獲授權，請自行建立名稱空間。`/whisk.system` 名稱空間是保留供隨 {{site.data.keyword.openwhisk_short}} 系統一起配送的實體使用。


### 完整名稱
{: #openwhisk_entities_fullyqual}

實體的完整名稱是 `/namespaceName[/packageName]/entityName`。請注意，`/` 是用來區隔名稱空間、套件及實體。名稱空間的前面也必須加上 `/`。

為方便起見，您可以停止使用者的*預設名稱空間*。

例如，請考慮預設名稱空間為 `/myOrg` 的使用者。下列範例說明一些實體的完整名稱及其別名。

| 完整名稱 | 別名 | 名稱空間 | 套件 | 名稱 |
| --- | --- | --- | --- | --- |
| `/whisk.system/cloudant/read` |  | `/whisk.system` | `cloudant` | `read` |
| `/myOrg/video/transcode` | `video/transcode` | `/myOrg` | `video` | `transcode` |
| `/myOrg/filter` | `filter` | `/myOrg` |  | `filter` |

在其他位置中，使用 {{site.data.keyword.openwhisk_short}} CLI 時，將會使用此命名方法。

### 實體名稱
{: #openwhisk_entities_names}

所有實體（包括動作、觸發程式、規則、套件及名稱空間）的名稱都是遵循下列格式的一串字元：

* 第一個字元必須是英數字元或底線。
* 後續字元可以是英數字元、空格或下列任何一項：`_`、`@`、`.`、`-`。
* 最後一個字元不能是空格。

更精確地來說，名稱必須符合下列正規表示式（以 Java meta 字元語法表示）：`\A([\w]|[\w][\w@ .-]*[\w@.-]+)\z`。


## 動作語意
{: #openwhisk_semantics}

下列各節說明 {{site.data.keyword.openwhisk_short}} 動作的詳細資料。

### 無狀態
{: #openwhisk_semantics_stateless}

動作實作應該是無狀態，或*等冪*。雖然系統不會強制執行此內容，但是不保證在呼叫之間可以使用動作所維護的任何狀態。

此外，動作可能會有多個說明實例，而且每個說明實例都有自己的狀態。動作呼叫可能會分派至所有這些說明實例。

### 呼叫輸入及輸出
{: #openwhisk_semantics_invocationio}

動作的輸入及輸出是鍵值組的字典。索引鍵是字串，而值是有效的 JSON 值。

### 動作的呼叫順序
{: #openwhisk_ordering}

動作不是依序進行呼叫。如果使用者從指令行或 REST API 呼叫動作兩次，則可能會先執行第二次呼叫，再執行第一次呼叫。如果動作有負面影響，則可能會依任意順序觀察到它們。

此外，不保證將自動執行動作。可以同時執行兩個動作，而其負面影響可能會交錯。OpenWhisk 無法確保任何特定並行一致性模型是否有負面影響。所有並行性負面影響都是相依實作。

### 動作執行保證
{: #openwhisk_atmostonce}

收到呼叫要求時，系統會記錄要求，並分派啟動。

系統會傳回啟動 ID（如果是非封鎖呼叫），以確認收到呼叫。請注意，如果在您收到 HTTP 回應之前發生網路失敗或其他干擾失敗，則 {{site.data.keyword.openwhisk_short}} 可能已接受並處理要求。

系統嘗試呼叫該動作一次，而導致下列四種結果的其中一種：
- *成功*：動作呼叫已順利完成。
- *應用程式錯誤*：動作呼叫成功，但動作故意傳回錯誤值（例如，因為引數的前置條件不相符）。
- *動作開發人員錯誤*：已呼叫動作，但異常完成（例如，動作偵測不到異常狀況，或有語法錯誤）。
- *Whisk 內部錯誤*：系統無法呼叫動作。結果會記錄在啟動記錄的 `status` 欄位中（如下節所記載）。

每個成功收到的呼叫以及每個可能向使用者收費的呼叫，最後都會有一筆啟動記錄。

請注意，如果發生*動作開發人員錯誤*，則動作可能會局部執行，並產生外部可見的負面影響。使用者必須負責檢查是否實際發生這類負面影響，並在想要時發出重試邏輯。也請注意，特定 *whisk 內部錯誤* 將指出動作已開始執行，但系統在動作登錄完成之前失敗。

## 啟動記錄
{: #openwhisk_ref_activation}

每一個動作呼叫及觸發程式發動都會導致啟動記錄。

啟動記錄包含下列欄位：

- *activationId*：啟動 ID。
- *start* 及 *end*：記錄啟動開始及結束的時間戳記。值為 [UNIX 時間格式](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_15)。
- *namespace* 及 `name`：實體的名稱空間及名稱。
- *logs*：字串陣列，內含動作在其啟動期間所產生的日誌。每一個陣列元素都對應至動作之 `stdout` 或 `stderr` 的行輸出，並且包含日誌輸出的時間及串流。結構如下：`TIMESTAMP STREAM: LOG_OUTPUT`。
- *response*：定義索引鍵 `success`、`status` 及 `result` 的字典：
  - *status*：啟動結果，可能是下列其中一個值："success"、"application error"、"action developer error"、"whisk internal error"。
  - *success*：假設並且只有在狀態為 `"success"` 時，才會為 `true`
- *result*：包含啟動結果的字典。如果啟動成功，這會包含動作所傳回的值。如果啟動失敗，`result` 會包含 `error` 索引鍵，通常還會有失敗的說明。


## JavaScript 動作
{: #openwhisk_ref_javascript}

### 函數原型
{: #openwhisk_ref_javascript_fnproto}

{{site.data.keyword.openwhisk_short}} JavaScript 動作是在 Node.js 運行環境中執行。

以 JavaScript 撰寫的動作必須限制於單一檔案。此檔案可以包含多個函數，但依慣例，必須要有稱為 `main` 的函數，而且此函數是在呼叫動作時呼叫。例如，以下是具有多個函數的動作的範例。

```
function main() {return { payload: helper() }
}

function helper() {
    return new Date();
}
```
{: codeblock}

動作輸入參數被當作 `main` 函數的 JSON 物件參數來傳遞。成功啟動的結果也是 JSON 物件，但會根據動作是同步還是非同步（如下節所述），而以不同的方式傳回。


### 同步及非同步行為
{: #openwhisk_ref_javascript_synchasynch}

JavaScript 函數很常會在回呼函數中繼續執行，即使是函數返回之後也是一樣。考慮到這種情況，JavaScript 動作的啟動可以是*同步* 或*非同步*。

如果 main 函數在下列其中一種狀況下結束，則 JavaScript 動作的啟動是**同步**：

- main 函數結束，而未執行 `return` 陳述式。
- main 函數結束的原因為執行會傳回任何值（Promise *除外*）的 `return` 陳述式。

以下是同步動作範例。

```
// an action in which each path results in a synchronous activation
function main(params) {
  if (params.payload == 0) {return;
  } else if (params.payload == 1) {
     return {payload: 'Hello, World!'};
  } else if (params.payload == 2) {
    return {error: 'payload must be 0 or 1'};
  }
}
```
{: codeblock}

如果 main 函數因為傳回 Promise 而結束，則 JavaScript 動作的啟動為**非同步**。在此情況下，在滿足或拒絕 Promise 之前，系統會假設動作仍在執行中。
首先，開始實例化新 Promise 物件，並將回呼函數傳遞給它。此回呼接受兩個引數（resolve 及 reject），而這兩者同時也是函數。所有非同步程式碼都在該回呼內。


下列範例說明如何呼叫 resolve 函數來滿足 Promise。

```
function main(args) {
     return new Promise(function(resolve, reject) {
       setTimeout(function() {
            resolve({ done: true });
       }, 100);
    })
 }
```
{: codeblock}

下列範例說明如何呼叫 reject 函數來拒絕 Promise。

```
function main(args) {
     return new Promise(function(resolve, reject) {
       setTimeout(function() {
            reject({ done: true });
       }, 100);
    })
 }
```
{: codeblock}

某個動作在部分輸入上可能為同步，但在其他輸入上則為非同步。範例如下。

```
function main(params) {
     if (params.payload) {
         // asynchronous activation
         return new Promise(function(resolve, reject) {
                setTimeout(function() {
            resolve({ done: true });
                }, 100);
             })
      } else {
// synchronous activation
         return {done: true};
      }
  }
```
{: codeblock}

請注意，不論啟動是同步還是非同步，動作的呼叫都可以是封鎖或非封鎖。

### 已移除 JavaScript 廣域 whisk 物件

已移除廣域物件 `whisk`；請移轉 nodejs 動作，以使用替代方法。
對於函數 `whisk.invoke()` 及 `whisk.trigger()`，請使用已安裝的用戶端程式庫 [openwhisk](https://www.npmjs.com/package/openwhisk)。
對於 `whisk.getAuthKey()`，您可以從環境變數 `__OW_API_KEY` 取得 API 金鑰值。
對於 `whisk.error()`，您可以傳回已拒絕的 Promise（即 Promise.reject）。

### JavaScript 運行環境
{: #openwhisk_ref_javascript_environments}

在 Node.js 6.9.1 版環境中，依預設會執行 JavaScript 動作。如果在建立/更新動作時明確指定值為 'nodejs:6' 的 `--kind` 旗標，則 6.9.1 環境也會用於動作。
下列套件適用於 Node.js 6.9.1 環境：

- apn 2.1.2 版
- async 2.1.4 版
- btoa 1.1.2 版
- cheerio 0.22.0 版
- cloudant 1.6.2 版
- commander 2.9.0 版
- consul 0.27.0 版
- cookie-parser 1.4.3 版
- cradle 0.7.1 版
- errorhandler 1.5.0 版
- glob 7.1.1 版
- gm 1.23.0 版
- lodash 4.17.2 版
- log4js 0.6.38 版
- iconv-lite 0.4.15 版
- marked 0.3.6 版
- merge 1.2.0 版
- moment 2.17.0 版
- mongodb 2.2.11 版
- mustache 2.3.0 版
- nano 6.2.0 版
- node-uuid 1.4.7 版
- nodemailer 2.6.4 版
- oauth2-server 2.4.1 版
- openwhisk 3.3.2 版
- pkgcloud 1.4.0 版
- process 0.11.9 版
- pug 2.0.0-beta6 版
- redis 2.6.3 版
- request 2.79.0 版
- request-promise 4.1.1 版
- rimraf 2.5.4 版
- semver 5.3.0 版
- sendgrid 4.7.1 版
- serve-favicon 2.3.2 版
- socket.io 1.6.0 版
- socket.io-client 1.6.0 版
- superagent 3.0.0 版
- swagger-tools 0.10.1 版
- tmp 0.0.31 版
- twilio 2.11.1 版
- underscore 1.8.3 版
- uuid 3.0.0 版
- validator 6.1.0 版
- watson-developer-cloud 2.29.0 版
- when 3.7.7 版
- winston 2.3.0 版
- ws 1.1.1 版
- xml2js 0.4.17 版
- xmlhttprequest 1.8.0 版
- yauzl 2.7.0 版


## Python 運行環境
{: #openwhisk_ref_python_environments}

OpenWhisk 支援使用兩個不同的運行環境版本來執行 Python 動作。

### Python 3 動作

Python 3 動作是使用 Python 3.6.1 來執行。若要使用此運行環境，請在建立或更新動作時指定 `wsk` CLI 參數 `--kind python:3`。
除了 Python 3.6 標準程式庫之外，Python 動作還可以使用下列套件。

- aiohttp 1.3.3 版
- appdirs 1.4.3 版
- asn1crypto 0.21.1 版
- async-timeout 1.2.0 版
- attrs 16.3.0 版
- beautifulsoup4 4.5.1 版
- cffi 1.9.1 版
- chardet 2.3.0 版
- click 6.7 版
- cryptography 1.8.1 版
- cssselect 1.0.1 版
- Flask 0.12 版
- gevent 1.2.1 版
- greenlet 0.4.12 版
- httplib2 0.9.2 版
- idna 2.5 版
- itsdangerous 0.24 版
- Jinja2 2.9.5 版
- kafka-python 1.3.1 版
- lxml 3.6.4 版
- MarkupSafe 1.0 版
- multidict 2.1.4 版
- packaging 16.8 版
- parsel 1.1.0 版
- pyasn1 0.2.3 版
- pyasn1-modules 0.0.8 版
- pycparser 2.17 版
- PyDispatcher 2.0.5 版
- pyOpenSSL 16.2.0 版
- pyparsing 2.2.0 版
- python-dateutil 2.5.3 版
- queuelib 1.4.2 版
- requests 2.11.1 版
- Scrapy 1.1.2 版
- service-identity 16.0.0 版
- simplejson 3.8.2 版
- six 1.10.0 版
- Twisted 16.4.0 版
- w3lib 1.17.0 版
- Werkzeug 0.12 版
- yarl 0.9.8 版
- zope.interface 4.3.3 版

### Python 2 動作

Python 2 動作是使用 Python 2.7.12 來執行。除非您在建立或更新動作時指定 `--kind` 旗標，否則這是 Python 動作的預設運行環境。若要明確地選取此運行環境，請使用 `--kind python:2`。除了 Python 2.7 標準程式庫之外，Python 2 動作還可以使用下列套件。

- appdirs 1.4.3 版
- asn1crypto 0.21.1 版
- attrs 16.3.0 版
- beautifulsoup4 4.5.1 版
- cffi 1.9.1 版
- click 6.7 版
- cryptography 1.8.1 版
- cssselect 1.0.1 版
- enum34 1.1.6 版
- Flask 0.11.1 版
- gevent 1.1.2 版
- greenlet 0.4.12 版
- httplib2 0.9.2 版
- idna 2.5 版
- ipaddress 1.0.18 版
- itsdangerous 0.24 版
- Jinja2 2.9.5 版
- kafka-python 1.3.1 版
- lxml 3.6.4 版
- MarkupSafe 1.0 版
- packaging 16.8 版
- parsel 1.1.0 版
- pyasn1 0.2.3 版
- pyasn1-modules 0.0.8 版
- pycparser 2.17 版
- PyDispatcher 2.0.5 版
- pyOpenSSL 16.2.0 版
- pyparsing 2.2.0 版
- python-dateutil 2.5.3 版
- queuelib 1.4.2 版
- requests 2.11.1 版
- Scrapy 1.1.2 版
- service-identity 16.0.0 版
- simplejson 3.8.2 版
- six 1.10.0 版
- Twisted 16.4.0 版
- virtualenv 15.1.0 版
- w3lib 1.17.0 版
- Werkzeug 0.12 版
- zope.interface 4.3.3 版

## Docker 動作
{: #openwhisk_ref_docker}

Docker 動作是在 Docker 容器中執行使用者提供的二進位檔。二進位檔是在根據 [python:2.7.12-alpine](https://hub.docker.com/r/library/python) 的 Docker 映像檔中執行，因此二進位檔必須與此發行套件相容。

Docker 架構是建置 OpenWhisk 相容 Docker 映像檔的一種簡便方式。您可以使用 `wsk sdk install docker` CLI 指令來安裝架構。

主要二進位程式必須位在容器的 `/action/exec` 中。執行檔會透過可解除序列化為 `JSON` 物件的單一指令行引數字串來收到輸入引數。它必須透過 `stdout`，以已序列化 `JSON` 的單行字串形式來傳回結果。

透過修改 `dockerSkeleton` 中所含的 `Dockerfile`，即可包含任何編譯步驟或相依關係。

## REST API
{: #openwhisk_ref_restapi}

系統中的所有功能都可透過 REST API 來使用。其中有動作、觸發程式、規則、套件、啟動和名稱空間的集合和實體端點。

以下是集合端點：

- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/actions`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/triggers`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/rules`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/packages`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/activations`

`openwhisk.`<span class="keyword" data-hd-keyref="DomainName">DomainName</span> 是 OpenWhisk API 主機名稱（例如，openwhisk.ng.bluemix.net、172.17.0.1 等）。

針對 `{namespace}`，字元 `_` 可以用來指定使用者的 *預設名稱空間*（亦即，電子郵件位址）。

您可以在集合端點上執行 GET 要求，以提取集合中的實體清單。

每一種實體類型都有實體端點：

- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/actions/[{packageName}/]{actionName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/triggers/{triggerName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/rules/{ruleName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/packages/{packageName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/activations/{activationName}`


名稱空間和啟動端點僅支援 GET 要求。動作、觸發程式、規則和套件端點可支援 GET、PUT 及 DELETE 要求。動作、觸發程式和規則的端點也可支援 POST 要求（用來呼叫動作和觸發程式，以及啟用或停用規則）。如需詳細資料，請參閱 [API 參考資料](https://console.{DomainName}/apidocs/98)。

所有 API 都是透過 HTTP 基本鑑別進行保護。基本鑑別認證位於 `~/.wskprops` 檔案的 `AUTH` 內容中，以冒號區隔。您也可以在 [CLI 配置步驟](./index.html#openwhisk_start_configure_cli)中擷取這些認證。

下列範例說明如何使用 cURL 指令來取得 `whisk.system` 名稱空間中的所有套件清單：

```
curl -u USERNAME:PASSWORD https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/packages
```
{: pre}
```
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
    "version": "0.0.9",
    "namespace": "whisk.system"
  },
  ...
]
```
{: screen}

OpenWhisk API 支援 Web 用戶端發出的「要求/回應」呼叫。OpenWhisk 會以「跨原點資源共用」標頭來回應 `OPTIONS` 要求。目前可允許所有原點（亦即，Access-Control-Allow-Origin 為 "`*`"），而 Access-Control-Allow-Header 會產生 Authorization 和 Content-Type。

**注意：**因為 OpenWhisk 目前針對每個帳戶僅支援一個金鑰，因此不建議在簡單實驗之外使用 CORS。您的金鑰需要內嵌在用戶端程式碼中，以公開顯示。請謹慎使用。

## 系統限制
{: #openwhisk_syslimits}

### 動作
{{site.data.keyword.openwhisk_short}} 有一些系統限制，包括動作可使用的記憶體數量，以及每分鐘允許的動作呼叫次數。

下表列出動作的預設限制。

| 限制 | 說明 | 可配置 | 單位 | 預設值 |
| ----- | ----------- | ------------ | -----| ------- |
| timeout | 不容許容器的執行時間超過 N 毫秒 | 每個動作 |  毫秒 | 60000 |
| memory | 不容許容器配置超過 N MB 的記憶體 | 每個動作 | MB | 256 |
| logs | 不容許容器寫入 stdout 的內容超過 N MB | 每個動作 | MB | 10 |
| concurrent | 每個名稱空間的執行中或置入佇列等待執行的活動次數未提交超過 N 次 | 每個名稱空間 | 數字 | 1000 |
| minuteRate | 每個名稱空間每分鐘的活動次數未提交超過 N 次 | 每位使用者 | 數字 | 5000 |
| codeSize | 動作碼的大小上限 | 不可配置，每個動作的限制 | MB | 48 |
| parameters | 可附加的參數的大小上限 | 不可配置，每個動作/套件/觸發程式的限制 | MB | 1 |

### 每個動作逾時（毫秒）（預設值：60 秒）
{: #openwhisk_syslimits_timeout}
* 逾時限制 N 落在 [100 毫秒..300000 毫秒] 的範圍內，並且是針對每個動作設定（毫秒）。
* 使用者可以在建立動作時變更此限制。
* 終止執行時間超過 N 毫秒的容器。

### 每個動作記憶體 (MB)（預設值：256MB）
{: #openwhisk_syslimits_memory}
* 記憶體限制 M 落在 [128MB..512MB] 的範圍內，並且是針對每個動作設定 (MB)。
* 使用者可以在建立動作時變更此限制。
* 配置給容器的記憶體不能超過限制。

### 每個動作日誌 (MB)（預設值：10MB）
{: #openwhisk_syslimits_logs}
* 日誌限制 N 落在 [0MB..10MB] 的範圍內，並且是針對每個動作設定。
* 使用者可以在建立或更新動作時變更此限制。
* 會截斷超出所設定限制的日誌，並將警告新增為啟動的最後一個輸出，指出啟動已超出所設定的日誌限制。

### 每個動作構件 (MB)（固定：48MB）
{: #openwhisk_syslimits_artifact}
* 動作的程式碼大小上限為 48MB。
* 建議 JavaScript 動作使用工具，將所有原始碼（包括相依關係）連結成單一組合檔。

### 每個啟動有效負載大小 (MB)（固定：1MB）
{: #openwhisk_syslimits_activationsize}
* POST 內容大小，加上為動作呼叫或觸發程式發動而附帶的任何參數，上限為 1MB。

### 每個名稱空間同時呼叫（預設值：1000）
{: #openwhisk_syslimits_concur}
* 名稱空間的執行中或置入佇列等待執行的活動次數不能超過 1000。
* Whisk 可以在 consul kvstore 中靜態配置預設限制。
* 使用者目前無法變更限制。

### 每分鐘的呼叫次數（固定：5000）
{: #openwhisk_syslimits_invocations}
* 速率限制 N 設定為 5000，並限制一分鐘時間範圍內的動作呼叫次數。
* 使用者無法在建立動作時變更此限制。
* 超過此限制的 CLI 或 API 呼叫會收到與 HTTP 狀態碼 `429: TOO MANY REQUESTS` 對應的錯誤碼。

### 參數大小（固定：1MB）
{: #openwhisk_syslimits_parameters}
* 用於建立或更新動作/套件/觸發程式的參數的大小限制是 1MB。
* 使用者無法變更限制。
* 嘗試建立或更新參數太大的實體時，將會拒絕該實體。

### 每個 Docker 動作開啟檔案 ulimit（固定：64:64）
{: #openwhisk_syslimits_openulimit}
* 開啟檔案的數量上限為 64（同時適用於硬性和軟性限制）。
* docker run 指令使用引數 `--ulimit nofile=64:64`。
* 如需開啟檔案 ulimit 的相關資訊，請參閱 [docker run](https://docs.docker.com/engine/reference/commandline/run) 文件。

### 每個 Docker 動作程序 ulimit（固定：512:512）
{: #openwhisk_syslimits_proculimit}
* 可供使用者使用的程序數上限為 512（同時適用於硬性和軟性限制）。
* docker run 指令使用引數 `--ulimit nproc=512:512`。
* 如需程序數上限 ulimit 的相關資訊，請參閱 [docker run](https://docs.docker.com/engine/reference/commandline/run) 文件。

### 觸發程式

觸發程式受限於每分鐘的發動率，如下表所記載。

| 限制 | 說明 | 可配置 | 單位 | 預設值 |
| ----- | ----------- | ------------ | -----| ------- |
| minuteRate | 每個名稱空間每分鐘的觸發程式次數未發動超過 N 次 | 每位使用者 | 數字 | 5000 |

### 每分鐘的觸發程式數目（固定：5000）
* 速率限制 N 設定為 5000，並限制一分鐘時間範圍內可能發動的觸發程式數目。
* 使用者無法在建立觸發程式時變更此限制。
* 超過此限制的 CLI 或 API 呼叫會收到與 HTTP 狀態碼 `429: TOO MANY REQUESTS` 對應的錯誤碼。
