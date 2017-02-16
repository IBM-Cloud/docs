---

copyright:
  years: 2016, 2017
lastupdated: "2016-09-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 開始使用 {{site.data.keyword.openwhisk_short}}


{{site.data.keyword.openwhisk}} 是分散式事件驅動運算服務（也稱為「無伺服器運算」或「功能即服務 (FaaS)」），{{site.data.keyword.openwhisk_short}} 會執行應用程式邏輯，以從 Web 或透過 HTTP 的行動應用程式回應事件或直接呼叫。事件可以從 Bluemix 服務（如 Cloudant）以及外部來源提供。開發人員可以關注撰寫應用程式邏輯，以及建立依需求執行的動作。執行動作的比率一律會符合事件比率，這導致根本的擴充及備援以及最佳使用率。您只需為您的用量付費，而且不需要管理伺服器。您也可以取得[原始碼](https://github.com/openwhisk/openwhisk)，以及自行執行系統。
{: shortdesc}

如需 {{site.data.keyword.openwhisk_short}} 運作方式的詳細資料，請參閱[關於 {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html)。

您可以使用「瀏覽器」或 CLI 來開發 {{site.data.keyword.openwhisk_short}} 應用程式。
這兩者具有類似的功能可用來開發應用程式；CLI 可讓您進一步控制部署及作業。


## 在瀏覽器中開發
{: #openwhisk_start_editor}

請在[瀏覽器](https://console.{DomainName}/openwhisk/editor){: new_window}中試用 {{site.data.keyword.openwhisk_short}} 來建立動作、使用觸發程式自動化動作，以及探索公用套件。
如需「OpenWhisk 使用者介面」的快速導覽，請造訪[進一步瞭解](https://console.{DomainName}/openwhisk/learn){: new_window}頁面。

## 設定 {{site.data.keyword.openwhisk_short}} CLI
{: #openwhisk_start_configure_cli}

您可以使用 {{site.data.keyword.openwhisk_short}} 指令行介面 (CLI) 來設定名稱空間及授權金鑰。移至[配置 CLI](https://new-console.{DomainName}/openwhisk/cli){: new_window}，並遵循指示進行安裝。

### 配置 CLI 以使用 HTTPS Proxy
{: #openwhisk_configure_https_proxy_cli}

CLI 可以設定成使用 HTTPS Proxy。若要設定 HTTPS Proxy，必須建立稱為 `HTTPS_PROXY` 的環境變數。變數必須設為 HTTPS Proxy 的位址，而其埠的格式如下：`{PROXY IP}:{PROXY PORT}`。

使用 CLI 設定 {{site.data.keyword.openwhisk_short}} 之後，您可以從指令行開始使用它。

## 使用 {{site.data.keyword.openwhisk_short}} CLI
{: #openwhisk_start_using_cli}

在您[已配置環境](https://new-console.{DomainName}/openwhisk/cli){: new_window}之後，可以開始使用 {{site.data.keyword.openwhisk_short}} CLI 來執行下列動作：

* 在 {{site.data.keyword.openwhisk_short}} 上，執行您的程式碼 Snippet 或動作。請參閱[建立及呼叫動作](./openwhisk_actions.html)。
* 使用觸發程式及規則，讓動作回應事件。請參閱[建立觸發程式及規則](./openwhisk_triggers_rules.html)。
* 瞭解套件如何組合動作以及配置外部事件來源。請參閱[使用及建立套件](./openwhisk_packages.html)。
* 探索套件的型錄，以及使用外部服務（例如 [Cloudant 事件來源](./openwhisk_catalog.html#openwhisk_catalog_cloudant)）來加強應用程式。請參閱[使用啟用 {{site.data.keyword.openwhisk_short}} 功能的服務](./openwhisk_catalog.html)。


## 從 iOS 應用程式使用 {{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_using_ios}

使用 {{site.data.keyword.openwhisk_short}} iOS SDK，即可從 iOS 行動應用程式或 Apple Watch 使用 {{site.data.keyword.openwhisk_short}}。如需詳細資料，請參閱 [iOS 文件](./openwhisk_mobile_sdk.html)。

## 使用 REST API 與 {{site.data.keyword.openwhisk_short}} 搭配
{: #openwhisk_start_using_restapi}

啟用 {{site.data.keyword.openwhisk_short}} 環境之後，您可以使用 REST API 呼叫來搭配使用 {{site.data.keyword.openwhisk_short}} 與 Web 應用程式或行動應用程式。如需有關動作、啟動、套件、規則及觸發程式的 API 的詳細資料，請參閱 [{{site.data.keyword.openwhisk_short}} API 文件](https://new-console.{DomainName}/apidocs/98)。

## {{site.data.keyword.openwhisk_short}} Hello World 範例
{: #openwhisk_start_hello_world}
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
{: #openwhisk_system_details}

您可以在下列主題中尋找 {{site.data.keyword.openwhisk_short}} 的其他資訊：

* [實體名稱](./openwhisk_reference.html#openwhisk_entities)
* [動作語意](./openwhisk_reference.html#openwhisk_semantics)
* [限制](./openwhisk_reference.html#openwhisk_syslimits)
* [REST API](https://new-console.{DomainName}/apidocs/98)

# 相關鏈結
{: #rellinks notoc}

## API 參考資料
{: #api}
* [REST API 文件](./openwhisk_reference.html#openwhisk_ref_restapi)
* [REST API](https://new-console.{DomainName}/apidocs/98){:new_window}

## 相關鏈結
{: #general}
* [探索：{{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [IBM developerWorks 上的 {{site.data.keyword.openwhisk_short}}](https://developer.ibm.com/openwhisk/){:new_window}
