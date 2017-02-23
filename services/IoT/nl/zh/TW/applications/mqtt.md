---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 應用程式的 MQTT 連線功能
{: #mqtt}

MQTT 是裝置及應用程式用來與 {{site.data.keyword.iot_full}} 通訊的主要通訊協定。我們提供了用戶端程式庫、資訊及範例，以協助您連接及整合 {{site.data.keyword.iot_short_notm}} 應用程式。
{:shortdesc}

## 用戶端連線
{: #client_connections}

如需用戶端安全以及如何將 MQTT 用戶端連接至 {{site.data.keyword.iot_short_notm}} 中應用程式的相關資訊，請參閱[將應用程式、裝置及閘道連接至 {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html)。

## MQTT 鑑別
{: #mqtt_authentication}

{{site.data.keyword.iot_short_notm}} 應用程式需要有 API 金鑰才能連接至組織。登錄 API 金鑰時，會產生必須與該 API 金鑰搭配使用的鑑別記號。

下列範例顯示一般 API 金鑰：

<pre class="pre">a-<var class="keyword varname">orgId</var>-a84ps90Ajs</pre>
{: codeblock}


下列範例顯示一般鑑別記號：

```
MP$08VKz!8rXwnR-Q*
```

當您使用 API 金鑰建立 MQTT 連線時，請確定套用下列準則：

- MQTT 用戶端 ID 的格式為：a:*orgId*:*appId*
- MQTT 使用者名稱是 API 金鑰（例如，a-*orgId*-a84ps90Ajs）
- MQTT 密碼是鑑別記號（例如，MP$08VKz!8rXwnR-Q*）


## 發佈裝置事件
{: #publishing_device_events}

應用程式可以發佈事件，就彷彿事件是來自任何已登錄的裝置一樣，例如：

-  發佈至主題 iot-2/type/*device_type*/id/*device_id*/evt/*event_id*/fmt/*format_string*

若要將現有資料從裝置傳送至 {{site.data.keyword.iot_short_notm}}，您可以建立應用程式來處理資料，並將它發佈至 {{site.data.keyword.iot_short_notm}}。

**重要事項：**訊息有效負載上限為 131072 個位元組。超出此限制的訊息會被拒絕。

### 保留的訊息
{{site.data.keyword.iot_short_notm}} 組織未獲授權，無法發佈保留的 MQTT 訊息。如果應用程式、閘道或裝置傳送保留的訊息，則 {{site.data.keyword.iot_short_notm}} 服務會置換設為 true 的保留的訊息旗標，而且處理訊息的方式就像旗標設為 false 一樣。

## 發佈裝置指令
{: #publishing_device_commands}

應用程式可以將指令發佈至任何已登錄裝置，例如：

-  發佈至主題 iot-2/type/*device_type*/id/*device_id*/cmd/*command_id*/fmt/*format_string*

## 訂閱裝置事件
{: #subscribe_device_events}

應用程式可以訂閱一個以上裝置的事件，例如：

-  訂閱主題 iot-2/type/*device_type*/id/*device_id*/evt/*event_id*/fmt/*format_string*

**附註：**若要訂閱一個以上單一裝置的多種類型事件，請針對下列任何元件使用 MQTT「任何」萬用字元 (+)：

- device_type
- device_id
- event_id
- format_string

## 訂閱裝置指令
{: #subscribe_device_commands}

應用程式可以訂閱正在傳送至一個以上裝置的指令，例如：

-  訂閱主題 iot-2/type/*device_type*/id/*device_id*/cmd/*command_id*/fmt/*format_string*

**附註：**若要訂閱多個裝置的多種類型事件，請針對下列任何元件使用 MQTT「任何」萬用字元 (+)：

-  device_type
-  device_id
-  cmd_id
-  format_string

## 訂閱裝置狀態訊息
{: #subscribe_device_status}

應用程式可以訂閱來監視一個以上裝置的狀態，例如：

-  訂閱主題 iot-2/type/*device_type*/id/*device_id*/mon

**附註：**若要訂閱多個裝置的更新，請針對下列任何元件使用 MQTT「任何」萬用字元 (+)：

- device_type
- device_id

## 訂閱應用程式狀態訊息
{: #subscribe_app_status}

應用程式可以訂閱來監視一個以上應用程式的狀態，例如：

- 訂閱主題 iot-2/app/*appId*/mon

**附註：**若要訂閱所有應用程式的更新，請針對 *appId* 元件使用 MQTT「任何」萬用字元 (+)。


## Quickstart 限制
{: #quickstart_restrictions}
如果您計劃建立應用程式碼以與 Quickstart 服務搭配使用，Quickstart 中不支援下列特性：

- 發佈指令
- 訂閱指令
- 在 **deviceType** 或 **appId** 元件中使用 MQTT「任何」萬用字元 (+)
- 透過「傳輸層安全 (TLS)」的 MQTT 連線
- 可擴充應用程式

## 可擴充應用程式
{: #scalable_apps}

透過調整應用程式的連接方式，即可平衡多個應用程式實例的事件訊息負載處理來擴充 {{site.data.keyword.iot_short_notm}} 應用程式。

最佳負載平衡及可擴充性所需的用戶端數目會根據部署而不同。若要識別最佳用戶端數目，您需要對系統進行壓力測試。

可擴充應用程式定義為不可延續訂閱或混合延續性共用訂閱（測試版）。

### 不可延續訂閱
{: #shared_sub_non_durable}

若要啟用負載平衡，請確定應用程式訂閱是不可延續的，而且訂閱中的用戶端 ID 符合下列格式：

<pre class="pre">A:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
{: codeblock}

其中：
-  字元 **A** 指出用戶端是可擴充應用程式。
-  *orgId* 是在登錄服務時，所產生的唯一 6 個字元組織 ID。
-  *appId* 是用戶端的使用者定義唯一字串 ID。此字串只能包含英數字元（a-z、A-Z、0-9）以及橫線 (-)、底線 (_) 和點 (.) 特殊字元。


**重要事項：**
- 用戶端 ID 的開頭必須是 {{site.data.keyword.iot_short_notm}} 正確地指定為可擴充應用程式的大寫 **A** 字元。
- 為可擴充應用程式一部分的其他用戶端必須使用相同的用戶端 ID。
- 清除階段作業值必須設為 false (0) 以表示不可延續訂閱。

### 混合延續性共用訂閱（測試版）
{: #shared_sub_mixed}

{{site.data.keyword.iot_short_notm}} 服務會延伸 MQTT 3.1.1 版傳訊通訊協定規格來支援混合延續性共用訂閱的測試版試用。共用訂閱提供應用程式的負載平衡功能。如果後端企業應用程式無法處理發佈至特定主題空間的訊息數量，則可能需要共用訂閱。例如，多個裝置發佈單一應用程式所處理的訊息時，可能需要使用共用訂閱的負載平衡功能。

針對混合延續性共用訂閱，請確定訂閱中的用戶端 ID 符合下列格式：

<pre class="pre">A:<var class="keyword varname">org</var>:<var class="keyword varname">appId</var>:<var class="keyword varname">instanceId</var></pre>
{: codeblock}

其中：
- 用戶端 ID 中字元 **A**、*orgId* 及 *appId* 的定義方式與[不可延續訂閱](#shared_sub_non_durable)相同。
- *instanceID* 是字串，不得超過 36 個字元，而且只能包含下列字元：
   - 英數字元（a-z 、A-Z、0-9）
   - 橫線 ( - )
   - 底線 ( _ )
   - 句點 ( . )

**重要事項：**
- 混合延續性共用訂閱的支援只是測試版特性。請不要在正式作業應用程式中實作測試版特性。
- 在混合延續性共用訂閱中，清除階段作業值可以設為 true (1) 或 false (0)。
- 使用 instanceId 進行連線的用戶端所使用的訂閱，與不使用 instanceId 進行連線的用戶端所使用的訂閱不同。因此，如果您要在混合延續性共用訂閱上連接多個用戶端，則需要在所有訂閱中指定 instanceID。

**範例情境**

下列情境是 {{site.data.keyword.iot_short_notm}} 中不可延續可擴充應用程式運作方式的一個範例：

- 用戶端 1 連接為 **A:abc123:myApplication** 並訂閱所有裝置事件，這表示用戶端 1 會收到 100% 的已發佈裝置事件。
- 用戶端 2 連接為 **A:abc123:myApplication** 並訂閱所有裝置事件，這表示用戶端 1 及用戶端 2 兩者會共用所有已發佈事件。用戶端 1 與用戶端 2 共用處理負載。
- 用戶端 3 連接為 **A:abc123:myApplication** 並訂閱所有裝置事件，這表示用戶端 1、用戶端 2 及用戶端 3 都會共用事件的處理負載。
- 用戶端 2 及用戶端 3 接著取消訂閱所有裝置事件，這表示只有用戶端 1 才會收到所有已發佈裝置事件。雖然用戶端 2 及用戶端 3 仍然連接至服務，但是用戶端 1 會收到 100% 的已發佈裝置事件。
- 兩個以上的應用程式共用訂閱時，訊息可能不會依傳送的順序送達。例如，訊息 B 可能會先到達用戶端 1，訊息 A 才到達用戶端 2，即使是先傳送訊息 A 也一樣。
