---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 關於
{: #about}

使用 {{site.data.keyword.streaminganalyticsfull}}，即可對動態資料執行即時分析，以作為 {{site.data.keyword.Bluemix_short}} 應用程式的一部分。
{:shortdesc}

第一次使用 {{site.data.keyword.streaminganalyticsshort}}？請取得[服務的快速簡介](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix-2/){:new_window}。

{{site.data.keyword.streaminganalyticsshort}} 服務提供下列功能，讓您能部署、分析及監視雲端中的資料：

**透過互動和程式設計方式使用服務：**

您可以透過 [{{site.data.keyword.streaminganalyticsshort}} 主控台](/docs/services/StreamingAnalytics/c_streams_console.html)以互動方式使用服務，或透過 [{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220){:new_window} 以程式設計方式使用服務。

**部署及監視 SPL、Java、Scala 及 Python 應用程式：**

您可以用 SPL、Java、Scala 及 Python 撰寫 {{site.data.keyword.streamsshort}} 應用程式。使用 {{site.data.keyword.streaminganalyticsshort}} 主控台[部署及監視這些應用程式](/docs/services/StreamingAnalytics/t_deploytocloud.html)。

如果您想要以 SPL 撰寫應用程式，您應該知道 {{site.data.keyword.streamsfull}} Processing Language (SPL) 是一種程式設計語言，用來建立串流處理應用程式。如果要進一步使用您自己的 SPL 應用程式，可以取得 {{site.data.keyword.streamsshort}} 開發環境，而且 SPL 應用程式必須準備好使用雲端。

若要建立及部署 Python 應用程式而不使用 {{site.data.keyword.streamsshort}} 開發環境，請使用 IBM Data Science Experience (DSX) 中的記事本或 {{site.data.keyword.streamsshort}} Python API。如需相關資訊，請參閱[針對 {{site.data.keyword.streaminganalyticsshort}} 開發 Python 應用程式](/docs/services/StreamingAnalytics/t_develop_apps_python.html)。

**與 {{site.data.keyword.streamsshort}} 運算子的相容性：**

[{{site.data.keyword.streamsshort}} Processing Language (SPL) 標準工具箱中的 {{site.data.keyword.streamsshort}} 運算子](/docs/services/StreamingAnalytics/c_beta_adapters.html)應該全部與 {{site.data.keyword.streaminganalyticsshort}} 相容。

## {{site.data.keyword.streaminganalyticsfull}} 責任
{: #responsibilities notoc}

### 用戶端責任
{: #clientresponsibilities notoc}

「用戶端」負責：

* 遵循 IBM 起始配置 {{site.data.keyword.streamsshort}}、監視、配置及管理在其實例中執行的 {{site.data.keyword.streamsshort}} 工作。用戶端具有彈性可啟動及停止實例，以及啟動與停止實例上執行的工作。
* 依需要或必要，開發服務上的程式及應用程式來分析資料，以及瞭解它。用戶端也負責這類所開發程式或應用程式的品質及效能。使用 {{site.data.keyword.streamsshort}} Topology 特性，即可透過 SPL、Java 或其他支援語言來開發程式。其編譯方式必須搭配使用 {{site.data.keyword.streamsshort}} Developer Edition 或 {{site.data.keyword.streamsshort}} Quick Start Edition 與用於 {{site.data.keyword.streaminganalyticsshort}} 的相同作業系統。
* 定期檢查下列鏈結，以收到有關所排程非干擾性或干擾性關閉時間的通知 - [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window}  
* 根據商業需求來備份所有資料、meta 資料、配置檔及環境參數，以確保持續性。
* 基於任何類型的失敗（故障）（包括但不限於資料中心或 Pod 失敗、伺服器故障或硬碟故障或軟體失敗），而還原任何備份中的資料、meta 資料、配置檔及環境參數，以確保持續性。

### IBM 責任
{: #ibmresponsibilities notoc}

身為 {{site.data.keyword.streaminganalyticsfull}} 的一部分，IBM 將：

* 提供與管理 Customer 實例的伺服器、儲存空間及網路基礎架構。
* 對所選取的節點數，提供 {{site.data.keyword.streamsshort}} 起始配置。
* 提供與管理網際網路面向及內部防火牆的基礎架構，以進行保護和隔離。
* 在 {{site.data.keyword.streaminganalyticsfull}} 上監視及管理下列元件：
	* 網路元件
	* 伺服器及其本端儲存空間
	* 基礎架構作業系統
	* {{site.data.keyword.streamsshort}} 管理服務
	* {{site.data.keyword.streamsshort}} 實例
* 提供維護修補程式，包括基礎架構作業系統及 {{site.data.keyword.streamsshort}} 的適當安全修補程式。
* 執行應該不需要任何系統關閉時間（「非干擾性」維護）的一般維護，以及將會在 [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window} 發佈的排程時間執行且可能需要一些系統關閉時間及重新啟動的維護（「干擾性」維護）
* 將會張貼任何對排程維護時間進行的變更以及適當的注意事項。
