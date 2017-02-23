---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 閘道的 MQTT 連線功能
{: #mqtt}

MQTT 是裝置及應用程式用來與 {{site.data.keyword.iot_full}} 通訊的主要通訊協定。我們提供了用戶端程式庫、資訊及範例，以協助您使用 MQTT 用戶端作為閘道，將裝置連接至 {{site.data.keyword.iot_short_notm}}。
{:shortdesc}

## 用戶端連線
{: #client_connections}

如需用戶端安全以及如何連接 MQTT 用戶端作為閘道的相關資訊，請參閱[將應用程式、裝置及閘道連接至 {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html)。

## MQTT 鑑別
{: #authentication}
對於閘道和裝置，{{site.data.keyword.iot_short_notm}} 會使用 MQTT 記號型鑑別。

若要啟用 MQTT 鑑別，請在建立 MQTT 連線時，提交使用者名稱和密碼。

### 使用者名稱
{: #username}

所有閘道的使用者名稱值皆相同：`use-token-auth`。這個值會使 {{site.data.keyword.iot_short_notm}} 使用閘道的鑑別記號（已指定作為密碼）。

### 密碼
{: #password}

每一個閘道的密碼都是向 {{site.data.keyword.iot_short_notm}} 登錄閘道時所產生的唯一鑑別記號。

## 發佈事件
{: #pub_events}

閘道可以發佈其本身的事件，也可以代表透過該閘道連接的任何裝置來發佈事件。若要發佈事件，請根據所想要的事件來源，使用下列主題，並替換適當的 `typeId` 和 `deviceId`：

<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/evt/<var class="keyword varname">eventId</var>/fmt/<var class="keyword varname">formatString</var></pre>
{: codeblock}


**範例**


|    |'typeID'|'deviceID'|
|:---|:---|:---|
|閘道 1 |mygateway |gateway1 |
|裝置 1 |mydevice |device1 |

-   「閘道 1」可以發佈自己的狀態事件：
      
    `iot-2/type/mygateway/id/gateway1/evt/status/fmt/json`
-   「閘道 1」可以代表「裝置 1」發佈狀態事件：
      
    `iot-2/type/mydevice/id/device1/evt/status/fmt/json`

**重要事項：**訊息有效負載上限為 131072 個位元組。大於此限制的訊息都會被拒絕。

### 保留的訊息
{{site.data.keyword.iot_short_notm}} 組織未獲授權，無法發佈保留的 MQTT 訊息。如果閘道傳送保留的訊息，則 {{site.data.keyword.iot_short_notm}} 服務會置換設為 true 的保留的訊息旗標，而且處理訊息的方式就像保留的訊息旗標設為 false 一樣。

## 訂閱指令
{: #subscribing_cmds}

閘道可以訂閱導向閘道本身的指令，以及導向組織中任何裝置（包括其他閘道）的指令。若要訂閱指令，請使用下列主題，並替換適當的 `typeId` 和 `deviceId`：

<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/cmd/<var class="keyword varname">commandId</var>/fmt/<var class="keyword varname">formatString</var></pre>
{: codeblock}

MQTT `+` 萬用字元可用來讓 `typeId`、`deviceId`、`commandId` 和 `formatString` 訂閱多個指令來源。

**範例：**

|裝置 |`typeId`|`deviceId`|
|:---|:---|
|閘道 1| mygateway   | gateway1   |
|裝置 1 | mydevice    | device1    |


-   「閘道 1」可以訂閱導向閘道的指令：
      
    `iot-2/type/mygateway/id/gateway1/cmd/+/fmt/+`
-   「閘道 1」可以訂閱傳送至「裝置 1」的指令：
      
    `iot-2/type/mydevice/id/device1/cmd/+/fmt/+`
-   「閘道 1」可以訂閱傳送至 `mydevice` 類型之裝置的任何指令：  
     `iot-2/type/mydevice/id/+/cmd/+/fmt/+`

**重要事項：**指定為 `cleansession=false` 的 MQTT 持續性階段作業，不會搜尋連接至閘道的裝置。如果裝置連接至閘道 A，之後又連接至閘道 B，則它不會收到在其中斷連線時針對該裝置發佈到閘道 A 的任何訊息。閘道擁有 MQTT 用戶端和訂閱，但不擁有連接至閘道的裝置。

## 閘道自動登錄
{: #auto-reg}

閘道裝置可以自動登錄與其連接的裝置。當閘道代表已取消登錄的裝置發佈訊息或訂閱主題時，就會自動登錄該裝置。

閘道裝置提出的登錄要求節流控制為一次 128 個擱置要求。嘗試連接許多新裝置，可能會導致透過閘道登錄裝置時發生延遲。

**警告**

如果閘道無法自動登錄裝置，則短時間內不會再嘗試登錄該裝置。來自失敗裝置的任何訊息或訂閱都會在當時捨棄。

## 閘道通知
{: #notification}

若在驗證發佈或訂閱主題期間或是在自動登錄期間發生錯誤，則會傳送通知給閘道裝置。閘道可以透過訂閱下列主題、替換 `typeId` 和 `deviceId` 值，來接收這些通知：

```
iot-2/type/**typeId**/id/**deviceId**/notify
```
<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/notify</pre>
{: codeblock}

在通知主題收到的訊息使用下列格式：

```   
{
   "Request": "<Request_Type>",
   "Time": "<Timestamp>",
   "Topic": "<Topic>",
   "Type": "<Device_Type>",
   "Id": "<Device_Id>",
   "Client": "<Client_ID>",
   "RC": "<Return_Code>",
   "Message": "<Message>"
}
```
其中
-   `Request_Type` 值是 `publish` 或 `subscribe`
-   `Timestamp` 是 ISO 8601 格式的時間
-   `Topic` 是來自閘道的要求主題
-   `Device_Type` 是來自主題的裝置類型
-   `Device_Id` 是來自主題的裝置 ID
-   `Client_ID` 是要求的用戶端 ID
-   `Return_Code` 是回覆碼
-   `Message` 是錯誤訊息

閘道可以接收下列通知：

-   主題不符合任何容許的主題規則。
-   裝置類型無效。
-   裝置 ID 無效。
-   已達到每個閘道的裝置數上限。
-   已達到每個組織的裝置數上限。
-   因為發生內部錯誤，而無法建立裝置。

## 受管理閘道
{: #managed_gateways}

對裝置生命週期管理的支援是選用性的。{{site.data.keyword.iot_short_notm}} 所使用的裝置管理通訊協定，使用與閘道用於事件和指令控制的相同 MQTT 連線。

### 服務品質水準及全新階段作業
{: #quality_service}

受管理閘道可以發佈服務品質 (QoS) 水準為 0 或 1 的訊息。

QoS=0 的訊息可以捨棄，而且在傳訊伺服器重新啟動之後，不會持續保存。QoS=1 的訊息可以置入佇列，而且在傳訊伺服器重新啟動之後，會持續保存。訂閱的延續性會決定是否將要求置入佇列。用來訂閱之連線的 `cleansession` 參數會決定訂閱的延續性。  

{{site.data.keyword.iot_short_notm}} 會發佈 QoS 水準為 1 的要求，以支援訊息的佇列作業。若要將受管理閘道未連線時所傳送的訊息置入佇列，請將 `cleansession` 參數設為 false，以將裝置配置為不使用全新階段作業。

**警告**

受管理閘道使用可延續訂閱時，如果閘道未於要求逾時之前重新連接至服務，則會將閘道離線時傳送至其中的裝置管理指令報告為失敗的作業。當閘道重新連接時，閘道即會處理那些要求。可延續訂閱是由 `cleansession=false` 參數指定。

不論閘道後面有哪些裝置，閘道都擁有 MQTT 階段作業。當裝置透過閘道提交訂閱要求時，不論是否設定 `cleansession=false` 選項，該要求都不會漫遊至其他閘道。

### 主題
{: #topics}

受管理閘道必須訂閱下列主題，才能處理來自 {{site.data.keyword.iot_short_notm}} 的要求和回應：

-   受管理閘道訂閱裝置管理回應的位置：  
<pre class="pre">iotdm-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/response/+</pre>
{: codeblock}
-   受管理閘道訂閱裝置管理要求的位置：  
<pre class="pre">iotdm-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/+</pre>
{: codeblock}

受管理閘道會發佈下列回應和要求：

- 裝置管理回應發佈在：  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/response/</pre>
{: codeblock}
- 裝置管理要求發佈在：  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/</pre>
{: codeblock}

閘道可以使用相關的 **typeId** 和 **deviceId**，為自己以及代表其他連接的裝置來處理「裝置管理通訊協定」訊息。

### 訊息格式
{: #msg_format}

所有訊息都會以 JSON 格式傳送。

**要求**

要求會格式化，如下列程式碼範例所示：

```   
    {  "d": {...}, "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056" }
```

-   `d` 負載與要求相關的任何資料
-   `reqId` 是要求的 ID，必須複製到回應中。如果回應不是必要項目，則不使用此欄位。

**回應**

回應會格式化，如下列程式碼範例所示：

```
    {
        "rc": 0,
        "message": "success",
        "d": {...},
        "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056"
    }
```
其中：
-   `rc` 是原始要求的結果碼。
-   `message` 是含有回應碼文字說明的選用性元素。
-   `d` 是隨附於回應的選用性資料元素。
-   `reqId` 是原始要求的要求 ID。要求 ID 可用來讓回應與要求產生關聯，而裝置需要確保所有要求 ID 都是唯一的。{{site.data.keyword.iot_short_notm}} 要求的回應必須包含正確的 `reqId` 值。
