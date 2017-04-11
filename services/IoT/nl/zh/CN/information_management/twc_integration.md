---

copyright:
years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 将 The Weather Company 的数据与设备一起使用
{: #weathercompany}

The Weather Company 集成可让您将天气数据与现有 {{site.data.keyword.iot_short_notm}} 设备相组合。
{:shortdesc}

如果使用 API 发起了更新位置请求，或者设备已使用设备管理消息设置其位置，那么来自 The Weather Company 的天气数据会显示在设备详细信息视图中。

**重要信息：**只有受管设备可以设置其自己的位置。所有非受管设备必须使用 API 手动设置其位置。有关设置设备位置的更多信息，请参阅[更新位置请求](../../devices/device_mgmt/index.html#update-location)。

### 用于 The Weather Company 的 REST API 
要访问用于 The Weather Company 的 REST API，请参阅
[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部链接图标](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather){: new_window} 文档中“设备位置天气”部分。

### 查看天气数据

要查看针对设备位置检索到的天气数据：
1. 单击**设备**窗格中的设备。
2. 在详细设备视图中，向下滚动到**扩展**部分。  
列出了以下天气数据：
 - 当前天气。
 - 当前温度。
 - 预测的最高和最低温度。
 - 相对湿度。
 - 气压。
 - 能见度。
 - 风速。
 - 风向。
 - 纬度。
 - 经度。

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html){: new_window}. -->
