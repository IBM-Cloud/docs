---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} 特性概觀
{: #feature_overview}

前次更新：2016 年 6 月 29 日
{: .last-updated}

{{site.data.keyword.iot_full}} 是以下列重要領域為建置基礎：

  1. 連接 - 連接裝置及開發應用程式。
  2. 資訊管理 - 儲存及檢視裝置資料，以及整合您的 {{site.data.keyword.iot_short_notm}} 與其他服務。
  3. 分析 - 使用 {{site.data.keyword.iot_short_notm}} 儀表板，視覺化即時裝置資料。
  4. 風險管理 - 使用使用者及應用程式的存取控制，配置安全的連線功能及架構。

## 連接
{: #connect}

{{site.data.keyword.iot_short_notm}} 的「連接」是任何 {{site.data.keyword.iot_short_notm}} 服務的起點。連接裝置、建立應用程式、控制您的裝置，以及與協力廠商服務整合，全都位於 {{site.data.keyword.iot_short_notm}} 的「連接」下。

### 閘道裝置

您可以使用閘道，將裝置連接至無法以其他方式連接至網際網路的 {{site.data.keyword.iot_short_notm}}。閘道裝置結合了裝置與應用程式的功能。閘道可用與裝置相同的方式接收指令及傳送裝置資料，但是它們也可以將指令傳送至連接至其中的其他裝置，其方式與應用程式相同。

無法直接連接至網際網路的裝置可以連接至閘道裝置，而且其裝置資料可以傳送至閘道裝置，然後可將它傳送至您的 {{site.data.keyword.iot_short_notm}} 服務。

### 裝置管理

「裝置管理」功能是透過下列組合提供的：裝置管理 API 及裝置上安裝的裝置管理代理程式。受管理裝置可以執行裝置管理動作，這些動作可透過主要 {{site.data.keyword.iot_short_notm}} 儀表板觸發。

裝置管理可讓您重新開機、下載並安裝韌體更新項目，以及遠端將裝置重設為原廠設定，全部動作都可從 {{site.data.keyword.iot_short_notm}} 使用者介面執行。

### 協力廠商服務整合

協力廠商服務整合內建至 {{site.data.keyword.iot_short_notm}}，包括 Weather Company 天氣定位服務的支援，可讓您尋找裝置位置的現行天氣。

---

## 資訊管理
{: #information_management}

{{site.data.keyword.iot_short_notm}} 的「資訊管理」可控制裝置在連接 {{site.data.keyword.iot_short_notm}} 服務之後所傳送的資料。資訊管理包括資料儲存與轉換。

### 裝置前次事件快取

您可以使用 {{site.data.keyword.iot_short_notm}} 的「前次事件快取 API」，擷取裝置前次傳送的事件。不論裝置是連線還是離線，此作業皆可運作，如此可讓您擷取裝置狀態，而不管裝置的實體位置或使用狀態。可針對最多 365 天之前發生的任何特定事件，擷取裝置的前次事件資料。

### 裝置事件資料儲存

可以儲存來自 {{site.data.keyword.iot_short_notm}} 服務的裝置事件資料，以供稍後使用。資料儲存是重要的首要步驟，用於執行深入分析，以從該資料取獲得見解。例如，您可以追蹤長時段的變更並儲存資料集，以與強大的分析工具搭配使用，包括與 Watson API 及認知計算搭配使用。

---

## 分析
{: #analytics}

### 視覺化即時裝置資料

您可以使用儀表板卡，視覺化及顯示即時裝置資料。儀表板卡可以即時監視及顯示裝置資料，如此可讓您追蹤重要裝置或裝置資料。這些視覺化資料會顯示在主要 {{site.data.keyword.iot_short_notm}} 儀表板上，讓您可以快速存取即時裝置資料的環境定義及狀態。

---

## 風險管理
{: #risk_management}

### 安全的連線功能及架構

{{site.data.keyword.iot_short_notm}} 架構的設計旨在防止裝置假冒其他裝置，如此即可維護裝置資料的完整性，裝置會使用用戶端 ID 與鑑別記號（只有您知道）的結合，來連接至 {{site.data.keyword.iot_short_notm}}。在登錄裝置或產生 API 金鑰之後，鑑別記號是以隨機雜湊方式產生，以維護認證的安全。完整支援透過 TLS 1.2 版的連線功能。

---
