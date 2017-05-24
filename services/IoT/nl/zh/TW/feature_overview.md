---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-12"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} 特性概觀
{: #feature_overview}

{{site.data.keyword.iot_full}} 是以下列重要領域為建置基礎：

  1. 連接 - 連接裝置及開發應用程式。
  2. 資訊管理 - 儲存及檢視裝置資料，以及整合您的 {{site.data.keyword.iot_short_notm}} 與其他服務。
  3. 分析 - 使用 {{site.data.keyword.iot_short_notm}} 儀表板，視覺化即時裝置資料。
  4. 風險管理 - 使用使用者及應用程式的存取控制，配置安全的連線功能及架構。

## 連接
{: #connect}

{{site.data.keyword.iot_short_notm}} 的「連接」是任何 {{site.data.keyword.iot_short_notm}} 服務的起點。連接裝置、建立應用程式、控制您的裝置，以及與協力廠商服務整合，全都位於 {{site.data.keyword.iot_short_notm}} 的「連接」下。

### 閘道裝置

您可以使用閘道，將裝置連接至無法以其他方式連接至網際網路的 {{site.data.keyword.iot_short_notm}}。閘道具有裝置的所有功能，但也可以代表與其連接的裝置進行發佈和訂閱。閘道裝置可讓無法連接至網際網路的感應器群組，藉由將其資料傳送至閘道來連接 {{site.data.keyword.iot_short_notm}}。如需相關資訊，請參閱[為閘道開發](https://console.ng.bluemix.net/docs/services/IoT/gateways/gw_dev_index.html)。

### 裝置管理

裝置管理功能是透過裝置管理 API 以及裝置上安裝的裝置管理代理程式來提供。含有裝置管理代理程式的裝置可以執行裝置管理動作，這些動作可透過主要 {{site.data.keyword.iot_short_notm}} 儀表板或裝置管理 API 來觸發。裝置管理動作包括重新開機、下載和安裝韌體更新，以及將裝置重設為原廠設定。裝置管理也可以延伸，以包含自訂裝置管理動作。如需相關資訊，請參閱[裝置管理文件](https://console.ng.bluemix.net/docs/services/IoT/devices/device_mgmt/index.html)。

### 延伸規格和服務整合

延伸規格和服務整合可讓外部服務和核心服務的使用者定義延伸規格新增至 {{site.data.keyword.iot_short_notm}} 的實例。可與 {{site.data.keyword.iot_short_notm}} 整合的外部服務包括 The Weather Company 的天氣位置服務，讓您能夠在裝置位置、Jasper SIM 資料和 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}} 找到目前的天氣。如需協力廠商服務整合及延伸規格的相關資訊，請參閱[整合外部服務](https://console.ng.bluemix.net/docs/services/IoT/reference/extensions/index.html)。

---

## 資訊管理
{: #information_management}

{{site.data.keyword.iot_short_notm}} 的「資訊管理」可控制裝置在連接 {{site.data.keyword.iot_short_notm}} 服務之後所傳送的資料。資訊管理包含資料儲存與轉換。

### 裝置前次事件快取

您可以使用 {{site.data.keyword.iot_short_notm}} 的「前次事件快取 API」，擷取裝置前次傳送的事件。不論裝置是連線還是離線，此作業皆可運作，如此可讓您擷取裝置狀態，而不管裝置的實體位置或使用狀態。可針對最多 365 天之前發生的任何特定事件，擷取裝置的前次事件資料。

### 裝置事件資料儲存

可以儲存來自 {{site.data.keyword.iot_short_notm}} 服務的裝置事件資料，以供稍後使用。資料儲存是重要的首要步驟，用於執行深入分析，以從該資料取獲得見解。例如，您可以追蹤較長時段的變更並儲存資料集，以便與強大的分析工具搭配使用，包括與 Watson API 及認知運算搭配使用。如需相關資訊，請參閱[連接 {{site.data.keyword.cloudant_short_notm}} 歷程服務](https://console.ng.bluemix.net/docs/services/IoT/cloudant_connector.html)，或[連接 {{site.data.keyword.messagehub}} 歷程服務](https://console.ng.bluemix.net/docs/services/IoT/message_hub.html)。

---

## 分析
{: #analytics}

### 視覺化即時裝置資料

您可以使用儀表板卡，視覺化及顯示即時裝置資料。儀表板卡可以即時監視及顯示裝置資料，如此可讓您追蹤重要裝置或裝置資料。這些視覺化資料會顯示在主要 {{site.data.keyword.iot_short_notm}} 儀表板上，讓您可以快速存取即時裝置資料的環境定義及狀態。如需相關資訊，請參閱[視覺化即時資料](https://console.ng.bluemix.net/docs/services/IoT/data_visualization.html)。

### 邊緣和雲端分析

您可以使用 {{site.data.keyword.iot_short_notm}} 雲端分析，指定以即時裝置資料為依據的規則條件，用來在符合時觸發警示及選用性動作。例如，您可以建立一個規則，以確保當裝置掉落時，或裝置溫度驟升時，將警示傳送至使用者裝置上的儀表板，並將電子郵件傳送給管理者。如需相關資訊，請參閱[雲端分析文件](https://console.ng.bluemix.net/docs/services/IoT/cloud_analytics.html)。

使用邊緣分析，您可以將雲端中的分析規則觸發程序移至啟用邊緣分析功能的閘道，如此即可透過在接近裝置之處進行分析處理，顯著減少傳送至雲端的裝置資料流量。
如需相關資訊，請參閱[邊緣分析文件](https://console.ng.bluemix.net/docs/services/IoT/edge_analytics.html)。

---

## 風險管理
{: #risk_management}

### 安全的連線功能及架構

{{site.data.keyword.iot_short_notm}} 架構的設計可防止裝置假冒其他裝置，如此即可維護裝置資料的完整性。裝置會使用用戶端 ID 與鑑別記號（只有您知道）的組合，來連接至 {{site.data.keyword.iot_short_notm}}。在登錄裝置或產生 API 金鑰之後，鑑別記號是以隨機雜湊方式產生，以維護認證的安全。

「風險與安全管理」附加程式可讓您加強 {{site.data.keyword.iot_short_notm}} 安全，以確保伺服器與裝置之間的所有連接點都以經過驗證的認證進行鑑別。利用此附加程式，除了 {{site.data.keyword.iot_short_notm}} 會使用使用者 ID 和記號，還會使用憑證和傳輸層安全 (TLS) 鑑別。在裝置與伺服器通訊期間，沒有伺服器存取有效憑證的任何裝置（如「風險與安全管理」附加程式所配置），都會被拒絕存取，即使其使用有效的使用者 ID 和密碼也一樣。

---
