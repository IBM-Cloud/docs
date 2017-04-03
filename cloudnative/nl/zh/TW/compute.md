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

# 運算
{: #compute}

當您針對 Web 及行動建置雲端原生數位通道應用程式時，最佳作法是具備 Backend for Frontend (BFF)，其專用於數位通道，或針對 Web 及行動用戶端應用程式提供相同的資料及邏輯整合支援。如需此架構的相關資訊，請參閱[適用於 Web 及行動的微服務 ![外部鏈結圖示](../icons/launch-glyph.svg)](https://www.ibm.com/devops/method/content/architecture/omnichannelArchitecture)。

下圖顯示 BFF 架構概觀。

![BFF 架構](images/bff-arch.png)

圖 1：BFF 架構

BFF 的概念是摘錄自微服務或高價值 {{site.data.keyword.Bluemix}} 雲端服務的一般商業邏輯及整合邏輯。

使用此架構，您可以部署及釋放行動或 Web 應用程式的更新，以及搭配使用持續交付管線與開發作業服務來部署新版本的 BFF。

如果您有一個適用於 iOS 的 BFF 以及另一個適用於 Android 的 BFF，交付這些應用程式的功能的工程團隊不會受限於集中化 API 釋放排程的釋放特性。這是微服務及數位通道架構的一般目標 - 讓團隊經常釋放功能及特性，而不需要緊密連結另一個團隊的釋放排程。

<!--
## Backend for Frontends (BFF)
{: #bff}

Backend for Frontend patterns, commonly known as BFFs, really help you to focus on exposing business data and services in a form that matches the user interaction requirements. To optimize a user journey to your cloud solution, it may require a different user journey for the mobile application and a richer, more detailed journey for the Web application. With the introduction of voice-controlled devices like the [{{site.data.keyword.conversationfull}} ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/conversation.html) service, the interaction with a user could be controlled by voice. This digital channel will require a very different BFF for managing these voice intent-based interactions.

With {{site.data.keyword.Bluemix_notm}}, you can build a BFF by using polyglot programming approach to define the BFF. IBM recommends using Node, Swift, or Java and running them in a cloud native pattern with either Cloud Foundry, Container services, or serverless.

The BFF will manage the integration with services for data persistence, caching, and integration with high-value services like {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}}, and data analytics like {{site.data.keyword.sparks}}.

The BFF will expose an API most commonly using a REST pattern, but you can design your BFF to work from a messaging architecture using {{site.data.keyword.messagehub}}.
-->


## 整合行動用戶端與 Backend for Frontend
{: #integration}

為了啟用行動用戶端與 BFF 之間的輕鬆整合，{{site.data.keyword.Bluemix_notm}} 分別以 Swift 及 Java 語言支援適用於 iOS 及 Android 的行動用戶端 SDK 產生。若要啟用此特性，您必須使用 Open API 規格 (Swagger) 文件來公開 BFF 整合。此文件可以採用 JSON 或 YAML 格式。

用戶端 SDK 產生器使用 Open API 定義檔，來定義在原生行動應用程式中輕鬆使用的用戶端最佳化的開發人員 SDK。它將加速 BFF 與行動應用程式的整合。


## 定義 API
{: #definition}

BFF 需要公開符合即時伺服器端點上所執行之 Open API 規格的 API 定義檔。若要啟用「{{site.data.keyword.Bluemix_notm}} 開發人員體驗」及 {{site.data.keyword.Bluemix_notm}} SDK CLI（指令行介面）來探索此端點，您必須將環境變數新增至稱為 `OPENAPI_SPEC` 的 Cloud Foundry 應用程式。此環境變數必須參照使用相對路徑的規格。

若要在 {{site.data.keyword.Bluemix_notm}} 中新增 `OPENAPI_SPEC` 環境變數，請遵循下列步驟：

1. 登入 [{{site.data.keyword.Bluemix_notm}} ![外部鏈結圖示](../icons/launch-glyph.svg)](http://bluemix.net)。
2. 選取 Cloud Foundry 應用程式。
3. 選取**運行環境**。
4. 選取**環境變數**。
5. 按一下**使用者定義**區段中的**新增**。
6. 在**名稱**中指定 `OPENAPI_SPEC`，並指定 Open API 定義檔的相對 URL 路徑。
7. 按一下**儲存**。

<!--
To add the `OPENAPI_SPEC` environment variable locally and push your changes to {{site.data.keyword.Bluemix_notm}} with the [Cloud Foundry CLI ![External link icon](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli#getting-started), follow these steps:

1. Open Terminal and navigate to your project directory.
2. Add the following code to the `manifest.yml` file.

   ```
   env:
       "OPENAPI_SPEC": "<relative URL path to your Open API definition file>"
   ```
   {: codeblock}
3. Save your changes to the `manifest.yml` file.
4. Run `cf push` to deploy the changes to {{site.data.keyword.Bluemix_notm}}.
-->

例如：

```
OPENAPI_SPEC='/explorer/swagger.json'
```
{: codeblock}

{{site.data.keyword.apiconnect_long}} 及 Loopback 應用程式特別適合使用此方式。您可以使用 Loopback 及 {{site.data.keyword.apiconnect_short}} 來定義持續性模型，以及使用 Open API 定義檔來公開 CRUD（建立、讀取、更新及刪除）作業。

您也可以定義商業邏輯作業。


### Open API 規格的支援元素
{: #supported-elements notoc}

Open API 規格中唯一未完全支援的部分是檔案結構。此規格容許將定義的各部分分割為不同檔案，並使用 json `$ref` 欄位予以參照。您的整個定義必須包含在一個檔案內。


## 使用 Bluegen 的 Backend for Frontend 範例
{: #bff-bluegen}

{{site.data.keyword.Bluemix_notm}} 已使用 {{site.data.keyword.apiconnect_short}} 及 Strongloop 來建立參照 BFF（這會將產品模型對映至 {{site.data.keyword.cloudant}}），以及建立用於參照 {{site.data.keyword.objectstorageshort}} 中映像檔的映像檔 API。

您可以使用此 BFF 型樣，快速開始將完全運作的 BFF 佈建至 {{site.data.keyword.Bluemix_notm}}，以及使用它協助瞭解將 BFF 整合至行動專案並分別以 Swift 及 Java 產生適用於 iOS 及 Android 的原生 SDK 是多麼簡單。

請遵循 [README ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/backend-for-frontend-node) 指示來建立並安裝專案。


## 搭配使用 Backend for Frontend 與開發人員體驗專案
{: #bff-devex}

「{{site.data.keyword.Bluemix_notm}} 行動開發人員體驗」的設計目的是要簡化定義具有許多相關聯雲端服務的行動專案。您可以輕鬆地新增 [{{site.data.keyword.mobilepushshort}} ![外部鏈結圖示](../icons/launch-glyph.svg)](/docs/services/mobilepush/index.html)、[分析 ![外部鏈結圖示](../icons/launch-glyph.svg)](/docs/services/mobileanalytics/index.html)，以及資料或儲存空間服務。

{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} 引進在**運算**頁面中將 BFF 整合至行動專案的能力。您可以將現有「運算」服務實例新增至行動專案。新增之後，即可針對您選擇的語言來產生原生 SDK，也可以產生完整專案，以及在**程式碼**頁面中，將 SDK 整合至專案的來源套件。這特別適用於與已明確定義之 BFF 的整合。

下載專案之後，即可使用 Xcode 或 Android Studio 來開啟它，以及使用用戶端 SDK 來編譯專案。


## 使用 CLI
{: #cli}

開發 BFF 時，API 規格可能會變更。若要支援這些變更，您有下列兩個選項。

* 將整個專案重新產生成新的 GitHub 分支，並將變更合併為開發分支。
* 使用指令行 (CLI) 工具直接重新產生 SDK，並且只更新行動專案的 SDK 部分。

若要使用 CLI，您必須予以[安裝](sdk_cli.html#installation)。

使用下列指令，以列出您可執行的動作。

```
bluemix sdk
```
{: codeblock}

使用下列指令，以列出現行 {{site.data.keyword.Bluemix_notm}} 空間中的執行中 Cloud Foundry 實例。

```
bluemix sdk list
```
{: codeblock}

如果設定 `OPENAPI_SPEC` 環境變數，則會列出每一個應用程式，並驗證 API。在 `VALID` 直欄中，您會看到綠色勾號或紅色 `X`。應用程式之 `VALID` 直欄中的勾號表示具有有效的 Open API 定義。應用程式之 `VALID` 直欄中的 `X` 表示下列兩個事項之一：

* 未定義應用程式的 `OPENAPI_SPEC` 環境變數，或者
* 對於 Open API 規格，API 定義無效

使用下列指令，以檢視 API 的形式完整 URL。會列出 API 規格的形式完整路徑及 URI。您可以在瀏覽器中檢視原始規格、在 CLI 中直接使用它，或驗證已正確地設定 BFF `OPENAPI_SPEC` 環境變數。

```
bluemix sdk list --url
```
{: codeblock}

使用下列指令，以驗證 `<AppName>` 的 Open API 定義檔來判斷是否可以使用它來產生 SDK。此指令會在您的現行空間中尋找 `<AppName>`，並在 `OPENAPI_SPEC` 環境變數中使用相對路徑來尋找進行驗證的規格。

```
bluemix sdk validate <AppName>
```
{: codeblock}

使用下列指令，以產生適用於您所選擇之原生 `<Platform>` 的 SDK，並將壓縮檔放入現行工作目錄。

```
bluemix sdk generate <AppName> <SDKName> --<Platform>
```
{: codeblock}

使用 `--unzip` 選項會將 SDK 自動解壓縮至現行工作目錄。您可以選擇性地使用 `--output` 選項指定用來解壓縮 SDK 的位置。您可以使用 GitHub 管理原始碼，並建立專門用來更新 SDK 的新分支。使用此方式可以更輕鬆地檢視已更新 SDK 中的變更，並將其合併至開發分支。


## 使用 SDK 產生的模型及 API
{: #models-apis}

既然已使用產生的 SDK 將您的 BFF 整合至行動應用程式，您就可以開始使用。

SDK 在 `docs` 目錄及 `source` 目錄中隨附完整的產生文件。您可以開啟 `README.html` 檔案以取得文件的 Web 視圖，或開啟 `README.md` 檔案以取得文件的 Markdown 視圖。將 SDK 發佈至 Cocoapods 或 Maven Central 時，Markdown 文件十分有用。

在本文件內，您可以看到產生的 API 清單。您可以按一下 API 來查看可直接貼入行動應用程式的程式碼 Snippet。
