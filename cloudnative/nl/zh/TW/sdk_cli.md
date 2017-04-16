---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# SDK 產生器外掛程式
{: #sdk-cli}

「{{site.data.keyword.IBM}} SDK 產生器」外掛程式可以安裝於 [{{site.data.keyword.Bluemix_notm}} CLI ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/cli/reference/bluemix_cli/index.html)。

身為 {{site.data.keyword.Bluemix_notm}} 上的開發人員，您可以使用此外掛程式，從 [Open API 規格 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.openapis.org/) 相容的 REST API 定義產生 SDK。變更 REST API 定義時，可以使用此外掛程式僅重新產生 SDK，而不是重新產生整個專案。

您也可以查看給定空間中的 Cloud Foundry 應用程式是否有適用於產生 SDK 的 REST API 定義。最終，您可以使用「{{site.data.keyword.IBM_notm}} SDK 產生器」外掛程式來驗證任何 REST API 定義，確定它們符合 SDK 產生器需求。

此「{{site.data.keyword.IBM_notm}} SDK 產生器」外掛程式可讓您使用產生的 SDK 將後端服務輕鬆地整合至應用程式。REST API 變更時，您可以重新產生 SDK，並取代舊的 SDK 以進行無縫式 SDK 升級。您也可以將 CLI 整合至 DevOps 管線，並確定 SDK 在每次建置應用程式時一律與 API 規格一致。

REST API 定義必須有效，並且在即時伺服器端點上或您系統的本端檔案上進行管理。如果管理 REST API 定義，則相對 URL 必須定義於 `OPENAPI_SPEC` 環境變數。


## 需求
{: #prereqs}

請確定您滿足下列需求。

* 您具有 [{{site.data.keyword.Bluemix_notm}} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://bluemix.net) 帳戶
* 符合 [Open API ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.openapis.org/) 規格的有效 API 定義


## 安裝
{: #installation}

1. [安裝 {{site.data.keyword.Bluemix}} CLI ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://clis.ng.bluemix.net/ui/home.html)。

2. [安裝外掛程式 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/cli/reference/bluemix_cli/index.html#install_plug-in)。

	```
	bx plugin install sdk-gen -r Bluemix
	```
	{: codeblock}


## 指令
{: #commands}

使用下列指令以產生 SDK、驗證 Open API 定義檔，或列出 Cloud Foundry 應用程式。


### 產生 SDK
{: #gen}

使用 `bluemix sdk generate [arguments...][command options]`。


#### 引數
{: #gen-args}

* `APP_NAME` - 現行空間中 Cloud Foundry 應用程式的名稱
* `OPENAPI_DOC_LOCATION` - 原始 REST API 定義 JSON 或 Yaml 的 URL 或相對檔案路徑
* `GENERATED_SDK_NAME`（選用）- 所產生 SDK 的名稱


#### 選項
{: #gen-options}

* `PLATFORM`（必要）
   * `--android` - 產生 Android SDK
   * `--ios` - 產生 iOS Swift SDK
   * `--swift` - 產生 Swift 伺服器 SDK
* `--output "YOUR_RELATIVE_PATH"`（選用）- 將產生的 SDK 放入 `YOUR_RELATIVE_PATH` 所指定的目錄（如果有現有的 SDK，則會進行覆寫）
* `--unzip`（選用）- 解壓縮產生的 SDK（如果有現有的 SDK 構件，則會進行覆寫）


#### 用法
{: #gen-usage}

若要從 {{site.data.keyword.Bluemix_notm}} 中執行的 Cloud Foundry 應用程式產生 SDK，您可以使用應用程式的名稱作為 CLI 的參數。下列指令使用應用程式的名稱作為 `SDK_Name`。

```
bluemix sdk generate [APP_NAME] [PLATFORM]
```
{: codeblock}

若要從 Open API 定義檔或者本端 JSON 或 Yaml 檔案的 URL 產生 SDK，請使用下列指令。

```
bluemix sdk generate [OPENAPI_DOC_LOCATION] [SDK_Name] [Platform]
```
{: codeblock}


### 驗證 Open API 定義
{: #validating}

使用 `bluemix sdk validate [argument]`。


#### 引數
{: #val-args}

* `APP_NAME` - 現行空間中 Cloud Foundry 應用程式的名稱
* `OPENAPI_DOC_LOCATION` - 原始 REST API 定義 JSON 或 Yaml 的 URL 或相對檔案路徑


#### 用法
{: #val-usage}

若要驗證 {{site.data.keyword.Bluemix_notm}} 中執行之 Cloud Foundry 應用程式的 API 規格，您可以使用應用程式的名稱作為 CLI 的參數。

```
bluemix sdk validate [APP_NAME]
```
{: codeblock}

若要從 API 規格文件或者本端 JSON 或 Yaml 檔案的 URL 驗證 SDK，請使用下列指令。

```
bluemix sdk validate [OPENAPI_DOC_LOCATION]
```
{: codeblock}



### 列出應用程式 (Cloud Foundry)
{: #list-apps}

使用 `bluemix sdk list [argument][option]` 列出應用程式以及驗證 API 規格。您必須將 `OPENAPI_SPEC` 環境變數設為管理您規格的相對 URL 路徑。


#### 引數
{: #list-args}

* `SPACE_NAME`（選用）- 現行組織內您要搜尋應用程式的 Cloud Foundry 空間名稱。如果未提供，則會搜尋現行空間。


#### 選項
{: #list-options}

* `--url`（選用）- 顯示清單中每一個應用程式之 Open API 定義的形式完整的 URL


#### 用法
{: #list-usage}

若要列出現行空間中的應用程式，請使用下列指令。

```
bluemix sdk list
```
{: codeblock}

若要列出現行空間中的應用程式，並顯示 API 規格 URL，請使用下列指令。

```
bluemix sdk list --url
```
{: codeblock}

若要列出特定空間中的應用程式，請使用下列指令。

```
bluemix sdk list [SPACE_NAME]
```
{: codeblock}

若要列出特定空間中的應用程式，並顯示 API 規格 URL，請使用下列指令。

```
bluemix sdk list [SPACE_NAME] --url
```
{: codeblock}
