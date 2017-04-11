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

#服务需求
{: #requirements}


##MQTT 设备消息需求

* MQTT 消息代理必须以 JSON 格式在一个或多个 MQTT 主题上提供设备消息。
* 设备消息可以包含任意数量的属性，但是总是需要以下三个属性：
	* 唯一标识设备的属性。
	* 指定设备当前位置的维度的属性。
	* 指定设备当前位置的经度的属性。
* 支持以下两个消息方式：
	* MQTT 消息可以包含具有单个设备的相关信息的 JSON 对象。
	* MQTT 消息可以包含具有一组设备的信息的 JSON 数组对象。

##MQTT 事件和配置服务

您的应用程序预订 MQTT 消息并通过其 [REST API](https://console.ng.bluemix.net/apidocs/246) 控制 {{site.data.keyword.geospatialshort_Geospatial}}。可以通过 REST API 调用执行以下操作：

* 配置和启动服务。
* 添加和除去要监视的地理区域。
* 检索有关服务状态以及当前定义的区域集的信息。
* 停止服务。
* 重新启动已配置的服务。

