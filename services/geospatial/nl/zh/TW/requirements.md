---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#服務需求
{: #requirements}


##MQTT 裝置訊息需求

* MQTT 訊息分配管理系統必須對一個以上的 MQTT 主題提供 JSON 格式的裝置訊息。
* 裝置訊息可以包含任意數目的屬性，但是一律需要下列三個屬性：
	* 唯一識別裝置的屬性。
	* 指定裝置現行位置緯度的屬性。
	* 指定裝置現行位置經度的屬性。
* 支援兩種訊息模式：
	* MQTT 訊息可以包含具有單一裝置相關資訊的 JSON 物件。
	* MQTT 訊息可以包含具有一組裝置相關資訊的物件的 JSON 陣列。

##MQTT 事件及配置服務

您的應用程式會訂閱 MQTT
訊息並控制透過 [REST API](https://console.ng.bluemix.net/apidocs/246) 控制 {{site.data.keyword.geospatialshort_Geospatial}}。
下列動作可透過 REST API 呼叫進行：

* 配置及啟動服務。
* 新增及移除要監視的地理區域。
* 擷取服務狀態及目前定義的一組地區的相關資訊。
* 停止服務。
* 重新啟動已配置的服務。

