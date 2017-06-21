---

copyright:
years: 2016, 2017
lastupdated: "2017-03-21"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 透過您的裝置來使用 The Weather Company 的資料
{: #weathercompany}

The Weather Company 整合可讓您將天氣資料與現有 {{site.data.keyword.iot_short_notm}} 裝置結合。
{:shortdesc}

如果已使用 API 提出更新位置要求，或裝置已使用裝置管理訊息設定其位置，則 The Weather Company 的天氣資料會出現在裝置詳細資料視圖中。

**重要事項：**只有受管理裝置才能設定自己的位置。所有未受管理裝置都必須使用 API 手動設定其位置。如需設定裝置位置的相關資訊，請參閱[更新位置要求](../../devices/device_mgmt/index.html#update-location)。

## The Weather Company 的 REST API
若要存取 The Weather Company 的 REST API，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部鏈結圖示](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather){: new_window} 文件中的「裝置位置天氣」小節。

## 檢視天氣資料

若要檢視針對裝置位置所擷取的天氣資料，請執行下列動作：
1. 在**裝置**窗格中按一下該裝置。
2. 在詳細裝置視圖中，向下捲動至**延伸規格**區段。  
即會列出下列天氣資料：
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
