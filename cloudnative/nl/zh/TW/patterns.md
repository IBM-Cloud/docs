
---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# 型樣類型
{: #patterns}

雲端原生型樣是經過驗證的設計，有助於確保應用程式的一致、可擴充及可靠的拓蹼。當您建立專案時，會呈現可讓您從中選擇的不同型樣類型。您只要選取要併入專案的型樣類型及功能即可。定義專案喜好設定之後，會產生要編輯、執行或除錯並在本端部署或部署至 {{site.data.keyword.Bluemix}} 的入門範本專案。

## Web 應用程式
{: #web}

Web 專案會將提供 Web 內容（例如 HTML、JavaScript 及樣式表）的能力新增至 Web 伺服器。

下列是可用的 Web 入門範本：

* Basic Web：提供靜態 `index.html` 檔案、預設和空的樣式表，以及 JavaScript 檔案。
* Webpack：建立專案，其中，ECMAScript 6 (ES6) 原始檔位於 `src/client` 且使用 WebPack 進行編譯，讓它們變小並轉換以在瀏覽器中使用。
* Webpack + React：建置使用者介面的豐富架構。原始檔位於 `src/client/app`，並且將使用 WebPack 進行編譯並提供於公用目錄中。


## 行動應用程式
{: #mobile}

行動應用程式型樣可協助您建置直接連接至後端服務（例如 {{site.data.keyword.mobilepushshort}}、{{site.data.keyword.mobileanalytics_short}}、{{site.data.keyword.appid_short}} 等等）的行動應用程式。專案也可以透過 sdkGen（例如 BFF 及 Microservice）予以新增。

您可以從入門範本清單中選擇（例如 {{site.data.keyword.watson}} Conversation、{{site.data.keyword.visualrecognitionshort}}、{{site.data.keyword.openwhisk_short}} 等等）。

您可以在 Swift、Android 或 Cordova 中產生行動應用程式。


## Backend for Frontend (BFF)
{: #bff}

Backend for Frontend 型樣（通稱為 BFF）可協助您聚焦於以符合使用者互動需求的形式公開商業資料及服務。若要最佳化雲端解決方案的使用者行程，則行動應用程式可能需要不同的使用者行程，而 Web 應用程式可能需要更豐富且更詳細的行程。引進 [{{site.data.keyword.conversationfull}} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/conversation.html) 服務這類語音控制裝置，即可透過語音控制與使用者的互動。此數位通道需要極為不同的 BFF 來管理這些語音目的互動。

搭配 {{site.data.keyword.Bluemix_notm}}，您可以使用多國語言進行程式設計方式定義 BFF 來建置 BFF。IBM 建議使用 Node.js、Swift 或 Java，並搭配 Cloud Foundry、Container 服務或無伺服器以雲端原生型樣執行。

BFF 將管理與進行資料持續性、快取之服務的整合，以及與高價值服務（例如 {{site.data.keyword.ibmwatson}}、{{site.data.keyword.iot_short_notm}}、{{site.data.keyword.weather_short}} 以及 {{site.data.keyword.sparks}} 這類資料分析）的整合。

BFF 將公開最常使用 REST 型樣的 API，但您可以使用 {{site.data.keyword.messagehub}} 設計 BFF 來運用傳訊架構。

使用 Node.js 或 Swift 可以使用 BFF Basic 入門範本。


## Microservice
{: #microservice}

Microservice 專案提供用於建置後端微服務（包括基本性能端點：REST API）的基礎。產生的專案將包含微服務本身以及任何連接的雲端服務所需的所有相依關係。

使用 Java 可以使用 Microservice Basic 入門範本。

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


## 語言
{: #languages notoc}

支援的語言為：

   * [Java ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](../runtimes/swift/getting-started.html){: new_window}


### Java
{: #java notoc}

Java 具有經過驗證的功能可建置企業級應用程式。但是，Java 8 中的新功能與更輕量型的運行環境（例如 Liberty）及架構（例如 Spring Boot）搭配使用，也可讓 Java 更完美地適用於建置微服務。


### Node.js
{: #node notoc}

Node.js 是一種 JavaScript 運行環境，使用事件驅動、非封鎖 I/O 模型讓它更為輕量且更具效率，對於 Web 應用程式、Backend for Frontend 型樣及微服務的產量及可擴充性最有幫助。Node.js 的套件生態系統 npm 可存取大量的開放程式碼模組，並提供廣泛的功能來加速應用程式開發。


### Swift
{: #swift notoc}

Swift 是 Apple 在 2014 所建立的現代化程式設計語言，其設計目的是要取代 Objective C 的使用，並在 2015 年 12 月公開開放程式碼。現在，它是用來在使用 x86、ARM 或 Z 架構的 Linux 及 macOS 作業系統上建置 iOS、macOS、Web 服務及系統軟體。它的撰寫方式類似 Scripting 語言，但會進行編譯以獲得類似 C 語言的低額外負擔與高效能，讓它更適用於雲端運行環境。它會使用您在 Java 中看到的強式及靜態類型系統，而不是您在 JavaScript 中看到的功能性樣式及非同步常式。它的效能極高，而且原始檔會使用 LLVM 編譯器工具鏈編譯成原生程式碼，並且可以輕鬆地運用使用 C 所撰寫的外部系統程式庫。
