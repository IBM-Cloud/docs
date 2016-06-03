---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 使用及建立 {{site.data.keyword.openwhisk_short}} 套件
{: #openwhisk_packages}
*前次更新：2016 年 3 月 28 日*

在 {{site.data.keyword.openwhisk}} 中，您可以使用套件以將一組相關動作組合在一起，並與其他人共用。

套件可以包括*動作* 及*資訊來源*。
- 動作是在 {{site.data.keyword.openwhisk_short}} 上執行的程式碼片段。例如，Cloudant 套件包括在 Cloudant 資料庫中讀取及寫入記錄的動作。
- 資訊來源是用來配置外部事件來源，以發動觸發程式事件。例如，「警示」套件包括可依指定的頻率發動觸發程式的資訊來源。

每個 {{site.data.keyword.openwhisk_short}} 實體（包括套件）都屬於*名稱空間*，而實體的完整名稱是 `/namespaceName[/packageName]/entityName`。如需相關資訊，請參閱[命名準則](./openwhisk_reference.html#openwhisk_entities)。

下列各節說明如何瀏覽套件，以及如何使用其中的觸發程式及資訊來源。此外，如果是對將自己的套件提出至型錄感興趣的使用者，請閱讀有關建立及共用套件的各小節。

## 瀏覽套件
{: #openwhisk_packagedisplay}

{{site.data.keyword.openwhisk_short}} 中已登錄數個套件。您可以取得名稱空間中的套件清單、列出套件中的實體，以及取得套件中個別實體的說明。

1. 取得 `/whisk.system` 名稱空間中的套件清單。

  ```
  wsk package list /whisk.system
  ```
  {: pre}
  ```
  packages
  /whisk.system/alarms                                              shared
  /whisk.system/cloudant                                            shared
  /whisk.system/github                                              shared
  /whisk.system/samples                                             shared
  /whisk.system/slack                                               shared
  /whisk.system/util                                                shared
  /whisk.system/watson                                              shared
  /whisk.system/weather                                             shared
  ```
  {: screen}

2. 取得 `/whisk.system/cloudant` 套件中的實體清單。

  ```
  wsk package get --summary /whisk.system/cloudant
  ```
  {: pre}
  ```
  package /whisk.system/cloudant: Cloudant database service
     (params: {{site.data.keyword.Bluemix_notm}}ServiceName host username password dbname includeDoc overwrite)
   action /whisk.system/cloudant/read: Read document from database
   action /whisk.system/cloudant/write: Write document to database
   feed   /whisk.system/cloudant/changes: Database change feed
  ```
  {: screen}

  此輸出顯示 Cloudant 套件提供兩個動作（`read` 及 `write`）以及一個稱為 `changes` 的觸發程式資訊來源。`changes` 資訊來源會導致在指定的 Cloudant 資料庫中新增文件時發動觸發程式。

  Cloudant 套件也定義參數 `username`、`password`、`host` 及 `port`。您必須指定這些參數，動作及資訊來源才有意義。例如，這些參數容許動作在特定 Cloudant 帳戶上操作。

3. 取得 `/whisk.system/cloudant/read` 動作的說明。

  ```
  wsk action get --summary /whisk.system/cloudant/read
  ```
  {: pre}
  ```
  action /whisk.system/cloudant/read: Read document from database
     (params: dbname includeDoc id)
  ```
  {: screen}

  此輸出顯示 Cloudant `read` 動作需要三個參數（包括要擷取的資料庫及文件 ID）。


## 在套件中呼叫動作
{: #openwhisk_package_invoke}

您可以在套件中呼叫動作，就像處理其他動作一樣。下列幾個步驟顯示如何使用不同的參數在 `/whisk.system/samples` 套件中呼叫 `greeting` 動作。

1. 取得 `/whisk.system/samples/greeting` 動作的說明。

  ```
  wsk action get --summary /whisk.system/samples/greeting
  ```
  {: pre}
  ```
  action /whisk.system/samples/greeting: Print a friendly greeting
     (params: name place)
  ```
  {: screen}

  請注意，`greeting` 動作接受兩個參數：`name` 及 `place`。

2. 不使用任何參數來呼叫動作。

  ```
  wsk action invoke --blocking --result /whisk.system/samples/greeting
  ```
  {: pre}
  ```
  {
      "payload": "Hello, stranger from somewhere!"
  }
  ```
  {: screen}

  輸出是一則一般訊息，因為未指定任何參數。

3. 使用參數來呼叫動作。

  ```
  wsk action invoke --blocking --result /whisk.system/samples/greeting --param name Mork --param place Ork
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Mork from Ork!"
  }
  ```
  {: screen}

  請注意，輸出使用已傳遞給動作的 `name` 及 `place` 參數。


## 建立及使用套件連結
{: #openwhisk_package_bind}

雖然您可以直接使用套件中的實體，但是可能會發現您每次都將相同的參數傳遞給動作。避免此狀況的方式是連結至套件，並指定預設參數。套件中的動作會繼承這些參數。

例如，在 `/whisk.system/cloudant` 套件中，您可以在套件連結中設定預設 `username`、`password` 及 `dbname` 值，而這些值會自動傳遞給套件中的所有動作。

在下列簡單範例中，您連結至 `/whisk.system/samples` 套件。

1. 連結至 `/whisk.system/samples`，並設定預設 `place` 參數值。

  ```
  wsk package bind /whisk.system/samples valhallaSamples --param place Valhalla
  ```
  {: pre}
  ```
  ok: created binding valhallaSamples
  ```
  {: screen}

2. 取得套件連結的說明。

  ```
  wsk package get --summary valhallaSamples
  ```
  {: pre}
  ```
  package /myNamespace/valhallaSamples
   action /myNamespace/valhallaSamples/greeting: Print a friendly greeting
   action /myNamespace/valhallaSamples/wordCount: Count words in a string
   action /myNamespace/valhallaSamples/helloWorld: Print to the console
   action /myNamespace/valhallaSamples/echo: Returns the input arguments, unchanged
  ```
  {: screen}

  請注意，`valhallaSamples` 套件連結中提供 `/whisk.system/samples` 套件中的所有動作。

3. 在套件連結中呼叫動作。

  ```
  wsk action invoke --blocking --result valhallaSamples/greeting --param name Odin
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Odin from Valhalla!"
  }
  ```
  {: screen}

  請注意動作繼承您在建立 `valhallaSamples` 套件連結時所設定的 `place` 參數的結果。

4. 呼叫動作，並且改寫預設參數值。

  ```
  wsk action invoke --blocking --result valhallaSamples/greeting --param name Odin --param place Asgard
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Odin from Asgard!"
  }
  ```
  {: screen}

  請注意，透過動作呼叫指定的 `place` 參數值會改寫 `valhallaSamples` 套件連結中所設定的預設值。


## 建立及使用觸發程式資訊來源
{: #openwhisk_package_trigger}

資訊來源提供一種簡便的方法，將外部事件來源配置成向 {{site.data.keyword.openwhisk_short}} 觸發程式發動這些事件。此範例顯示如何使用「警示」套件中的資訊來源來每秒發動觸發程式，以及使用規則來每秒呼叫動作。

1. 取得 `/whisk.system/alarms` 套件中資訊來源的說明。

  ```
  wsk package get --summary /whisk.system/alarms
  ```
  {: pre}
  ```
  package /whisk.system/alarms
   feed   /whisk.system/alarms/alarm
  ```
  {: screen}

  ```
  wsk action get --summary /whisk.system/alarms/alarm
  ```
  {: pre}
  ```
  action /whisk.system/alarms/alarm: Fire trigger when alarm occurs
     (params: cron trigger_payload)
  ```
  {: screen}

  `/whisk.system/alarms/alarm` 資訊來源接受兩個參數：
  - `cron`：何時發動觸發程式的 crontab 規格。
  - `trigger_payload`：要在每一個觸發程式事件中設定的有效負載參數值。

2. 建立每八秒即發動的觸發程式。

  ```
  wsk trigger create everyEightSeconds --feed /whisk.system/alarms/alarm -p cron '*/8 * * * * *' -p trigger_payload '{"name":"Mork", "place":"Ork"}'
  ```
  {: pre}
  ```
  ok: created trigger feed everyEightSeconds
  ```
  {: screen}

3. 使用下列動作碼來建立 'hello.js' 檔案。

  ```
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

4. 確定動作已存在。

  ```
  wsk action update hello hello.js
  ```
  {: pre}

5. 建立規則，以在每次 `everyEightSeconds` 觸發程式發動時呼叫 `hello` 動作。

  ```
  wsk rule create --enable myRule everyEightSeconds hello
  ```
  {: pre}
  ```
  ok: created rule myRule
  ok: rule myRule is activating
  ```
  {: screen}

6. 確認是透過輪詢啟動日誌來呼叫動作。

  ```
  wsk activation poll
  ```
  {: pre}

  您應該每八秒就會看到觸發程式、規則及動作的啟動。在每次呼叫時，動作都會接收到參數 `{"name":"Mork", "place":"Ork"}`。


## 建立套件
{: #openwhisk_packages_create}

套件用來組織一組相關動作及資訊來源。
它也容許在套件中的所有實體之間共用參數。

若要建立具有簡單動作的自訂套件，請嘗試下列範例：

1. 建立稱為 "custom" 的套件。

  ```
  wsk package create custom
  ```
  {: pre}
  ```
  ok: created package custom
  ```
  {: screen}

2. 取得套件的摘要。

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /myNamespace/custom
  ```
  {: screen}

  請注意，套件是空的。

3. 建立稱為 `identity.js` 且包含下列動作碼的檔案。此動作會傳回所有輸入參數。

  ```
  function main(args) { return args; }
  ```
  {: codeblock}

4. 在 `custom` 套件中，建立 `identity` 動作。

  ```
  wsk action create custom/identity identity.js
  ```
  {: pre}
  ```
  ok: created action custom/identity
  ```
  {: screen}

  在套件中建立動作，需要您在動作名稱前面加上套件名稱。不容許套件巢狀。套件只能包含動作，而且不能包含另一個套件。

5. 再次取得套件的摘要。

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /myNamespace/custom
   action /myNamespace/custom/identity
  ```
  {: screen}

  現在，您可以在名稱空間中看到 `custom/identity` 動作。

6. 在套件中呼叫動作。

  ```
  wsk action invoke --blocking --result custom/identity
  ```
  {: pre}
  ```
  {}
  ```
  {: screen}


您可以設定套件中所有實體的預設參數。作法是設定套件中所有動作所繼承的套件層次參數。若要查看此作業的運作方式，請嘗試下列範例：

1. 使用兩個參數來更新 `custom` 套件：`city` 及 `country`。

  ```
  wsk package update custom --param city Austin --param country USA
  ```
  {: pre}
  ```
  ok: updated package custom
  ```
  {: screen}

2. 顯示套件及動作中的參數，以及查看套件中的 `identity` 動作如何繼承套件中的參數。

  ```
  wsk package get custom parameters
  ```
  {: pre}
  ```
  ok: got package custom, projecting parameters
  [
      {
          "key": "city",
          "value": "Austin"
      },
      {
          "key": "country",
          "value": "USA"
      }
  ]
  ```
  {: screen}

  ```
  wsk action get custom/identity parameters
  ```
  {: pre}
  ```
  ok: got action custom/identity, projecting parameters
  [
      {
          "key": "city",
          "value": "Austin"
      },
      {
          "key": "country",
          "value": "USA"
      }
  ]
  ```
  {: screen}

3. 不使用任何參數來呼叫 identity 動作，以驗證動作確實繼承參數。

  ```
  wsk action invoke --blocking --result custom/identity
  ```
  {: pre}
  ```
  {
      "city": "Austin",
      "country": "USA"
  }
  ```
  {: screen}

4. 使用一些參數來呼叫 identity 動作。呼叫參數會與套件參數合併；呼叫參數會置換套件參數。

  ```
  wsk action invoke --blocking --result custom/identity --param city Dallas --param state Texas
  ```
  {: pre}
  ```
  {
      "city": "Dallas",
      "country": "USA",
      "state": "Texas"
  }
  ```
  {: screen}


## 共用套件
{: #openwhisk_packages_share}

在除錯及測試包含套件的動作及資訊來源之後，即可與所有 {{site.data.keyword.openwhisk_short}} 使用者共用套件。透過共用套件，使用者可以連結套件、呼叫套件中的動作，以及編寫 {{site.data.keyword.openwhisk_short}} 規則及序列動作。

1. 與所有使用者共用套件：

  ```
  wsk package update custom --shared
  ```
  {: pre}
  ```
  ok: updated package custom
  ```
  {: screen}

2. 顯示套件的 `publish` 內容，以驗證它現在為 true。

  ```
  wsk package get custom publish
  ```
  {: pre}
  ```
  ok: got package custom, projecting publish
  true
  ```
  {: screen}


其他人現在可以使用 `custom` 套件（包括連結至套件，或直接呼叫其中的動作）。其他使用者必須知道套件的完整名稱，才能連結套件或呼叫其中的動作。共用套件內的動作及資訊來源為*公用*。如果套件為專用，則其所有內容也會是專用。

1. 取得套件的說明，以顯示套件及動作的完整名稱。

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /myNamespace/custom
   action /myNamespace/custom/identity
  ```
  {: screen}

  在前一個範例中，您是使用 `myNamespace` 名稱空間，而此名稱空間是以完整名稱顯示。

