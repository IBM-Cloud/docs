---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 常見使用案例
{: #openwhisk_common_use_cases}

{{site.data.keyword.openwhisk_short}} 所提供的執行模型支援各種使用案例。下列各節包括一般範例。如需「無伺服器」架構、範例使用案例、正反雙方討論及實作最佳作法的更詳細討論，請閱讀出色的 [Martin Fowler 部落格上的 Mike Roberts 文章](https://martinfowler.com/articles/serverless.html)。
{: shortdesc}

## 微服務
{: #openwhisk_common_use_cases_microservices}

無論其好處為何，微服務型解決方案都很難使用主流雲端技術進行建置，這通常需要控制複式工具鏈、不同的建置及作業管線。花太多時間來處理基礎架構及作業複雜性（容錯、負載平衡、自動擴充及記載）的小型及敏捷團隊，尤其想要有一種方式可以使用已知、愛用且最適合解決特定問題的程式設計語言來開發有效率且具有附加價值的程式碼。

{{site.data.keyword.openwhisk_short}} 的模組及固有的可擴充本質，讓它適用於實作動作中邏輯的精細部分。{{site.data.keyword.openwhisk_short}} 動作彼此無關，因此可以使用 {{site.data.keyword.openwhisk_short}} 所支援的各種不同語言進行實作，以及存取各種後端系統。每一個動作都可以個別進行部署及管理，與其他動作分開進行擴充。動作之間的交互連線是由 {{site.data.keyword.openwhisk_short}} 透過規則、序列及命名慣例形式所提供。這十分適用於微服務型應用程式。

{{site.data.keyword.openwhisk_short}} 的另一個重要引數，就是災難回復配置中的系統成本。我們將使用 PaaS 或 CaaS 的微服務與使用 {{site.data.keyword.openwhisk_short}} 進行比較。假設我們有 10 個使用容器或 CloudFoundry 運行環境的微服務，單一可用性區域中有 10 個持續執行且可入帳的處理程序，跨 2 個 AZ 執行時就有 20 個處理程序，跨 2 個各有 2 個區域的地區執行時就有 40 個處理程序。在 {{site.data.keyword.openwhisk_short}} 中執行微服務來進行相同的作業時，您要跨多少 AZ 和地區來執行微服務都可以，而且不需要支付任何增量成本。

[Logistics Wizard](https://www.ibm.com/blogs/bluemix/2017/02/microservices-multi-compute-approach-using-cloud-foundry-openwhisk/) 是企業級範例應用程式，其運用 {{site.data.keyword.openwhisk_short}} 和 CloudFoundry 來建置 12 因素樣式的應用程式。這是一個智慧型供應鏈管理解決方案，其目的是要模擬執行 ERP 系統的環境。其以應用程式來擴增此 ERP 系統，以提升供應鏈管理員的可見性和靈活性。

## Web 應用程式
{: #openwhisk_common_use_cases_webapps}

基於 {{site.data.keyword.openwhisk_short}} 的事件導向本質，它為使用者應對應用程式提供多項好處，而從使用者瀏覽器提出的 HTTP 要求則作為事件。{{site.data.keyword.openwhisk_short}} 應用程式使用運算能力，而且只有在負責處理使用者要求時，才會計費。並沒有閒置待命或等待模式這種東西。這讓 {{site.data.keyword.openwhisk_short}} 成本遠低於傳統容器或 CloudFoundry 應用程式，後兩者可能有大部分時間都只是在等待送入的使用者要求，而整個「休眠」時間都會計費。 

使用 {{site.data.keyword.openwhisk_short}} 可以建置及執行完整的 Web 應用程式。合併無伺服器 API 與網站資源的靜態檔案管理（例如 HTML、JavaScript 及 CSS），表示我們可以建置整個無伺服器 Web 應用程式。相較於使用及操作 Node.js Express 或其他傳統伺服器運行環境，操作 {{site.data.keyword.openwhisk_short}} 管理環境的簡化（或者，在 Bluemix 上管理之後，根本不需要任何操作）是一個很重要的優點。

以下是一些如何使用 {{site.data.keyword.openwhisk_short}} 來建置 Web 應用程式的範例：
- [Web 動作：使用 {{site.data.keyword.openwhisk_short}} 的無伺服器 Web 應用程式](https://medium.com/openwhisk/web-actions-serverless-web-apps-with-openwhisk-f21db459f9ba)。
- [使用 Bluemix 及 Node.js 建置使用者應對 {{site.data.keyword.openwhisk_short}} 應用程式](https://www.ibm.com/developerworks/cloud/library/cl-openwhisk-node-bluemix-user-facing-app/index.html)
- [使用 {{site.data.keyword.openwhisk_short}} 的無伺服器 HTTP 處理程式](https://medium.com/openwhisk/serverless-http-handlers-with-openwhisk-90a986cc7cdd)

## IoT
{: #openwhisk_common_use_cases_iot}

Internet of Things 情境本質上經常是由感應器所驅動。例如，如果需要針對感應器超過特定溫度做出反應，可能會觸發 {{site.data.keyword.openwhisk_short}} 中的動作。如果發生主要事件（自然災害、重大天氣事件、塞車等），則 IoT 互動通常是可能會有極高負載層次的無狀態。這會需要正常工作負載小的彈性系統，但需要使用可預測的回應時間以及處理極大量不會事先警告系統的事件的能力來極快速進行擴充。很難使用傳統伺服器架構來建置符合這些需求的系統，因為它們很容易動力不足而無法處理資料流量尖峰，或過量供應且極為昂貴。

肯定可以使用傳統伺服器架構來實作 IoT 應用程式，不過，在許多情況下，不同服務與資料橋接器的組合需要高效能及彈性管線，範圍從 IoT 裝置到雲端儲存空間及分析平台。預先配置的橋接器通常會缺乏實作及細部調整特定解決方案架構所需的程式設計性。如果有大量各種可能的管線，而且一般會缺乏資料合併的標準化，特別是在 IoT 中，在許多情況下，管線會需要自訂資料轉換（進行格式轉換、過濾、擴增等）。{{site.data.keyword.openwhisk_short}} 是一個可使用「無伺服器」方式來實作這類轉換的傑出工具，其中，自訂邏輯是在完整受管理及彈性的雲端平台上進行管理。

以下是使用 {{site.data.keyword.openwhisk_short}}、NodeRed、Cognitive 及其他服務的範例 IoT 應用程式：[使用 {{site.data.keyword.openwhisk_short}} 進行 IoT 動態資料的無伺服器轉換](https://medium.com/openwhisk/serverless-transformation-of-iot-data-in-motion-with-openwhisk-272e36117d6c#.akt3ocjdt)。

![IoT 解決方案架構範例](images/IoT_solution_architecture_example.png)

## API 後端
{: #openwhisk_common_use_cases_iot}

無伺服器運算平台可讓開發人員在沒有伺服器的情況下快速建置 API。{{site.data.keyword.openwhisk_short}} 支援自動產生 REST API 來執行動作。{{site.data.keyword.openwhisk_short}} 的這個[實驗性特性](./apigateway.md)可讓您使用 POST 以外的 HTTP 方法來呼叫動作，而不需要動作的授權 API 金鑰（透過「{{site.data.keyword.openwhisk_short}} API 閘道」）。此功能不僅有助於向外部消費者顯現 API，也有助於建置微服務應用程式。

此外，{{site.data.keyword.openwhisk_short}} 動作還可以連接至所選擇的「API 管理」工具（例如 [IBM API Connect](https://www-03.ibm.com/software/products/en/api-connect) 或其他工具）。與其他使用案例類似，適用可擴充性的所有考量以及其他「服務品質 (QoS)」。 

[Emoting](https://github.com/l2fprod/openwhisk-emoting) 是透過 REST API 使用 {{site.data.keyword.openwhisk_short}} 動作的範例應用程式。

以下是[使用無伺服器作為 API 後端](https://martinfowler.com/articles/serverless.html#ACoupleOfExamples)的範例及討論。

## 行動後端
{: #openwhisk_common_use_cases_mobile}

許多行動應用程式都需要伺服器端邏輯。由於行動開發人員通常對管理伺服器端邏輯沒什麼經驗，而比較專注在裝置上執行的應用程式，因此，使用 {{site.data.keyword.openwhisk_short}} 作為伺服器端後端是很好的解決方案。此外，伺服器端 Swift 的內建支援可讓開發人員重複使用其現有 iOS 程式設計技術。行動應用程式通常會有無法預期的負載型樣，而且受管理的 {{site.data.keyword.openwhisk_short}} 解決方案（例如 IBM Bluemix）可以調整以特別符合任何工作負載需求，而不需要事先佈建資源。

[Skylink](https://github.com/IBM-Bluemix/skylink) 是一個範例應用程式，可讓您透過 iPad 將無人機連接至 IBM Cloud，運用 {{site.data.keyword.openwhisk_short}}、IBM Cloudant、IBM Watson 和 Alchemy Vision，進行近乎即時的影像分析。

[BluePic](https://github.com/IBM-Swift/BluePic) 是一種照片和影像分享應用程式，可讓您拍攝照片並與其他 BluePic 使用者分享。此應用程式示範如何在 iOS 10 行動應用程式中，運用以 Swift 撰寫、使用 {{site.data.keyword.openwhisk_short}}、Cloudant、Object Storage 來處理影像資料的 Kitura 型伺服器應用程式。AlchemyAPI 也可以用在 {{site.data.keyword.openwhisk_short}} 序列來分析影像，並根據影像內容來擷取文字標籤，然後傳送推送通知給使用者。

## 資料處理
{: #openwhisk_common_use_cases_data}

運用現在可用的資料量，應用程式開發需要處理新資料的能力，而且可能會對它做出反應。此需求包括處理結構化資料庫記錄以及非結構化文件、映像檔或視訊。{{site.data.keyword.openwhisk_short}} 可以透過系統提供的或自訂資訊來源進行配置來反應資料變更，以及自動對送入的資料資訊來源執行動作。您可以對動作進行程式設計，以處理變更、轉換資料格式、傳送及接收訊息、呼叫其他動作，以及更新各種資料儲存庫（包括 SQL 型關聯式資料庫、記憶體內資料網格、NoSQL 資料庫、檔案、訊息分配管理系統及各種其他系統）。{{site.data.keyword.openwhisk_short}} 規則及序列提供彈性可在處理管線時進行變更，而不需要進行程式設計 - 只需要透過配置變更即可。這讓 {{site.data.keyword.openwhisk_short}} 型系統具備高度敏捷，並且可輕鬆地適應不斷變化的需求。

[OpenChecks](https://github.com/krook/openchecks) 專案是一種概念證明，示範如何利用光學字元辨識，使用 {{site.data.keyword.openwhisk_short}} 來處理存入銀行帳戶的支票存款。其目前建置在公用 Bluemix {{site.data.keyword.openwhisk_short}} 服務上，需依賴 Cloudant 和 SoftLayer Object Storage。在內部部署中，它可以使用 CouchDB 和 OpenStack Swift。其他儲存服務還包括 FileNet 或 Cleversafe。Tesseract 提供 OCR 檔案庫。
## 認知
{: #openwhisk_common_use_cases_cognitive}

認知技術可以有效率地與 {{site.data.keyword.openwhisk_short}} 合併，以建立功能強大的應用程式。例如，IBM Alchemy API 及 Watson Visual Recognition 可以與 {{site.data.keyword.openwhisk_short}} 搭配使用，自動從視訊擷取有用的資訊，而不需要實際觀看它們。這可以只是先前討論之[資料處理](#data-processing)使用案例的「認知」延伸。{{site.data.keyword.openwhisk_short}} 另一個很好的用法，就是實作與認知服務結合的 Bot 功能。 

以下是只執行該作業的範例應用程式 [Dark Vision](https://github.com/IBM-Bluemix/openwhisk-darkvisionapp)。在此應用程式中，使用者會使用 Dark Vision Web 應用程式來上傳視訊或影像，這會將它儲存在 Cloudant DB 中。上傳視訊之後，{{site.data.keyword.openwhisk_short}} 會接聽 Cloudant 變更（觸發程式）來偵測新視訊。{{site.data.keyword.openwhisk_short}} 接著會觸發視訊擷取程式動作。在其執行期間，擷取程式會產生訊框（影像），並將它們儲存在 Cloudant 中。然後，會使用 Watson Visual Recognition 來處理訊框，而且結果會儲存在相同的 Cloudant DB 中。可以使用 Dark Vision Web 應用程式或 iOS 應用程式來檢視結果。除了 Cloudant 之外，還可以使用 Object Storage。這麼做時，視訊及影像 meta 資料會儲存在 Cloudant 中，而媒體檔案會儲存在 Object Storage 中。

這裡有一個 [iOS Swift 應用程式範例](https://github.com/gconan/BluemixMobileServicesDemoApp)，示範 {{site.data.keyword.openwhisk_short}}、IBM Mobile Analytics、Watson 分析音調並張貼至 Slack 頻道。

## 使用 Kafka 或 Message Hub 來處理事件 

{{site.data.keyword.openwhisk_short}} 非常適合與 Kafka、IBM Message Hub（Kafka 型）及其他傳訊系統組合使用。這些系統的事件導向本質需要有事件導向的運行環境才能處理訊息，並將商業邏輯套用至那些訊息，這其實就是 {{site.data.keyword.openwhisk_short}} 隨著其資訊來源、觸發程式、動作等等提供的功能。Kafka 和 Message Hub 通常會用於非常大且無法預期的工作量，需要那些訊息的消費者一接到通知就能擴充，而這又是 {{site.data.keyword.openwhisk_short}} 的一大優點。{{site.data.keyword.openwhisk_short}} 具有內建功能，可以耗用訊息，也可以發佈 [openwhisk-package-kafka](https://github.com/openwhisk/openwhisk-package-kafka) 套件中提供的訊息。

這裡有一個[實作事件處理程序情境的應用程式範例](https://github.com/IBM/openwhisk-data-processing-message-hub)，搭配使用 {{site.data.keyword.openwhisk_short}}、Message Hub 及 Kafka。
