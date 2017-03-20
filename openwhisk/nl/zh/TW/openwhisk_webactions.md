---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Web 動作（實驗性）
{: #openwhisk_webactions}

Web 動作是標註成快速讓您建置 Web 型應用程式的 OpenWhisk 動作。這可讓您對後端邏輯進行程式設計，而 Web 應用程式可匿名存取該後端邏輯，而不需要 OpenWhisk 鑑別金鑰。由動作開發人員決定實作其擁有的所需鑑別及授權（即 OAuth 流程）。
{: shortdesc}

Web 動作啟動將與已建立動作的使用者相關聯。此動作會將來自呼叫者的動作啟動成本延遲到動作的擁有者。 

**附註**：此特性目前是實驗性供應項目，可讓使用者早期試用並提供意見。

讓我們採取下列 JavaScript 動作 `hello.js`：
```javascript
function main({name}) {
  var msg = 'you did not tell me who you are.';
  if (name) {
    msg = `hello ${name}!`
  }
  return {body: `<html><body><h3>${msg}</h3></body></html>`}
}
```
{: codeblock}

您可以使用註釋 `web-export`，在名稱空間 `guest` 的套件 `demo` 中建立 *web action* `hello`：
```
wsk package create demo
```
{: pre}
```
wsk action create /guest/demo/hello hello.js -a web-export true
```
{: pre}

`web-export` 註釋容許透過新的 REST 介面，將動作作為 Web 動作進行存取。URL 的結構如下：`https://{APIHOST}/api/v1/experimental/web/{QUALIFIED ACTION NAME}.{EXT}`。動作的完整名稱包含三個部分：名稱空間、套件名稱及動作名稱。範例為 `guest/demo/hello`。雖然如後面所述允許其他值，但是 URI 的最後一個部分稱為 `extension`（一般為 `.http`）。Web 動作 API 路徑可以與 `curl` 或 `wget` 搭配使用，而不需要 API 金鑰。它甚至可以直接輸入瀏覽器中。

請嘗試在 Web 瀏覽器中開啟 [https://${APIHOST}/api/v1/experimental/web/guest/demo/hello.http?name=Jane](https://${APIHOST}/api/v1/experimental/web/guest/demo/hello.http?name=Jane)。或者，嘗試透過 `curl` 呼叫動作：
```
curl https://openwhisk.{DomainName}/api/v1/experimental/web/guest/demo/hello.http?name=Jane
```
{: pre}
以下是執行 HTTP 重新導向的 Web 動作範例：
```javascript
function main() {
  return { 
    headers: { "location": "http://openwhisk.org" }, 
    code: 302 
  }
}
```
{: codeblock}

或者，設定 Cookie：
```javascript
function main() {
  return { 
    headers: { 
      "Set-Cookie": "UserID=Jane; Max-Age=3600; Version=",
      "Content-Type": "text/html"  
    }, 
    code: 200, 
    body: "<html><body><h3>hello</h3></body></html" }
}
```
{: codeblock}

或者，傳回 `image/png`：
```javascript
function main() {
    let png = <base 64 encoded string>
    return { headers: { 'Content-Type': 'image/png' },
             code: 200,
             body: png };
}
```
{: codeblock}

或者，傳回 `application/json`：
```javascript
function main(params) {
    return {
        'code': 200,
        'headers':{'Content-Type':'application/json'},
        'body' : new Buffer(JSON.stringify(params)).toString('base64'),
    };
}
```
{: codeblock}

重要的是要注意動作的[回應大小限制](./openwhisk_reference.html)，因為超出預先定義系統限制的回應將會失敗。例如，不應該透過 OpenWhisk 在行內傳送大型物件，而是延遲到物件儲存庫。

## 使用動作處理 HTTP 要求
{: #openwhisk_webactions_http}

不是 Web 動作的 OpenWhisk 動作需要鑑別，而且必須回應 JSON 物件。相對地，Web 動作可能是在未鑑別的情況下呼叫，而且可能用來實作回應不同類型的 *headers*、*status code* 及 *body* 內容的 HTTP 處理程式。Web 動作仍然必須傳回 JSON 物件，但是，如果 Web 動作的結果併入下列一個以上的項目作為最上層 JSON 內容，則 OpenWhisk 系統（即 `controller`）會以不同的方式處理 Web 動作：

- `headers`：索引鍵為標頭名稱且值為這些標頭的字串值的 JSON 物件（預設是無標頭）。
- `code`：有效的 HTTP 狀態碼（預設值為 200 OK）。
- `body`：為純文字或 Base 64 編碼字串（適用於二進位資料）的字串。

終止要求/回應時，控制器會將動作指定的標頭（如果有的話）傳遞給 HTTP 用戶端。同樣地，控制器將回應現有的給定狀態碼。最後，body 會作為回應的主體傳遞。除非在動作結果的 `headers` 中宣告 `content-type header`，否則會將 body 視為字串一樣傳遞（或者會導致錯誤）。定義 `content-type` 時，控制器將判斷回應是二進位資料還是純文字，並視需要使用 Base 64 解碼器來解碼字串。如果無法正確地解碼 body，則會將錯誤傳回給呼叫者。

*附註*：JSON 物件或陣列被視為二進位資料，而且必須是如上面範例所編碼的 base64。

## HTTP 環境定義

Web 動作在呼叫時會接收可作為動作輸入引數的其他參數的所有 HTTP 要求資訊。它們包含：

- `__ow_meta_verb`：要求的 HTTP 方法。
- `__ow_meta_headers`：要求標頭。
- `__ow_meta_path`：要求的不相符路徑（比對會在使用動作延伸之後停止）。

要求可能不會置換上面的任何具名 `__ow_` 參數；這麼做會導致失敗要求，其狀態等於「400 不正確的要求」。

## 其他特性
{: #openwhisk_webactions_extra}

Web 動作具備一些其他特性，包括：

- `內容延伸`：要求必須將其所需的內容類型指定為下列其中一項：`.json`、`.html`、`.text` 或 `.http`。作法是將延伸新增至 URI 中的動作名稱，因此動作 `/guest/demo/hello` 參照為 `/guest/demo/hello.http`（舉例來說），以接收傳回的 HTTP 回應。
- `投射結果中的欄位`：接在動作名稱後面的路徑是用來投射回應的一個以上層次。例如，`/guest/demo/hello.html/body`。這可讓傳回字典 `{body: "..." }` 的動作投射 `body` 內容，並且改為直接傳回其字串值。投射路徑遵循絕對路徑模型（如 XPath）。
- `作為輸入的查詢及主體參數`：動作會接收查詢參數，以及要求主體中的參數。參數的合併優先順序是：套件參數、動作參數、查詢參數、主體參數，而且所有這些項目都會在重疊時覆寫任何先前的值。舉例來說，`/guest/demo/hello.http?name=Jane` 會將引數 `{name: "Jane"}` 傳遞給動作。
- `表單資料`：除了標準 `application/json` 之外，Web 動作還可能會將透過資料 `application/x-www-form-urlencoded data` 編碼的 URL 接收作為輸入。
- `透過多個 HTTP 動詞啟動`：可能會透過四種 HTTP 方法的其中一種來呼叫 Web 動作：`GET`、`POST`、`PUT` 或 `DELETE`。


下面範例簡短概述如何在 Web 動作中使用這些特性。如果動作 `/guest/demo/hello` 具有下列主體：
```javascript
function main(params) { 
    return { 'response': params};
}
```
{: codeblock}

並且使用查詢參數 `name` 來呼叫動作、使用 `.json` 延伸來指出 JSON 回應，以及投射欄位 `/response`，則會產生下列 HTTP 回應：
```
curl https://openwhisk.{DomainName}/api/v1/experimental/web/guest/demo/hello.json/response?name=Jane
```
{: pre}
```json
{
    "name": "Jane",
    "__ow_meta_verb": "get",
    "__ow_meta_headers": {
        "accept": "*/*",
        "user-agent": "curl/7.51.0"
    },
    "__ow_meta_path": "/response"
}
```

## 內容延伸
{: #openwhisk_webactions_extensions}

呼叫 Web 動作時，需要內容延伸。`.json` 及 `.http` 延伸不需要投射路徑。`.text` 及 `.html` 延伸則需要，不過，基於便利性，假設預設路徑符合延伸名稱。因此，若要呼叫 Web 動作並接收 `.html` 回應，動作必須回應包含稱為 `html` 的最上層內容的 JSON 物件（或者回應必須位於明確給定路徑中）。換言之，`/guest/demo/hello.html` 相當於明確地投射 `html` 內容，如 `/guest/demo/hello.html/html`。動作的完整名稱必須包括其套件名稱，如果動作不在具名套件中，其為 `default`。


## 受保護的參數
{: #openwhisk_webactions_protected}

動作參數也可能受到保護並視為不可變。若要終結參數，以及將動作 Web 設為可存取，則必須將兩個[註釋](/openwhisk_annotations.html)附加至動作：必須將 `final` 和 `web-export` 其中一個設為 `true` 才會作用。透過先前重新造訪動作部署，我們如下新增註釋：

```
wsk action create /guest/demo/hello hello.js \
      --parameter name Jane \
      --annotation final true \
      --annotation web-export true
```
{: pre}

這些變更的結果為 `name` 已連結至 `Jane`，而且可能不會因 final 註釋而置換為查詢或主體參數。這樣可保護對意外或有意嘗試變更此值的查詢或主體參數所執行的動作。 

## 停用 Web 動作
{: #openwhisk_webactions_disable}

若要停用透過新 API 呼叫 Web 動作 (`https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/experimental/web/`)，則移除註釋或將它設為 `false` 即可。

```
wsk action update /guest/demo/hello hello.js \
      --annotation web-export false
```
{: pre}     

## 錯誤處理
{: #openwhisk_webactions_errors}

OpenWhisk 動作失敗時，有兩種不同的失敗模式。第一個稱為*應用程式錯誤*，類似於捕捉的異常狀況：此動作會傳回包含最上層 `error` 內容的 JSON 物件。第二個是動作災難性地失敗並且未產生回應時所發生的*開發人員錯誤*（這類似於未捕捉的異常狀況）。對於 Web 動作，控制器會如下處理應用程式錯誤：

- 忽略所有指定的路徑投射，控制器會改為投射 `error` 內容。
- 控制器會將依動作延伸所示的內容處理套用至 `error` 內容的值。

開發人員應該注意 Web 動作的使用方式，以及如何相應地產生錯誤回應。例如，與 `.http` 延伸搭配使用的 Web 動作應該會傳回 HTTP 回應，例如：`{error: { code: 400 }`。無法這麼做時，將會導致延伸中所示的 content-type 與錯誤回應中的動作 content-type 不符。必須對具有序列的 Web 動作進行特殊考量，因此構成序列的元件可以在必要時產生足夠的錯誤。
