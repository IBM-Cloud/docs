---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Web 動作
{: #openwhisk_webactions}

Web 動作是標註成快速讓您建置 Web 型應用程式的 OpenWhisk 動作。這可讓您對後端邏輯進行程式設計，而 Web 應用程式可匿名存取該後端邏輯，而不需要 OpenWhisk 鑑別金鑰。由動作開發人員決定實作其擁有的所需鑑別及授權（即 OAuth 流程）。
{: shortdesc}

Web 動作啟動將與已建立動作的使用者相關聯。此動作會將來自呼叫者的動作啟動成本延遲到動作的擁有者。

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

您可以搭配使用 CLI 的 `--web` 旗標與 `true` 或 `yes` 值，在名稱空間 `guest` 的套件 `demo` 中建立 *Web 動作* `hello`：
```
wsk package create demo
```
{: pre}
```
wsk action create /guest/demo/hello hello.js --web true
```
{: pre}

搭配使用 `--web` 旗標與 `true` 或 `yes` 值，容許透過 REST 介面存取動作，而不需要使用認證。您可以使用結構如下的 URL 來呼叫 Web 動作：`https://{APIHOST}/api/v1/web/{QUALIFIED ACTION NAME}.{EXT}`。動作的完整名稱包含三個部分：名稱空間、套件名稱及動作名稱。

*動作的完整名稱必須包括其套件名稱，如果動作不在具名套件中，則為 `default`。*

範例為 `guest/demo/hello`。雖然如後面所述允許其他值，但是 URI 的最後一個部分稱為 `extension`（一般為 `.http`）。Web 動作 API 路徑可以與 `curl` 或 `wget` 搭配使用，而不需要 API 金鑰。它甚至可以直接輸入瀏覽器中。

請嘗試在 Web 瀏覽器中開啟 [https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.http?name=Jane](https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.http?name=Jane)。或者，嘗試透過 `curl` 呼叫動作：
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.http?name=Jane
```
{: pre}

以下是執行 HTTP 重新導向的 Web 動作範例：

```javascript
function main() {
  return { 
    headers: { location: 'http://openwhisk.org' },
    statusCode: 302
  }
}
```
{: codeblock}    

或者，設定 Cookie：
```javascript
function main() {
  return { 
    headers: { 
      'Set-Cookie': 'UserID=Jane; Max-Age=3600; Version=',
      'Content-Type': 'text/html'
    }, 
    statusCode: 200,
    body: '<html><body><h3>hello</h3></body></html>' }
}
```
{: codeblock}  

或者，傳回 `image/png`：
```javascript
function main() {
    let png = <base 64 encoded string>
    return { headers: { 'Content-Type': 'image/png' },
             statusCode: 200,
             body: png };
}
```
{: codeblock}  

或者，傳回 `application/json`：
```javascript
function main(params) {
    return {
        statusCode: 200,
        headers: { 'Content-Type': 'application/json' },
        body: new Buffer(JSON.stringify(params)).toString('base64'),
    };
}
```
{: codeblock}  

請務必注意動作的[回應大小限制](./openwhisk_reference.html)，因為如果回應超出預先定義的系統限制將會失敗。例如，不應該透過 OpenWhisk 在行內傳送大型物件，而是延遲到物件儲存庫。

## 使用動作處理 HTTP 要求
{: #openwhisk_webactions_http}

不是 Web 動作的 OpenWhisk 動作需要鑑別，而且必須回應 JSON 物件。相反地，Web 動作可能是在未鑑別的情況下呼叫，而且可能用來實作回應不同類型的 *headers*、*statusCode* 及 *body* 內容的 HTTP 處理程式。Web 動作仍然必須傳回 JSON 物件，但是，如果 Web 動作的結果併入下列一個以上的項目作為最上層 JSON 內容，則 OpenWhisk 系統（即 `controller`）會以不同的方式處理 Web 動作：

- `headers`：索引鍵為標頭名稱且值為這些標頭的字串值的 JSON 物件（預設是無標頭）。
- `statusCode`：有效的 HTTP 狀態碼（預設值為 200 OK）。
- `body`：為純文字或 Base 64 編碼字串（適用於二進位資料）的字串。

終止要求/回應時，控制器會將動作指定的標頭（如果有的話）傳遞給 HTTP 用戶端。同樣地，控制器將回應現有的給定狀態碼。最後，body 會作為回應的內文傳遞。除非在動作結果的 `headers` 中宣告 `content-type header`，否則會將 body 視為字串一樣傳遞（或者會導致錯誤）。定義 `content-type` 時，控制器將判斷回應是二進位資料還是純文字，並視需要使用 Base 64 解碼器來解碼字串。如果無法正確地解碼 body，則會將錯誤傳回給呼叫者。

*附註*：JSON 物件或陣列被視為二進位資料，而且必須是如上面範例所編碼的 base64。

## HTTP 環境定義

所有 Web 動作在呼叫後都會以動作輸入引數參數的方式，接收其他 HTTP 要求明細。它們包含：

- `__ow_method`（類型：字串）：要求的 HTTP 方法。
- `__ow_headers`（類型：將字串對映至字串）：要求標頭。
- `__ow_path`（類型：字串）：要求的不相符路徑（比對會在使用動作延伸之後停止）。
- `__ow_user`（類型：字串）：識別 OpenWhisk 鑑別主旨的名稱空間
- `__ow_body`（類型：字串）：要求內文實體，當內容為二進位時，為 base64 編碼的字串，否則為一般字串
- `__ow_query`（類型：字串）：要求中的查詢參數，為未剖析的字串

要求可能不會置換上述任何具名 `__ow_` 參數；這麼做會導致要求失敗，其狀態等於「400 不正確的要求」。

只有在 Web 動作[標註為需要鑑別](./openwhisk_annotations.html#openwhisk_annotations_webactions)，並允許 Web 動作實作自己的授權原則時，`__ow_user` 才會存在。只有在 Web 動作選擇要處理[「原始」HTTP 要求](#raw-http-handling)時，才能使用 `__ow_query`。這是一個字串，其中包含從 URI 剖析的查詢參數（以 `&` 區隔）。在處理「原始」HTTP 要求時，或是當 HTTP 要求實體不是 JSON 物件或表單資料時，`__ow_body` 內容會存在。否則，Web 動作會接收查詢和內文參數，以作為動作引數的第一級內容，內文參數優先於查詢參數，而查詢參數優先於動作和套件參數。

## 其他特性

Web 動作具備一些其他特性，包括：

- `內容副檔名`：要求必須將其所需的內容類型指定為下列其中一項：`.json`、`.html`、`.http`、`.svg` 或 `.text`。作法是將副檔名新增至 URI 中的動作名稱，因此動作 `/guest/demo/hello` 參照為 `/guest/demo/hello.http`（舉例來說），以接收傳回的 HTTP 回應。為了方便起見，如果未偵測到副檔名，則假設為 `.http` 副檔名。
- `投射結果中的欄位`：接在動作名稱後面的路徑是用來投射回應的一個以上層次。例如，`/guest/demo/hello.html/body`。這可讓傳回字典 `{body: "..." }` 的動作投射 `body` 內容，並且改為直接傳回其字串值。投射路徑遵循絕對路徑模型（如 XPath）。
- `作為輸入的查詢及內文參數`：動作會接收查詢參數，以及要求內文中的參數。參數的合併優先順序是：套件參數、動作參數、查詢參數、內文參數，而且所有這些項目都會在重疊時覆寫任何先前的值。舉例來說，`/guest/demo/hello.http?name=Jane` 會將引數 `{name: "Jane"}` 傳遞給動作。
- `表單資料`：除了標準 `application/json` 之外，Web 動作還可能會將透過資料 `application/x-www-form-urlencoded data` 編碼的 URL 接收作為輸入。
- `透過多個 HTTP 動詞啟動`：Web 動作可以透過下列任何 HTTP 方法來呼叫：`GET`、`POST`、`PUT`、`PATCH` 和 `DELETE`，以及 `HEAD` 和 `OPTIONS`。
- `非 JSON 內文和原始 HTTP 實體處理`：Web 動作可以接受 JSON 物件以外的 HTTP 要求內文，並可選擇一律接收這類值作為不透明值（非二進位時為純文字，否則為 base64 編碼字串）。

下面範例簡短概述如何在 Web 動作中使用這些特性。請考量具有下列內文的動作 `/guest/demo/hello`：
```javascript
function main(params) { 
    return { response: params };
}
```

將此動作當作 Web 動作呼叫時，您可以從結果投射不同的路徑，以變更 Web 動作的回應。例如，若要傳回整個物件，並查看動作收到哪些引數：

```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json
```
{: pre}
```json
{
  "response": {
    "__ow_method": "get",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

並使用查詢參數：
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json?name=Jane
```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "get",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

或表單資料：
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -d "name":"Jane"
```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "10",      
      "content-type": "application/x-www-form-urlencoded",      
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

或 JSON 物件：
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -H 'Content-Type: application/json' -d '{"name":"Jane"}'
```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "15",      
      "content-type": "application/json",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

並且只投射名稱（以文字形式）：
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.text/response/name?name=Jane
```
{: pre}
```
Jane
```

從上面可以看到，為了方便，查詢參數、表單資料和 JSON 物件內文實體全都被當作字典來處理，並且可以直接存取其值作為動作輸入內容。但是選擇以較直接的方式來處理 HTTP 要求實體的 Web 動作，或是當 Web 動作接收不是 JSON 物件的實體時，就不是這樣了。

以下範例是使用 "text" content-type 來搭配上述相同的範例：
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -H 'Content-Type: text/plain' -d "Jane"
```
{: pre}
```json
{
  "response": {
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "4",      
      "content-type": "text/plain",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": "",
    "__ow_body": "Jane"
  }
}
```


## 內容副檔名
{: #openwhisk_webactions_extensions}

在呼叫 Web 動作時，通常會需要內容副檔名；若沒有副檔名，則會假設 `.http` 為預設值。`.json` 及 `.http` 副檔名不需要投射路徑。`.html`、`.svg` 及 `.text` 副檔名則需要，不過，為方便起見，會假設預設路徑符合副檔名。因此，若要呼叫 Web 動作並接收 `.html` 回應，動作必須回應包含稱為 `html` 的最上層內容的 JSON 物件（或者回應必須位於明確給定路徑中）。換言之，`/guest/demo/hello.html` 相當於明確地投射 `html` 內容，如 `/guest/demo/hello.html/html`。動作的完整名稱必須包括其套件名稱，如果動作不在具名套件中，其為 `default`。


## 受保護的參數
{: #openwhisk_webactions_protected}

在呼叫 Web 動作時，通常會需要內容副檔名；若沒有副檔名，則會假設 `.http` 為預設值。`.json` 及 `.http` 副檔名不需要投射路徑。`.html`、`.svg` 及 `.text` 副檔名則需要，不過，為方便起見，會假設預設路徑符合副檔名。因此，若要呼叫 Web 動作並接收 `.html` 回應，動作必須回應包含稱為 `html` 的最上層內容的 JSON 物件（或者回應必須位於明確給定路徑中）。換言之，`/guest/demo/hello.html` 相當於明確地投射 `html` 內容，如 `/guest/demo/hello.html/html`。動作的完整名稱必須包括其套件名稱，如果動作不在具名套件中，其為 `default`。


## 受保護的參數

動作參數也會受到保護並視為不可變。啟用 Web 動作時，會自動完成參數。

```
 wsk action create /guest/demo/hello hello.js \
      --parameter name Jane \
      --web true
```

這些變更的結果為 `name` 已連結至 `Jane`，而且可能不會因 final 註釋而置換為查詢或內文參數。這樣可保護對意外或有意嘗試變更此值的查詢或內文參數所執行的動作。 

## 停用 Web 動作

若要停用透過 Web API (`https://openwhisk.ng.bluemix.net/api/v1/web/`) 呼叫 Web 動作，請在使用 CLI 更新動作時，將 `false` 或 `no` 值傳遞給 `--web` 旗標。

```
 wsk action update /guest/demo/hello hello.js --web false
```
{: pre}

## 原始 HTTP 處理

Web 動作可以選擇直接解譯及處理送入的 HTTP 內文，而不需將 JSON 物件提升至可用於動作輸入的第一級內容（例如，`args.name` 與剖析 `args.__ow_query`）。透過 `raw-http` [註釋](annotations.md)即可完成此作業。使用與前面相同的範例，但現在是作為「原始」HTTP Web 動作，接收 `name` 同時作為查詢參數以及 HTTP 要求內文中的 JSON 值：
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json?name=Jane -X POST -H "Content-Type: application/json" -d '{"name":"Jane"}'
```
{: pre}
```json
{
    "response": {
    "__ow_method": "post",
    "__ow_query": "name=Jane",
    "__ow_body": "eyJuYW1lIjoiSmFuZSJ9",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "15",
      "content-type": "application/json",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"      
    },
    "__ow_path": ""
  }
}
```

請注意，在此情況下，JSON 內容為 base64 編碼，因為它被當成二進位值來處理。該動作必須對此值進行 base64 解碼和 JSON 剖析，以回復 JSON 物件。OpenWhisk 會使用 [Spray](https://github.com/spray/spray) 架構來[判斷](https://github.com/spray/spray/blob/master/spray-http/src/main/scala/spray/http/MediaType.scala#L282)哪些內容類型是二進位，哪些是純文字。


### 啟用原始 HTTP 處理

若要啟用原始 HTTP Web 動作，可以搭配使用 `--web` 旗標與 `raw` 值。

```
 wsk action create /guest/demo/hello hello.js --web raw
```

### 停用原始 HTTP 處理

將 `false` 或 `no` 值傳遞給 `--web` 旗標，即可停用原始 HTTP。

```
 wsk update create /guest/demo/hello hello.js --web false
```

### 從 Base64 解碼二進位主體內容

使用原始 HTTP 處理時，若要求 content-type 是二進位，將會以 Base64 編碼 `__ow_body` 內容。
下面函數示範如何解碼 Node、Python 及 Swift 中的主體內容。只需要將下面所顯示的方法儲存至檔案、建立利用所儲存構件的原始 HTTP Web 動作，然後呼叫 Web 動作即可。

#### Node

```javascript
  function main(args) {
       decoded = new Buffer(args.__ow_body, 'base64').toString('utf-8')
    return {body: decoded}
}
```
{: codeblock}

#### Python

```python
def main(args):
    try:
        decoded = args['__ow_body'].decode('base64').strip()
        return {"body": decoded}
    except:
        return {"body": "Could not decode body from Base64."}
```
{: codeblock}

#### Swift

```swift
extension String {
    func base64Decode() -> String? {
        guard let data = Data(base64Encoded: self) else {
            return nil
        }

        return String(data: data, encoding: .utf8)
    }
}

func main(args: [String:Any]) -> [String:Any] {
    if let body = args["__ow_body"] as? String {
        if let decoded = body.base64Decode() {
            return [ "body" : decoded ]
        }
    }

    return ["body": "Could not decode body from Base64."]
}
```
{: codeblock}

例如，將 Node 函數儲存為 `decode.js`，然後執行下列指令：
```
 wsk action create decode decode.js --web raw
```
{: pre}
```
ok: created action decode
```
```
curl -k -H "content-type: application" -X POST -d "Decoded body" https:// openwhisk.ng.bluemix.net/api/v1/web/guest/default/decodeNode.json
```
{: pre}
```json
{
  "body": "Decoded body"
}
```

## 錯誤處理
{: #openwhisk_webactions_errors}

OpenWhisk 動作失敗時，有兩種不同的失敗模式。第一個稱為*應用程式錯誤*，類似於捕捉的異常狀況：此動作會傳回包含最上層 `error` 內容的 JSON 物件。第二個是動作災難性地失敗並且未產生回應時所發生的*開發人員錯誤*（這類似於未捕捉的異常狀況）。對於 Web 動作，控制器會如下處理應用程式錯誤：

- 忽略所有指定的路徑投射，控制器會改為投射 `error` 內容。
- 控制器會將依動作副檔名所暗示的內容處理套用至 `error` 內容的值。

開發人員應該注意 Web 動作的使用方式，以及如何相應地產生錯誤回應。例如，與 `.http` 副檔名搭配使用的 Web 動作應該會傳回 HTTP 回應，例如：`{error: { statusCode: 400 }`。無法這麼做時，將會導致副檔名中所暗示的 content-type 與錯誤回應中的動作 content-type 不符。必須對具有序列的 Web 動作進行特殊考量，因此構成序列的元件可以在必要時產生足夠的錯誤。

