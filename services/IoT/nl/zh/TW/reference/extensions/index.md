---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-02-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 外部服務整合
{: #ref-index}

外部服務整合可讓您從協力廠商或 {{site.data.keyword.iot_full}} 組織中的外部服務存取資料與作業。

## Jasper
{: #jasper}

Jasper 是 SIM 裝置的系統管理和管理平台。Jasper 整合在 {{site.data.keyword.iot_short_notm}} 儀表板中，讓您能夠透過 {{site.data.keyword.iot_short_notm}} 組織儀表板來管理 Jasper 裝置。

### 支援的 Jasper 作業

我們平台所提供的內建 Jasper 整合為下列 Jasper 作業提供支援：

- 檢視整體 Jasper 資料
  - 顯示：狀態、費率方案、月初至今的資料使用情形、月初至今的 SMS 使用情形、月初至今的語音使用情形、超額限制、新增日期和修改日期。
- 變更 SIM 啟動狀態。
  - 從下列項目中選取：庫存、啟動就緒、已啟動、已關閉、已淘汰。
- 檢視 SIM 使用情形
  - 顯示：週期開始日期、可入帳資料和資料總計、可入帳 SMS 和 SMS 總計、可入帳語音和語音總計。
  - 週期開始日期可使用 YYYY-MM-DD 格式來設定。
- 傳送 SMS 至 SIM
- 變更費率方案

完成下列配置步驟之後，您可以在 Jasper 連接裝置的裝置往下探查中，存取支援的作業：

### Jasper 的 REST API
若要存取 Jasper 的 REST API，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部鏈結圖示](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Jasper_Extension){: new_window} 文件中的「Jasper 延伸規格」小節。

### Jasper 的配置

為了能夠將 Jasper 服務連接至 {{site.data.keyword.iot_short_notm}} 組織，必須先完成兩個配置階段。首先，{{site.data.keyword.iot_short_notm}} 必須連接至 Jasper 裝置，然後必須配置 {{site.data.keyword.iot_short_notm}} 裝置。


1. 啟用 Jasper 延伸規格。若要讓 Jasper 與 {{site.data.keyword.iot_short_notm}} 組織整合，請完成下列步驟：
  1. 從 {{site.data.keyword.iot_short_notm}} 儀表板選取**延伸規格**。
  2. 在**延伸規格**頁面中，按一下**新增延伸規格**。
  3. 按一下 Jasper 旁的**新增**。
  4. 輸入 Jasper 使用者名稱、密碼、存取鍵及網域 ID。
  5. 按一下**完成**。

2. 配置您的裝置  
您可以配置同時連接 {{site.data.keyword.iot_short_notm}} 組織和 Jasper 帳戶的裝置，以在 {{site.data.keyword.iot_short_notm}} 儀表板中顯示 Jasper 的資料。  
  
**重要事項：**在「新增裝置」程序中無法套用 Jasper 配置，只有先前已連接的裝置可以用 Jasper 來配置。  
若要配置 Jasper 連接的裝置，請完成下列步驟：
 1. 在 {{site.data.keyword.iot_short_notm}} 儀表板的裝置標籤中，尋找要配置的 Jasper 連接裝置。
 2. 選取裝置，以開啟*裝置往下探查*視圖。
 3. 向下捲動至*延伸配置*。
 4. 使用下列 JSON 格式來輸入延伸配置，然後按一下**確認變更**，以儲存配置。  

```json  
    {
        "jasper": {
            "iccid": "string"
        }
    }

```

順利配置組織之後，*延伸規格*區段會顯示在*裝置往下探查*視圖中的*延伸配置*區段之下。

## AT&T
{: #att}

### 支援的 AT&T 作業

AT&T 延伸規格可讓您執行下列 AT&T 作業：

- 檢視整體 AT&T 資料
  - 顯示：狀態、費率方案、月初至今的資料使用情形、月初至今的 SMS 使用情形、月初至今的語音使用情形、超額限制、新增日期和修改日期。
- 變更 SIM 啟動狀態。
  - 從下列項目中選取：庫存、啟動就緒、已啟動、已關閉、已淘汰。
- 檢視 SIM 使用情形
  - 顯示：週期開始日期、可入帳資料和資料總計、可入帳 SMS 和 SMS 總計、可入帳語音和語音總計。
  - 週期開始日期可使用 YYYY-MM-DD 格式來設定。
- 傳送 SMS 至 SIM
- 變更費率方案

### AT&T 的 REST API
若要存取 AT&T 的 REST API，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部鏈結圖示](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/AT&T_Extension){: new_window} 文件中的「AT&T 延伸規格」小節。

### AT&T 的配置

為了能夠將 {{site.data.keyword.iot_short_notm}} 組織連接至 AT&T，您必須完成組織配置和裝置配置。

若要配置 {{site.data.keyword.iot_short_notm}} 平台，請完成下列步驟。

1. 啟用 AT&T 延伸規格。若要讓 AT&T 與 {{site.data.keyword.iot_short_notm}} 組織整合，請完成下列步驟：
  1. 從 {{site.data.keyword.iot_short_notm}} 儀表板選取**延伸規格**。
  2. 在**延伸規格**頁面中，按一下**新增延伸規格**。
  3. 按一下 AT&T 旁的**新增**。
  4. 輸入 AT&T 使用者名稱、密碼、存取鍵及網域 ID。
  5. 按一下**完成**。

為了能夠將 {{site.data.keyword.iot_short_notm}} 組織與 AT&T 帳戶連接，必須先完成兩個配置階段。先完成組織配置，然後再配置您的裝置。


2. 配置您的裝置  
您可以配置同時連接 {{site.data.keyword.iot_short_notm}} 組織和 AT&T 帳戶的裝置，以在 {{site.data.keyword.iot_short_notm}} 儀表板中顯示 AT&T 的資料。  
  
**重要事項：**在「新增裝置」程序中無法套用 AT&T 配置，只有先前已連接的裝置可以用 AT&T 來配置。  
若要配置 AT&T 連接的裝置，請完成下列步驟：
 1. 在 {{site.data.keyword.iot_short_notm}} 儀表板的裝置標籤中，尋找要配置的 AT&T 連接裝置。
 2. 選取裝置，以開啟*裝置往下探查*視圖。
 3. 向下捲動至*延伸配置*。
 4. 使用下列 JSON 格式來輸入延伸配置，然後按一下**確認變更**，以儲存配置。  

```json  
    {
        "atnt": {
            "iccid": "string"
        }
    }

```

順利配置組織之後，*延伸規格*區段會顯示在*裝置往下探查*視圖中的*延伸配置*區段之下。

## ARM mbed 連接器
{: #arm}

ARM mbed 連接器可讓您將 ARM mbed 裝置連接至 {{site.data.keyword.iot_short_notm}}。ARM mbed 延伸規格容許 ARM mbed 入口網站及 {{site.data.keyword.iot_short_notm}} 傳送及接收來自 ARM mbed 入口網站的資料。

### 設定配置


1. 啟用 ARM mbed 連接器延伸規格。若要啟用 ARM mbed 連接器延伸規格，請完成下列步驟：
  1. 從 {{site.data.keyword.iot_short_notm}} 儀表板選取**設定**，並導覽至**延伸規格**。
  2. 在**延伸規格**功能表中，按一下**新增延伸規格**。
  3. 按一下 ARM mbed 連接器延伸規格旁的**新增**。
  4. 輸入 ARM mbed 存取鍵及網域 ID。您可以使用 ARM mbed 入口網站 https://connector.mbed.com 找到這些項目。
  5. 按一下**檢查連線**按鈕，以檢查認證正確無誤。
  6. 按一下**完成**。

### 有效負載格式

ARM mbed 平台有兩種類型的送入訊息：通知及非同步回應。{{site.data.keyword.iot_short_notm}} 可以將指令傳送給連接至 ARM mbed 平台的裝置。

#### 通知

裝置或感應器資料中的變更會產生通知。{{site.data.keyword.iot_short_notm}} 處理訊息之後，訊息會傳送至裝置事件主題，而且方法與將裝置直接連接至 {{site.data.keyword.iot_short_notm}} 一樣。源自連接至 ARM mbed 平台的裝置的通知所使用的事件類型是 `notify`。

下列程式碼範例顯示 ARM mbed 平台 API 所傳送通知的有效負載格式：

```
{
  "ep":<endpoint/deviceID>,
  "path":<resource path>,
  "ct":<content type>,
  "payload":<Base64 encoded payload>,
  "max-age":<how long the payload is valid, in seconds>
}
```

#### 非同步回應

{{site.data.keyword.iot_short_notm}} 將指令傳送給連接至 ARM mbed 平台的裝置時，裝置會將確認訊息傳送回 {{site.data.keyword.iot_short_notm}}。此確認訊息稱為*非同步回應*，使用事件類型 `asyncResponse`。

下列程式碼範例顯示 ARM mbed 雲端服務所傳送非同步回應的有效負載格式：

```
{
  "id":<transaction id>,
  "status":<200 is command was sucessfully executed. Check other HTTP response codes>,
  "ct":<content type>,
  "max-age":<how long the payload is valid, in seconds>,
  "payload":<base64 encoded payload>,
  "ep":<endpoint/deviceID affected by the command>,
  "path":<resource path affected by the command>
}
```

#### 將指令傳送至 ARM mbed 平台

{{site.data.keyword.iot_short_notm}} 可以將指令傳送給連接至 ARM mbed 平台的裝置。傳送至 ARM mbed 平台的指令必須使用下列 JSON 格式。

```
{
  "method":<PUT or POST>,
  "deviceId":<endpoint/deviceId>,
  "resourceId":<resource path>,
  "payload": <Base64 encoded payload>
}
```
選擇的方法區分大小寫。必須跳過資源路徑的起始 '/'。


有效負載應該發佈至下列主題：

```
iot-2/type/<device_type>/id/<deviceId>/cmd/<command_type>/fmt/<command_format>
```


## Orange
{: #orange}

Orange 延伸規格可讓您檢視連接至 {{site.data.keyword.iot_short_notm}} 並已安裝 Orange SIM 卡之裝置中的 SIM 卡資料。

https://developer.ibm.com/iotplatform/2016/03/30/watson-iot-platform-integration-with-orange-beta/

### 支援的 Orange 作業

如果您的裝置連接至 {{site.data.keyword.iot_short_notm}} 服務，並有 Orange SIM 卡，則您可以使用 Orange 延伸規格來檢視下列 SIM 卡資料：

- SIM 序號
- 啟動狀態
- 前次狀態變更
- 前次狀態重新整理
- 位置狀態

### Orange 的 REST API
若要存取 Orange 的 REST API，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部鏈結圖示](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Orange_Extension){: new_window} 文件中的「Orange 延伸規格」小節。

### Orange 的配置

若要啟用 Orange 延伸規格，請執行下列動作：

1. 從 {{site.data.keyword.iot_short_notm}} 儀表板選取**延伸規格**。
2. 在**延伸規格**頁面中，按一下**新增延伸規格**。
3. 按一下 Orange 延伸規格旁的**新增**。
4. 輸入您的 Orange 使用者名稱和密碼。
6. 按一下**完成**。

啟用 Orange 延伸規格之後，必須配置含有 Orange SIM 卡的每一個裝置，以顯示 Orange SIM 資料。

1. 在 {{site.data.keyword.iot_short_notm}} 儀表板的裝置標籤中，尋找要配置的 Orange SIM 裝置。
2. 選取裝置，然後向下捲動至*延伸配置*。
3. 使用下列 JSON 格式來輸入延伸配置，然後按一下**確認變更**，以儲存配置。

```  
    {
        "orange": {
            "serialnumber": "<serial number of Orange SIM>"
        }
    }

```
順利配置組織之後，*延伸規格*區段會顯示在*裝置往下探查*視圖中的*延伸配置*區段之下。

## 歷程資料儲存
{: #historical_data}

歷程資料儲存延伸規格可讓您尋找及配置 IoT 資料的相容訊息儲存服務（例如 [{{site.data.keyword.cloudantfull}}](../../cloudant_connector.html) 或 [{{site.data.keyword.messagehub_full}}](../../message_hub.html)）。

## 自訂裝置管理套件
{: #device_mgmt}

裝置管理是 {{site.data.keyword.iot_short_notm}} 的核心功能，不過，可加以延伸，以開發其他功能。自訂裝置管理套件必須包含有效的 JSON，並定義至少一個自訂裝置管理動作。

如需自訂裝置管理功能（包括所需 JSON 格式的範例）的相關資訊，請參閱[裝置管理自訂延伸規格](../../devices/device_mgmt/custom_actions.html){: new_window}。

### 新增自訂裝置管理套件

使用 {{site.data.keyword.iot_short_notm}} 儀表板，或使用 API，即可新增自訂裝置管理套件。

若要使用 {{site.data.keyword.iot_short_notm}} 儀表板新增自訂裝置管理套件，請執行下列動作：

1. 從 {{site.data.keyword.iot_short_notm}} 儀表板中，按一下導覽列中的**設定**。
2. 按一下**自訂裝置管理套件**。
3. 按一下**新增套件**按鈕。
4. 選取套件檔，然後按一下**開啟**。

若要使用 API 新增自訂裝置管理套件，請參閱 [{{site.data.keyword.iot_short_notm}} API 文件 ![外部鏈結圖示](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}。

## 區塊鏈
{: #blockchain}

{{site.data.keyword.iot_short_notm}} 與區塊鏈可讓 IoT 裝置提供資料給區塊鏈交易，區塊鏈交易會將資料儲存在區塊鏈的不可變分類帳中，並將它用在智慧型合約商業規則中。{{site.data.keyword.iot_short_notm}} 會將裝置資料對映成區塊鏈智慧型合約所需的資料格式，並將它傳遞至區塊鏈網狀架構，以儲存在區塊鏈分類帳中。

### 支援的區塊鏈作業
- 以裝置事件來觸發智慧型合約更新。
- 執行智慧型合約商業邏輯，使用裝置事件資料來更新分類帳狀態。
- 使用監視使用者介面來監視區塊鏈、交易和分類帳狀態。

### 區塊鏈的配置

{{site.data.keyword.iot_short_notm}} 區塊鏈整合是 {{site.data.keyword.iot_short_notm}} 中預設不啟動的服務供應項目。若要在組織中啟動此特性，請完成下列步驟：
 1. 從 {{site.data.keyword.iot_short_notm}} 儀表板選取**延伸規格**。
 2. 在**延伸規格**頁面中，按一下**新增延伸規格**。
 3. 按一下 Blockchain 延伸規格旁的**新增**。
 4. 在 Blockchain 磚中，按一下**設定**。
 3. 在**啟動 Blockchain** 區段中，按一下**進一步瞭解**鏈結，以移至 [IoT 區塊鏈服務供應項目頁面 ![外部鏈結圖示](../../../../icons/launch-glyph.svg)](http://www.ibm.com/internet-of-things/iot-news/announcements/private-blockchain/){: new_window}。
 4. 按一下**開始區塊鏈專案**進行填寫，並提交*探索潛在的 IoT 及區塊鏈* 表單。  
 5. 核准要求之後，IBM 將會聯絡您以啟用組織的區塊鏈整合。
 6. 回到組織的 {{site.data.keyword.iot_short_notm}} 儀表板，遵循 [{{site.data.keyword.iot_short_notm}} 區塊鏈整合](../../bl_blockchain_integration.html)中的步驟來完成設定。



## The Weather Company
{: #weathercompany}

The Weather Company 延伸規格結合天氣資料與現有 {{site.data.keyword.iot_short_notm}} 裝置。如果已使用 API 提出更新位置要求，或裝置已使用裝置管理訊息設定其位置，則 The Weather Company 的天氣資料會出現在裝置詳細資料視圖中。

**附註：**只有受管理裝置才能設定其專屬位置。所有未受管理裝置都必須使用 API 手動設定其位置。如需設定裝置位置的相關資訊，請參閱[更新位置要求](../../devices/device_mgmt/index.html#update-location)。

### The Weather Company 的 REST API
若要存取 The Weather Company 的 REST API，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部鏈結圖示](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather){: new_window} 文件中的「裝置位置天氣」小節。

### 天氣資料

若要檢視針對裝置位置所擷取的天氣資料，請在**裝置**窗格中尋找裝置，然後按一下它。在詳細裝置視圖中，向下捲動至**延伸規格**區段。即會列出下列天氣資料：

- 現行天氣。
- 現行溫度。
- 預測最高溫度及最低溫度。
- 相對濕度。
- 壓力。
- 能見度。
- 風速。
- 風向。
- 緯度。
- 經度。

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html){: new_window}. -->
