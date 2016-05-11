---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 建立及呼叫 {{site.data.keyword.openwhisk_short}} 動作
{: #openwhisk_actions}

*前次更新：2016 年 3 月 22 日*

動作是在 {{site.data.keyword.openwhisk}} 平台上執行的無狀態程式碼 Snippet。動作可以是 JavaScript 函數、Swift 函數，或包裝在 Docker 儲存器中的自訂可執行程式。例如，動作可以用來偵測映像檔中的樣式、聚集一組 API 呼叫，或張貼推文。
{:shortdesc}

可以明確地呼叫動作，或為回應某事件而執行動作。在任一情況下，執行動作都會根據唯一啟動 ID 來識別啟動記錄。動作的輸入及動作的結果是鍵值組的定義檔，其中索引鍵是字串，而值是有效的 JSON 值。

動作是由其他動作的呼叫或定義的一連串動作所組成。

## 建立及呼叫 JavaScript 動作
{: #openwhisk_create_action_js}

下列各節會引導您透過 JavaScript 逐步執行動作。從建立及呼叫簡單動作開始，接著將參數新增至動作並使用參數來呼叫該動作、設定並呼叫預設參數、建立非同步動作，最後是使用動作序列。


### 建立及呼叫簡單 JavaScript 動作
{: #openwhisk_single_action_js}

請檢閱下列步驟及範例，以建立您的第一個 JavaScript 動作。

1. 建立含有下列內容的 JavaScript 檔。在此範例中，檔名是 'hello.js'。
  
  ```
  function main() {
      return {payload: 'Hello world'};
  }
  ```
  {: codeblock}

  JavaScript 檔可能包含其他函數。不過，依慣例，必須要有稱為 `main` 的函數，以提供動作的進入點。

2. 從下列 JavaScript 函數建立動作。在此範例中，動作稱為 'hello'。

  ```
  wsk action create hello hello.js
  ```
  {: pre}
  ```
  ok: created action hello
  ```
  {: screen}

3. 列出您已建立的動作：
  
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  hello       private
  ```
  {: screen}

  您可以看到剛剛建立的 `hello` 動作。

4. 建立動作之後，即可使用 'invoke' 指令透過 {{site.data.keyword.openwhisk_short}} 在雲端執行它。在指令中指定旗標，即可透過*封鎖* 呼叫或*非封鎖* 呼叫來呼叫動作。封鎖呼叫會等待動作執行完成並傳回結果。這個範例使用封鎖參數 `-blocking`：

  ```
  wsk action invoke --blocking hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 44794bd6aab74415b4e42a308d880e5b
  response:
  {
      "result": {
          "payload": "Hello world"
      },
      "status": "success",
      "success": true
  }
  ```
  {: screen}

  此指令輸出兩個重要的資訊部分：
  * 啟動 ID (`44794bd6aab74415b4e42a308d880e5b`)
  * 呼叫結果

  在此情況下，結果是 JavaScript 函數所傳回的 `Hello world` 字串。啟動 ID 之後可以用來擷取日誌或呼叫結果。  

5. 如果您不是立即需要動作結果，則可以省略 `--blocking` 旗標，以進行非封鎖呼叫。您稍後可以透過使用啟動 ID 來取得結果。請參閱下列範例：

  ```
  wsk action invoke hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: screen}

  ```
  wsk activation result 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: pre}
  ```
  {
      "payload": "Hello world"
  }
  ```
  {: screen}

6. 如果您忘記記錄啟動 ID，則可以取得從最近到最舊排列的啟動清單。執行下列指令，以取得啟動的清單：

  ```
  wsk activation list
  ```
  {: pre}
  ```
  activations
  44794bd6aab74415b4e42a308d880e5b         hello
  6bf1f670ee614a7eb5af3c9fde813043         hello
  ```
  {: screen}

### 將參數傳遞給動作
{: #openwhisk_adding_parameters_js}

呼叫動作時，可以將參數傳遞給動作。

1. 在動作中使用參數。例如，使用下列內容來更新 'hello.js' 檔：
  
  ```
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

  輸入參數被當作 `main` 函數的 JSON 物件參數來傳遞。請注意，在此範例中，`name` 及 `place` 參數擷取自 `params` 物件的方式。

2. 更新 `hello` 動作並呼叫動作，同時將 `name` 及 `place` 參數值傳遞給它。請參閱下列範例：
  
  ```
  wsk action update hello hello.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result hello --param name 'Bernie' --param place 'Vermont'
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  {: screen}

  請注意，`--param` 選項用來指定參數名稱及值，而 `--result` 選項用來只顯示呼叫結果。

### 設定預設參數
{: #openwhisk_binding_actions}

您可以使用多個具名參數來呼叫動作。請記住，前一個範例中的 `hello` 動作預期會有兩個參數：人員的名稱 (*name*) 及其所在位置 (*place*)。

您可以連結特定參數，而非每次都將所有參數傳遞給動作。下列範例會連結 *place* 參數，以將動作預設為 "Vermont" 這個位置：
 
1. 使用 `--param` 選項來連結參數值，以更新動作。

  ```
  wsk action update hello --param place 'Vermont'
  ```
  {: pre}

2. 呼叫動作，但這次只傳遞 `name` 參數。

  ```
  wsk action invoke --blocking --result hello --param name 'Bernie'
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  {: screen}

  請注意，呼叫動作時，您不需要指定 place 參數。在呼叫時指定參數值，仍然可以改寫連結的參數。

3. 呼叫動作，並傳遞 `name` 及 `place` 值。後者會改寫連結至動作的值。

  ```
  wsk action invoke --blocking --result hello --param name 'Bernie' --param place 'Washington, DC'
  ```
  {: pre}
  ```
  {  
      "payload": "Hello, Bernie from Washington, DC"
  }
  ```
  {: screen}

### 建立非同步動作
{: #openwhisk_asynchrony_js}

傳回 `main` 函數之後，在回呼函數中繼續執行的 JavaScript 函數可能需要傳回啟動結果。這項作業的完成方式是在動作中使用 `whisk.async()` 及 `whisk.done()` 函數。

1. 將下列內容儲存至稱為 `asyncAction.js` 的檔案中。

  ```
  function main() {
      setTimeout(function() {
          return whisk.done({done: true});
      }, 20000);
      return whisk.async();
  }
  ```
  {: codeblock}

  請注意，會立即傳回 `main` 函數，而 `whisk.async()` 回覆值指出此啟動應該繼續執行。

  在此情況下，`setTimeout()` JavaScript 函數會先等待 20 秒，再呼叫回呼函數，其中，`whisk.done()` 呼叫指出啟動已完成。

2. 執行下列指令，以建立並呼叫動作：

  ```
  wsk action create asyncAction asyncAction.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result asyncAction
  ```
  {: pre}
  ```
  {
      "done": true
  }
  ```
  {: screen}

  請注意，您已執行非同步動作的封鎖呼叫。

3. 提取啟動日誌，來查看啟動需要多久時間才能完成：

  ```
  wsk activation list --limit 1 asyncAction
  ```
  {: pre}
  ```
  activations
  b066ca51e68c4d3382df2d8033265db0             asyncAction
  ```
  {: screen}


  ```
  wsk activation get b066ca51e68c4d3382df2d8033265db0
  ```
  {: pre}
 ```
  {
      "start": 1455881628103,
      "end":   1455881648126,
      ...
  }
  ```
  {: screen}

  比較啟動記錄中的 `start` 與 `end` 時間戳記，您可以發現完成此啟動所需的時間略高於 20 秒。


### 使用動作來呼叫外部 API
{: #openwhisk_apicall_action}

到目前為止，這些範例已自行包含 JavaScript 函數。您也可以建立呼叫外部 API 的動作。

此範例會呼叫 Yahoo Weather 服務，以取得特定位置的現行狀況。 

1. 將下列內容儲存至稱為 `weather.js` 的檔案中。
  ```
    var request = require('request');
    
    function main(msg) {
        var location = msg.location || 'Vermont';
        var url = 'https://query.yahooapis.com/v1/public/yql?q=select item.condition from weather.forecast where woeid in (select woeid from geo.places(1) where text="' + location + '")&format=json';
    
        request.get(url, function(error, response, body) {
            var condition = JSON.parse(body).query.results.channel.item.condition;
            var text = condition.text;
            var temperature = condition.temp;
            var output = 'It is ' + temperature + ' degrees in ' + location + ' and ' + text;
            whisk.done({msg: output});
        });
    
        return whisk.async();
    }
  ```
  {: codeblock}

  請注意，此範例中的動作使用 JavaScript `request` 程式庫，對 Yahoo Weather API 發出 HTTP 要求，以及從 JSON 結果中擷取欄位。[參照](./openwhisk_reference.html#runtime_ref_runtime_environment)詳述可在動作中使用的 Node.js 套件。
  
  此範例也會顯示需要非同步動作。此動作會傳回 `whisk.async()`，指出傳回該函數時還無法使用這個動作的結果。而是，在完成 HTTP 呼叫之後，可以在 `request` 回呼中取得結果，並將它當作 `whisk.done()` 函數的引數來傳遞。

2. 執行下列指令，以建立並呼叫動作：
  ```
  wsk action create weather weather.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result weather --param location 'Brooklyn, NY'
  ```
  {: pre}
  ```
  {
      "msg": "It is 28 degrees in Brooklyn, NY and Cloudy"
  }
  ```
  {: screen}

### 建立動作序列
{: #openwhisk_create_action_sequence}

您可以建立一個動作，以將一連串的動作鏈結在一起。

在稱為 `/whisk.system/util` 的套件中提供數個公用程式動作，可用來建立第一個序列。您可以在[套件](./openwhisk_packages.html)小節中進一步瞭解套件。

1. 顯示 `/whisk.system/util` 套件中的動作。
  
  ```
  wsk package get --summary /whisk.system/util
  ```
  {: pre}
  ```
  package /whisk.system/util
   action /whisk.system/util/cat: Concatenate array of strings, and split lines into an array
   action /whisk.system/util/head: Filter first K array elements and discard rest
   action /whisk.system/util/date: Get current date and time
   action /whisk.system/util/sort: Sort array
  ```
  {: screen}

  在此範例中，您將使用 `cat` 及 `sort` 動作。

2. 建立動作序列，以將某個動作的結果當作下一個動作的引數來傳遞。
  
  ```
  wsk action create myAction --sequence /whisk.system/util/cat,/whisk.system/util/sort
  ```
  {: pre}

  此動作序列會將數行文字轉換成一個陣列，並排序這些行。

3. 在呼叫動作序列之前，請建立稱為 'haiku.txt' 且包含數行文字的文字檔：

  ```
  Over-ripe sushi,
  The Master
  Is full of regret.
  ```
  {: codeblock}

4. 呼叫動作：
  
  ```
  wsk action invoke --blocking --result myAction --param payload "$(cat haiku.txt)"
  ```
  {: pre}
  ```
  {
      "length": 3,
      "lines": [
          "Is full of regret.",
          "Over-ripe sushi,",
          "The Master"
      ]
  }
  ```
  {: screen}

  在結果中，會排序這些行。

**附註**：如需使用多個具名參數來呼叫動作序列的相關資訊，請參閱[設定預設參數](./openwhisk_actions.html##openwhisk_binding_actions)。

## 建立 Swift 動作
{: #openwhisk_actions_swift}

建立 Swift 動作的程序，與建立 JavaScript 動作的程序類似。下列各節會引導您建立及呼叫單一 Swift 動作，以及將參數新增至該動作。

您也可以使用線上 [Swift 沙盤推演](https://swiftlang.ng.bluemix.net)來測試 Swift 程式碼，而不需要在機器上安裝 Xcode。

### 建立及呼叫動作
{: #openwhisk_actions_invoke_swift}

動作只是最上層 Swift 函數。例如，建立稱為 `hello.swift` 且含有下列內容的檔案：

```
  func main(args: [String:Any]) -> [String:Any] {
      if let name = args["name"] as? String {
          return [ "greeting" : "Hello \(name)!" ]
      } else {
return [ "greeting" : "Hello stranger!" ]
      }
  }
```
{: codeblock}

請注意，Swift 動作就像 JavaScript 動作一樣，一律會使用定義檔，並產生定義檔。

您可以從此函數建立稱為 `helloSwift` 的 {{site.data.keyword.openwhisk_short}} 動作，如下所示：

```
wsk action create helloSwift hello.swift
```
{: pre}

使用指令行及 `.swift` 原始檔時，不需要指定是在建立 Swift 動作（相對於 JavaScript 動作）；工具是透過副檔名來判斷。

Swift 動作與 JavaScript 動作的動作呼叫相同：

```
wsk action invoke --blocking --result helloSwift --param name World
```
{: pre}

```
  {
      "greeting": "Hello World!"
  }
```
{: screen}

**注意：**Swift 動作是在 Linux 環境中執行。Swift on Linux 仍在開發中，而且 {{site.data.keyword.openwhisk_short}} 通常會使用最新的可用版本，但此版本不一定是穩定的。此外，與 {{site.data.keyword.openwhisk_short}} 搭配使用的 Swift 版本，可能與 MacOS 上穩定 XCode 版本的 Swift 版本不一致。

## 建立 Docker 動作
{: #openwhisk_actions_docker}

使用 {{site.data.keyword.openwhisk_short}} Docker 動作，您可以使用任何語言來撰寫動作。

您的程式碼會編譯成可執行二進位檔，並內嵌至 Docker 映像檔。二進位程式與系統互動的方式是從 `stdin` 取得輸入，並透過 `stdout` 回覆。

先決條件是您必須具備「Docker 中心」帳戶。若要設定免費 Docker ID 及帳戶，請移至 [Docker 中心](https://hub.docker.com){: new_window}。

對於下面的指示，假設使用者 ID 是 "janesmith"，而密碼是 "janes_password"。假設已設定 CLI，則需要三個步驟才能設定供 {{site.data.keyword.openwhisk_short}} 使用的自訂二進位檔。之後，上傳的 Docker 映像檔可以當作動作使用。

1. 下載 Docker 架構。您可以使用 CLI 進行下載，如下所示：

  ```
  wsk sdk install docker
  ```
  {: pre}
  ```
  Docker 架構現在安裝在現行目錄中。
  ```
  {: screen}

  ```
  ls dockerSkeleton/
  ```
  {: pre}
  ```
  Dockerfile      README.md       buildAndPush.sh client          server
  ```
  {: screen}

  架構是一個 Docker 儲存器範本，您可以在其中以自訂二進位檔形式來注入程式碼。

2. 在 blackbox 架構中，設定您的自訂二進位檔。此架構已包括您可以使用的 C 程式。

  ```
  cat ./dockerSkeleton/client/example.c
  ```
  {: pre}
  {: pre}
  ```
  #include <stdio.h>
  
  int main(int argc, char *argv[]) {
      printf("Hello %s from arbitrary C program!\n",
             (argc == 1) ? "anonymous" : argv[1]);
  }
  ```
  {: screen}

  您可以視需要修改此檔案。

3. 建置 Docker 映像檔，並使用提供的 Script 予以上傳。您必須先執行 `docker login` 進行鑑別，然後執行具有所選擇映像檔名稱的 Script。

  ```
  docker login -u janesmith -p janes_password
  ```
  {: pre}
  ```
  cd dockerSkeleton
  ```
  {: pre}
  ```
  ./buildAndPush.sh janesmith/blackboxdemo
  ```
  {: pre}

  請注意，example.c 檔案的一部分會編譯為 Docker 映像檔建置程序的一部分，因此不需要在機器上編譯的 C。

4. 若要從 Docker 映像檔建立動作，而非提供的 JavaScript 檔案，請新增 `--docker`，並將 JavaScript 檔名稱取代為 Docker 映像檔名稱。

  ```
  wsk action create --docker example janesmith/blackboxdemo
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result example --param payload Rey
  ```
  {: pre}
  ```
  {
      "msg": "Hello Rey from arbitrary C program!\n"
  }
  ```
  {: screen}


您可以在[參照](./openwhisk_reference.html#openwhisk_ref_docker)小節找到建立 Docker 動作的相關資訊。


## 監看動作輸出
{: #openwhisk_actions_polling}

其他使用者可能會呼叫 {{site.data.keyword.openwhisk_short}} 動作來回應各種事件，或是作為動作序列的一部分。在這類情況下，監視呼叫可能十分有用。

您可以使用 {{site.data.keyword.openwhisk_short}} CLI 來監看所呼叫動作的輸出。

1. 從 Shell，發出下列指令：
  ```
  wsk activation poll
  ```
  {: pre}

  此指令會啟動輪詢迴圈，以從啟動開始持續檢查日誌。

2. 切換至另一個視窗，然後呼叫動作：

  ```
  wsk action invoke /whisk.system/samples/helloWorld --param payload Bob
  ```
  {: pre}
  ```
  ok: invoked /whisk.system/samples/helloWorld with id 7331f9b9e2044d85afd219b12c0f1491
  ```
  {: screen}

3. 在輪詢視窗中，觀察啟動日誌：

  ```
  Activation: helloWorld (7331f9b9e2044d85afd219b12c0f1491)
    2016-02-11T16:46:56.842065025Z stdout: hello bob!
  ```
  {: screen}

  同樣地，只要執行輪詢公用程式，就可即時看到日誌中是否有任何代表您在 {{site.data.keyword.openwhisk_short}} 中執行的動作。

## 刪除動作
{: #openwhisk_delete_action}

刪除您不要使用的動作來進行清除。

1. 執行下列指令，以刪除動作：
  ```
  wsk action delete hello
  ```
  {: pre}
  ```
  ok: deleted hello
  ```
  {: screen}

2. 驗證動作不再出現於動作清單中。
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  ```
  {: screen}
