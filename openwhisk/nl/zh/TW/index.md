---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 開始使用 {{site.data.keyword.openwhisk_short}}
*前次更新：2016 年 2 月 17 日*

{{site.data.keyword.openwhisk}} 是分散式事件驅動運算服務。{{site.data.keyword.openwhisk_short}} 會執行應用程式邏輯，以回應來自 Web 或透過 HTTP 的行動式應用程式的事件或直接呼叫。事件可以從 Bluemix 服務（如 Cloudant）以及外部來源提供。開發人員可以關注撰寫應用程式邏輯，以及建立依需求執行的動作。執行動作的比率一律會符合事件比率，導致固有擴充及備援以及最佳使用率。只需為您的使用量付費，而且不需要管理伺服器。您也可以取得[原始碼](https://github.com/openwhisk/openwhisk)，以及自行執行系統。
{: shortdesc}

如需 {{site.data.keyword.openwhisk_short}} 運作方式的詳細資料，請參閱[關於 {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html)。

## 設定 {{site.data.keyword.openwhisk_short}}
您可以使用 {{site.data.keyword.openwhisk_short}} 指令行介面 (CLI) 來設定名稱空間及授權金鑰。移至[配置 CLI](https://console.{DomainName}/openwhisk/cli){: new_window}，並遵循引導式體驗來進行安裝。請注意，您必須已在系統上安裝 Python 2.7，才能使用 CLI。

使用 CLI 設定 {{site.data.keyword.openwhisk_short}} 之後，您可以從指令行或透過 REST API 開始使用它。

## 使用 {{site.data.keyword.openwhisk_short}} CLI
完成您環境的配置之後，就可以開始使用 {{site.data.keyword.openwhisk_short}} CLI 來執行下列動作：

* 在 {{site.data.keyword.openwhisk_short}} 上，執行您的程式碼 Snippet 或動作。請參閱[建立及呼叫動作](./openwhisk_actions.html)。
* 使用觸發程式及規則，讓動作回應事件。請參閱[建立觸發程式及規則](./openwhisk_triggers_rules.html)。
* 瞭解套件如何組合動作以及配置外部事件來源。請參閱[使用及建立套件](./openwhisk_packages.html)。
* 探索套件的型錄，以及使用外部服務（例如 [Cloudant 事件來源](./openwhisk_catalog.html#openwhisk_catalog_cloudant)）來加強應用程式。請參閱[使用啟用 {{site.data.keyword.openwhisk_short}} 功能的服務](./openwhisk_catalog.html)。


## 從 iOS 應用程式使用 {{site.data.keyword.openwhisk_short}}
使用 {{site.data.keyword.openwhisk_short}} iOS SDK，即可從 iOS 行動式應用程式或 Apple Watch 使用 {{site.data.keyword.openwhisk_short}}。如需詳細資料，請參閱 [iOS 文件](./openwhisk_mobile_sdk.html)。

## 使用 REST API 與 {{site.data.keyword.openwhisk_short}} 搭配
啟用 {{site.data.keyword.openwhisk_short}} 環境之後，您可以使用 REST API 呼叫來搭配使用 {{site.data.keyword.openwhisk_short}} 與 Web 應用程式或行動式應用程式。如需動作、啟動、套件、規則及觸發程式的 API 的詳細資料，請參閱 [{{site.data.keyword.openwhisk_short}} API 文件](https://new-console.{DomainName}/apidocs/98)。

## {{site.data.keyword.openwhisk_short}} Hello World 範例
若要開始使用 {{site.data.keyword.openwhisk_short}}，請嘗試下列 JavaScript 程式碼範例。

```
/**
 * Hello world as an OpenWhisk action.
 */
function main(params) {
    var name = params.name || 'World';
    return {payload:  'Hello, ' + name + '!'};
}
```
{: codeblock}

若要使用此範例，請遵循下列步驟：

1. 將程式碼儲存至檔案。例如，*hello.js*。

2. 從 {{site.data.keyword.openwhisk_short}} CLI 指令行中，輸入下列指令來建立動作：

    ```
    wsk action create hello hello.js
    ```
    {: pre}

3. 然後，輸入下列指令來呼叫動作。

    ```
    wsk action invoke hello --blocking --result
    ```
    {: pre}  

    此指令會輸出：

    ```
    {
        "payload": "Hello, World!"
    }
    ```
    {: screen}

    ```
    wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    此指令會輸出：

    ```
    {
        "payload": "Hello, Fred!"
    }
    ```
    {: screen}

您也可以使用 {{site.data.keyword.openwhisk_short}} 中的事件驅動功能，來呼叫此動作以回應事件。請遵循[警示服務範例](./openwhisk_packages.html#openwhisk_packages_trigger)，將事件來源配置成每次產生定期事件時都呼叫 `hello` 動作。


## 系統詳細資料

您可以在下列主題中尋找 {{site.data.keyword.openwhisk_short}} 的其他資訊：

* [實體名稱](./openwhisk_reference.html#openwhisk_entities)
* [動作語意](./openwhisk_reference.html#openwhisk_semantics)
* [限制](./openwhisk_reference.html#openwhisk_syslimits)
* [REST API](https://new-console.{DomainName}/apidocs/98)

# 相關鏈結
## api
* [REST API 文件](https://new-console.{DomainName}/apidocs/98){:new_window}

## 一般
* [探索：{{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [IBM developerWorks 上的 {{site.data.keyword.openwhisk_short}}](https://developer.ibm.com/openwhisk/){:new_window}
