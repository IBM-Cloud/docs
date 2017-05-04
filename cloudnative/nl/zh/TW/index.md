---

copyright:
  years: 2016, 2017
lastupdated: "2016-04-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# 建置雲端原生專案
{: #web-mobile}

您可以透過 {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} [專案](projects.html)的概念來管理雲端原生應用程式。您可以針對 {{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}} CLI，使用 [{{site.data.keyword.dev_console}}](devex.html) 或 [{{site.data.keyword.dev_cli_notm}}](dev_cli.html) 來建立專案。{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} 會將雲端原生應用程式開發人員所需的最常用服務功能帶入已針對開發人員最佳化的單一已連接體驗。

{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} 可讓雲端原生應用程式開發人員透過各種[型樣類型](patterns.html)及[入門範本](starters.html)建立專案、建立主要 {{site.data.keyword.Bluemix_notm}} 最佳化服務並將其連接至專案，以及使用 SDK 快速下載工作中程式碼。SDK 已與功能認證或相依關係完全整合，可讓您立即執行。如果您的應用程式正在執行，並且您已設定及配置功能，則可以回到專案以監視及管理與應用程式使用者的互動。您也可以透過 {{site.data.keyword.dev_console}} 配置及管理服務。

<!--
While the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} provides an integrated development experience, some developers might still want to have finer-grained control and wire services together manually. If this is your preferred approach, you might want to consider using the [{{site.data.keyword.mobilefirstbp}} Starter boilerplate](try_mobile.html).
-->

<!--With {{site.data.keyword.Bluemix}} Mobile services, you can incorporate pre-built, managed, and scalable cloud services into your mobile applications. You can focus on building your mobile apps, instead of the complexities of managing the back-end infrastructure.

The Mobile dashboard provides an integrated experience on {{site.data.keyword.Bluemix_notm}} where you can create mobile projects easily from within the dashboard.
-->


