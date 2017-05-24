---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-05"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# 使用 API 連接應用程式、裝置及閘道
{: #connect_devices_apps_gw}

您可以透過 MQTT 通訊協定將應用程式、裝置及閘道連接至 {{site.data.keyword.iot_full}}。您也可以使用 HTTP REST API 將裝置連接至 {{site.data.keyword.iot_short_notm}}。
{: shortdesc}


## 用戶端連線 URL
{: #client_connect_url}

若要將裝置、應用程式和閘道用戶端連接至 {{site.data.keyword.iot_short_notm}} 實例，請使用下列連線 URL：

### 傳訊位址

<pre class="pre"><var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com</pre>
{: codeblock}

### HTTP REST API 連線 URL

<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.internetofthings.ibmcloud.com/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>
{: codeblock}

**附註**
- 其中 *orgId* 是在登錄服務實例時所產生的唯一組織 ID。
- 如果您要將裝置或應用程式連接至 Quickstart 服務，請指定 'quickstart' 作為 *orgId* 值。

## 埠安全
{: #client_port_security}

確定所需的埠已開啟並已啟用，可進行通訊。埠 8883 及 443 支援搭配使用傳輸層安全 (TLS) 與 MQTT 及 HTTP 通訊協定的安全連線。埠 1883 支援使用 MQTT 及 HTTP 通訊協定的不安全連線。下表彙總連線類型及關聯埠號的相關資訊：   

|連線類型 |埠號|
|:---|:---|
|非安全|1883|
|安全|8883|
|安全|443|

MQTT 是透過 TCP 及 WebSockets 所支援。MQTT 用戶端會使用適當的認證來連接，例如適用於裝置的裝置鑑別記號，以及適用於應用程式的 API 金鑰和記號。因為傳訊至非安全埠 1883 的 MQTT 會以純文字格式來傳送這些認證，所以請務必改用安全的替代埠 8883 或 443。透過安全埠傳送時，一律會加密傳輸層安全 (TLS) 認證。請注意，您必須使用 Python MQTT 程式庫中的 tls_set() 方法，在應用程式中啟用傳輸層安全 (TLS)。否則，可能會以不安全的方式傳送資料。

當您在埠 8883 或 443 上使用安全的 MQTT 傳訊時，較新的用戶端程式庫會自動信任 {{site.data.keyword.iot_short_notm}} 所提出的憑證。如果您的用戶端環境不是這種情形，您可以從 [messaging.pem](https://github.com/ibm-messaging/iot-python/blob/master/src/ibmiotf/messaging.pem) 下載並使用完整的憑證鏈。


## 傳輸層安全 (TLS) 需求
{: #tls_requirements}

部分「傳輸層安全 (TLS)」用戶端程式庫不支援包含萬用字元的網域。如果您無法順利變更程式庫，請停用憑證檢查。

傳輸層安全 (TLS) 需求取決於是使用 MQTT 還是 HTTP 通訊協定連接至 {{site.data.keyword.iot_short_notm}}。下列各節顯示使用預設伺服器憑證時所支援的密碼組合。如果您使用的是自己的用戶端憑證，則支援的密碼組合取決於所使用的憑證。

### MQTT 連線的傳輸層安全 (TLS) 需求

{{site.data.keyword.iot_short_notm}} 需要 TLS 1.2 版及下列密碼組合：


- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384

### HTTP 連線的傳輸層安全 (TLS) 需求

如果您使用的是預設伺服器憑證，則 {{site.data.keyword.iot_short_notm}} 需要 TLS 第 1 版、TLS 1.1 版或 TLS 1.2 版，以及下列密碼組合：


- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_256_GCM_SHA384


## MQTT 用戶端鑑別
{: #mqtt_authentication}

**重要事項：**每一個 MQTT 用戶端都需要唯一的用戶端 ID。如果您嘗試使用已連接的用戶端 ID 來連接組織中的用戶端，則第一個連線會中斷。

直接連接到 {{site.data.keyword.iot_short_notm}} 的裝置和閘道會在儀表板上顯示狀態圖示，指出其已連接。透過閘道間接連接的裝置會顯示為中斷連線，因為儀表板無法感知透過閘道連接的裝置。

### MQTT 用戶端 ID

為了讓裝置、應用程式和閘道順利鑑別，請使用下列用戶端 ID 和格式來定義每一個 MQTT 用戶端：

|用戶端類型 |ID|MQTT ID 格式|
|:---|:---|:---|
|應用程式|a|<pre class="pre">a:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
|可擴充應用程式|A|<pre class="pre">A:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
|裝置|d|<pre class="pre">d:<var class="keyword varname">orgId</var>:<var class="keyword varname">deviceType</var>:<var class="keyword varname">deviceId</var></pre>|
|閘道|g|<pre class="pre">g:<var class="keyword varname">orgId</var>:<var class="keyword varname">typeId</var>:<var class="keyword varname">deviceId</var></pre>|

其中
- *orgId* 是在登錄服務時，所產生的唯一 6 個字元組織 ID。
- *appId* 是用戶端的使用者定義唯一字串 ID。
- *deviceId* 在所有類型中唯一地識別裝置或閘道，類似序號。
- *device_type* 是連接且類似型號的裝置類型 ID。
- *typeId* 是連接且類似型號的閘道類型 ID。

*appId*、*type_id*、*device_type* 和 *device_id* 值不得超過 36 個字元，而且只能包含：
- 英數字元（a-z 、A-Z、0-9）
- 橫線 ( - )
- 底線 ( _ )
- 句點 ( . )

**附註：**
- 當您連接至 Quickstart 服務時，不需要鑑別。
- 在連接之前，您不需要登錄應用程式。


### 使用 MQTT 來連接應用程式

{{site.data.keyword.iot_short_notm}} 應用程式需要有 API 金鑰才能連接至組織。登錄 API 金鑰時，會產生必須與該 API 金鑰搭配使用的記號。

下列程式碼提供 API 金鑰的範例：

<pre class="pre">a-<var class="keyword varname">orgId</var>-a84ps90Ajs</pre>
{: codeblock}

下列範例顯示一般鑑別記號：

```
 MP$08VKz!8rXwnR-Q*
```

當您使用 API 金鑰建立 MQTT 連線時，請確定符合下列需求：

- MQTT 用戶端 ID 的格式為：a:*orgId*:*appId*
- MQTT 使用者名稱是 API 金鑰，例如，a-*orgId*-a84ps90Ajs
- MQTT 密碼是鑑別記號，例如，*MP$08VKz!8rXwnR-Q*

如需相關資訊，請參閱[應用程式的 MQTT 連線功能](../../applications/mqtt.html)。

### 裝置鑑別

#### 使用者名稱
{{site.data.keyword.iot_short_notm}} 服務僅支援裝置的記號型鑑別；因此每一個裝置都只有一個有效使用者名稱。
`use-token-auth` 的值向服務指出，閘道或裝置的鑑別記號會用來作為 MQTT 連線的密碼。

如需相關資訊，請參閱[裝置的 MQTT 連線功能](../../devices/mqtt.html)。

#### 密碼
如果用戶端是使用記號型鑑別，請提交裝置鑑別記號作為所有 MQTT 連線的密碼。
