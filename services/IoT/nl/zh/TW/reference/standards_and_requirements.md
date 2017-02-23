---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-28"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
# 標準和需求
{: #standards_and_requirements}

{{site.data.keyword.iot_full}} 支援用於傳訊以及一般裝置和應用程式開發的數項標準和需求。
{:shortdesc}


<!-- ## Blockchain
{: #blockchain}

{{site.data.keyword.iot_short_notm}} supports the following versions of the Hyperledger fabric:
- 0.5

## Python
{: #python}

Support for MQTT over SSL requires at least Python v2.7.9 or v3.4, and OpenSSL v1.0.1.
-->

## MQTT
{: #mqtt}

{{site.data.keyword.iot_short_notm}} 支援下列版本的 MQTT 傳訊通訊協定：

MQTT 版本 | 附註
--- | --- | ---
[3.1.1](https://www.oasis-open.org/standards#mqttv3.1.1)（建議）  | <ul><li>OASIS 標準。<li>ISO 標準 (ISO/IEC PRF 20922) <li>相較於 3.1 版，由於通訊協定的定義更加精準，因此各種用戶端與伺服器之間的交互作業能力也隨之提升。<li>MQTT 用戶端 ID (ClientId) 的長度上限，已從 3.1 版強制限制的 23 個字元，增加到 256 個字元。</br>{{site.data.keyword.iot_short_notm}} 服務通常會需要較長的用戶端 ID。</br>不論 MQTT 通訊協定版本為何，都可支援較長的用戶端 ID。不過，部分 3.1 版用戶端程式庫會檢查 ClientId 值的長度，並強制施行 23 個字元的限制。</ul>
3.1 | MQTT 3.1 版是當今使用最廣泛的通訊協定版本。{{site.data.keyword.iot_short_notm}} 支援 MQTT 標準允許的任何內容。MQTT 不限制資料內容，因此能夠傳送影像、任何編碼的文字、加密的資料，以及幾乎所有類型的二進位格式資料。如需 MQTT 標準的相關資訊，請參閱下列資源：
- [MQTT.org](http://mqtt.org/)
- [HiveMQ：MQTT 簡介](http://www.hivemq.com/blog/mqtt-essentials-part-1-introducing-mqtt)

如需訊息有效負載大小限制，以及 {{site.data.keyword.iot_short_notm}} 特定使用案例格式限制的相關資訊，請參閱 [MQTT 傳訊](mqtt/index.html)。