## 專案
{: #projects}

{{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} 會將應用程式使用者介面、資料及服務結合在一個完整的*專案* 中。透過建立專案，應用程式的所有必要部分及已新增功能都會在 {{site.data.keyword.Bluemix_notm}} 伺服器上進行維護。如果服務已配置到專案，您就可以下載應用程式碼以及必要認證和起始設定程式。您可以選取**專案**來檢視所有專案。  

您可以在**專案**頁面上選取專案，來檢視單一專案的其他資訊。這會顯示**專案概觀**頁面，其中包括針對專案所配置及提供的服務。服務是透過新增功能來擴充應用程式的個別功能。因為它們是個別新增的，所以您可以新增所需的服務，例如推送服務、鑑別、資料和儲存空間或其他服務。若您在**專案概觀**頁面上將服務新增至專案、並且遵循指示進行配置，服務就會自動與您的應用程式相關聯。如需「專案概觀」頁面的相關資訊，請參閱[專案概觀頁面](project_overview_page.html)。

若要建立專案，您必須選取後面接著一個[入門範本](starters.html)的[型樣](patterns.html)。


### 專案概觀頁面
{: #project_overview}

您可以檢視及使用單一 {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} 專案，方法是在**專案**頁面上選取專案，這會開啟「專案概觀」頁面。
{: shortdesc}

**專案概觀**頁面會為每一個配置的功能或每一個可用於使用選取的專案來配置的功能顯示一個磚。這個磚會顯示功能的類型，以及一個具有三個垂直對齊點的*動作* 按鈕。可以使用或配置的功能範例包括 {{site.data.keyword.mobilepushshort}}、分析、資料及儲存空間。相容的功能取決於專案類型以及可在該地區使用的功能，因此並非所有功能都可用來與所有專案產生關聯。 

當功能類型尚未與專案相關聯時，磚上會顯示一個**建立**按鈕。動作按鈕選項為建立服務的實例，或在功能尚未關聯時新增現有服務實例。選取**新增現有項目**會提供空間內該類型之服務實例的清單。

如果功能已與此專案相關聯，則相關聯之服務實例的名稱會顯示在磚上，位於功能類型後面。這讓您可在 {{site.data.keyword.dev_console}} 上輕鬆發現哪個服務實例與此專案相關。當功能已與專案相關聯時，可在動作按鈕上使用的動作為**檢視**及**移除**。移除服務實例只會移除與此專案的關聯，並不會從 {{site.data.keyword.dev_console}} 中刪除服務實例。若要刪除服務實例，請按一下 **Web 及行動 > 服務**頁面來檢視及刪除服務實例。

在**程式碼**磚上選取**取得程式碼**，為您的專案下載程式碼。如需下載程式碼的相關資訊，請參閱[取得程式碼](get_code.html)。


### 更新專案以使用新的入門範本
{: #update-starter}

1. 從**專案**或**專案概觀**頁面中，按一下**溢位功能表**圖示，然後選取**更新入門範本**。

2. 選擇新的「入門範本」，然後按一下**更新**。

3. 按一下**專案概觀**頁面上的**取得程式碼**，以選取您的語言。

   您也可以按一下**程式碼**頁面。


### 更新專案以產生新語言
{: #update-language}

1. 從**專案**或**專案概觀**頁面中，按一下**溢位功能表**圖示，然後選取**更新入門範本**。

2. 選取新的語言，然後按一下**更新**。

3. 按一下**專案概觀**頁面上的**取得程式碼**，以選取您的語言。


## 型樣類型
{: #patterns}

雲端原生型樣是經過驗證的設計，有助於確保應用程式的一致、可擴充及可靠的拓蹼。當您建立專案時，會呈現可讓您從中選擇的不同型樣類型。您只要選取要併入專案的型樣類型及功能即可。定義專案喜好設定之後，會產生要編輯、執行或除錯並在本端部署或部署至 {{site.data.keyword.Bluemix}} 的入門範本專案。


### Web 應用程式
{: #web}

Web 專案會將提供 Web 內容（例如 HTML、JavaScript 及樣式表）的能力新增至 Web 伺服器。

下列是可用的 Web 入門範本：

* Basic Web：提供靜態 `index.html` 檔案、預設和空的樣式表，以及 JavaScript 檔案。
* Webpack：建立專案，其中，ECMAScript 6 (ES6) 原始檔位於 `src/client` 且使用 WebPack 進行編譯，讓它們變小並轉換以在瀏覽器中使用。
* Webpack + React：建置使用者介面的豐富架構。原始檔位於 `src/client/app`，並且將使用 WebPack 進行編譯並提供於公用目錄中。


### 行動應用程式
{: #mobile}

行動應用程式型樣可協助您建置直接連接至後端服務（例如 {{site.data.keyword.mobilepushshort}}、{{site.data.keyword.mobileanalytics_short}}、{{site.data.keyword.appid_short}} 等等）的行動應用程式。專案也可以透過 sdkGen（例如 BFF 及 Microservice）予以新增。

您可以從入門範本清單中選擇（例如 {{site.data.keyword.watson}} Conversation、{{site.data.keyword.visualrecognitionshort}}、{{site.data.keyword.openwhisk_short}} 等等）。

您可以在 Swift、Android 或 Cordova 中產生行動應用程式。


### Backend for Frontend (BFF)
{: #bff}

Backend for Frontend 型樣（通稱為 BFF）可協助您聚焦於以符合使用者互動需求的形式公開商業資料及服務。若要最佳化雲端解決方案的使用者行程，則行動應用程式可能需要不同的使用者行程，而 Web 應用程式可能需要更豐富且更詳細的行程。引進 [{{site.data.keyword.conversationfull}} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/conversation.html) 服務這類語音控制裝置，即可透過語音控制與使用者的互動。此數位通道需要極為不同的 BFF 來管理這些語音目的互動。

搭配 {{site.data.keyword.Bluemix_notm}}，您可以使用多國語言進行程式設計方式定義 BFF 來建置 BFF。IBM 建議使用 Node.js、Swift 或 Java，並搭配 Cloud Foundry、Container 服務或無伺服器以雲端原生型樣執行。

BFF 將管理與進行資料持續性、快取之服務的整合，以及與高價值服務（例如 {{site.data.keyword.ibmwatson}}、{{site.data.keyword.iot_short_notm}}、{{site.data.keyword.weather_short}} 以及 {{site.data.keyword.sparks}} 這類資料分析）的整合。

BFF 將公開最常使用 REST 型樣的 API，但您可以使用 {{site.data.keyword.messagehub}} 設計 BFF 來運用傳訊架構。

使用 Node.js 或 Swift 可以使用 BFF Basic 入門範本。


### Microservice
{: #microservice}

Microservice 專案提供用於建置後端微服務（包括基本性能端點：REST API）的基礎。產生的專案將包含微服務本身以及任何連接的雲端服務所需的所有相依關係。

使用 Java 可以使用 Microservice Basic 入門範本。

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


### 語言
{: #languages notoc}

支援的語言為：

   * [Java ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](../runtimes/swift/getting-started.html){: new_window}


#### Java
{: #java notoc}

Java 具有經過驗證的功能可建置企業級應用程式。但是，Java 8 中的新功能與更輕量型的運行環境（例如 Liberty）及架構（例如 Spring Boot）搭配使用，也可讓 Java 更完美地適用於建置微服務。


#### Node.js
{: #node notoc}

Node.js 是一種 JavaScript 運行環境，使用事件驅動、非封鎖 I/O 模型讓它更為輕量且更具效率，對於 Web 應用程式、Backend for Frontend 型樣及微服務的產量及可擴充性最有幫助。Node.js 的套件生態系統 npm 可存取大量的開放程式碼模組，並提供廣泛的功能來加速應用程式開發。


#### Swift
{: #swift notoc}

Swift 是 Apple 在 2014 所建立的現代化程式設計語言，其設計目的是要取代 Objective C 的使用，並在 2015 年 12 月公開開放程式碼。現在，它是用來在使用 x86、ARM 或 Z 架構的 Linux 及 macOS 作業系統上建置 iOS、macOS、Web 服務及系統軟體。它的撰寫方式類似 Scripting 語言，但會進行編譯以獲得類似 C 語言的低額外負擔與高效能，讓它更適用於雲端運行環境。它會使用您在 Java 中看到的強式及靜態類型系統，而不是您在 JavaScript 中看到的功能性樣式及非同步常式。它的效能極高，而且原始檔會使用 LLVM 編譯器工具鏈編譯成原生程式碼，並且可以輕鬆地運用使用 C 所撰寫的外部系統程式庫。


## 入門範本
{: #starters}

使用 {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}，您可以選擇每一個型樣類型的各種入門範本。

「入門範本」已最佳化成可進入正式作業的入門範本程式碼，其著重於示範主要 {{site.data.keyword.Bluemix_notm}} 與高價值服務的整合。每一個入門範本都著重於一項服務，並顯示如何將服務 SDK 整合至程式碼。在某些情況下，入門範本提供簡單的使用者體驗，強調顯示如何整合服務資料或與使用者的互動。每一個入門範本都已配置成啟用鑑別、資料及可能的其他功能（如果您決定為專案配置這些功能）。
