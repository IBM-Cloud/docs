---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 開始使用 {{site.data.keyword.iot_short_notm}}
{: #gettingstartedtemplate}

{{site.data.keyword.iot_full}} for {{site.data.keyword.Bluemix_notm}} 提供一個多用途的工具箱，其包含閘道裝置、裝置管理，以及功能強大的應用程式存取權。您可以使用 {{site.data.keyword.iot_short_notm}}，收集連接裝置的資料以及分析組織產生的即時資料。
{:shortdesc}

## 開始之前
{: #byb}

在連接裝置及使用資料之前，請登錄 {{site.data.keyword.Bluemix_notm}} 帳戶，並在 {{site.data.keyword.Bluemix_notm}} 組織中建立 {{site.data.keyword.iot_short_notm}} 服務實例。您可以直接從 [Bluemix 服務型錄中的 {{site.data.keyword.iot_short_notm}} 頁面 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.{DomainName}/catalog/services/internet-of-things-platform/){:new_window} 建立 {{site.data.keyword.iot_short_notm}} 實例。  

如需如何在 {{site.data.keyword.Bluemix_notm}} 上註冊帳戶、配置地區以及其他帳戶管理設定的詳細資訊，請參閱[管理 Bluemix 帳戶](https://console.ng.bluemix.net/docs/admin/account.html#signup)。

您可以從儀表板設定及配置 {{site.data.keyword.iot_short_notm}} 實例。若要開啟儀表板，請移至 {{site.data.keyword.Bluemix_notm}} 中的 {{site.data.keyword.iot_short_notm}} 服務實例，然後按一下**啟動儀表板**。

## 步驟 1：連接您的裝置
{: #up_and_running}

若要使用服務開始進行，請根據您的狀況來探索下列選項：

   |   已部署的服務 | 未部署的服務
  ------------- | -------------
  **我有要連接的裝置** | [將您的裝置連接至 {{site.data.keyword.iot_short_notm}}](iotplatform_task.html#iotplatform_task)。| 在[播放組織示範 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://discover-iot.eu-gb.mybluemix.net/?cm_mc_uid=44491599487314618721024&cm_mc_sid_50200000=1462798151#/play){:new_window} 中探索裝置連線。
  **我沒有要連接的裝置** | [建立並連接 Node-RED 裝置模擬器](nodereddevice_sample.html){:new_window}。 | 開始使用 [Watson IoT Platform 入門範本](https://console.ng.bluemix.net/docs/starters/IoT/iot500.html)。
如需如何將特定裝置類型連接至 {{site.data.keyword.iot_short_notm}} 的相關資訊，請參閱 [developerWorks 秘訣 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){:new_window}。  

如需裝置連線開發人員文件，請參閱：
- [裝置的 MQTT 連線功能](devices/mqtt.html)。
- [閘道的 MQTT 連線功能](gateways/mqtt.html)。

## 步驟 2：分析您的裝置資料
{: #analyzing_data}

開始探索裝置傳送至 {{site.data.keyword.iot_short_notm}} 的即時資料。

{{site.data.keyword.iot_short_notm}} 包含下列分析工具：  
- [板和卡片](data_visualization.html)可將即時裝置資料視覺化。
- 即時裝置資料觸發的[規則及動作](analytics.html)。

如需快速開始使用的範例，請參閱[使用 IBM Watson IoT Platform 雲端分析來使用規則及動作 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){:new_window} developerWorks 秘訣。

## 步驟 3：建立應用程式來使用您的裝置資料
{: #develop_applications}

建立並連接您自己的應用程式來使用即時和歷程裝置資料，以延伸 {{site.data.keyword.iot_short_notm}} 的資料分析特性。

如需相關資訊，請參閱下列主題：   
- 探索[應用程式開發人員文件](applications/api.html)和 [{{site.data.keyword.iot_short_notm}} API 文件](reference/api.html)。
- 探索 [{{site.data.keyword.iot_short_notm}} 用戶端程式庫](iot_platform_client_lib.html)，其提供建置及開發程式碼的工具和檔案，可用來整合及連接裝置與應用程式。
- [將 {{site.data.keyword.cloudantfull}} 服務](cloudant_connector.html)連接至 {{site.data.keyword.iot_short_notm}}，以儲存歷程裝置資料。




# 相關鏈結
{: #rellinks}
* [IBM Watson IoT 服務性能儀表板](https://status.internetofthings.ibmcloud.com){:new_window}

## 指導教學及範例
{: #samples}
* [連接裝置的秘訣 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){:new_window}
* [{{site.data.keyword.iot_short_notm}} 播放組織 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://play.internetofthings.ibmcloud.com/){:new_window}
* [將 Intel Galileo 連接至 {{site.data.keyword.iot_short_notm}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/connect-an-intel-galileo-to-the-internet-of-things-foundation-connect/){:new_window}
* [連接 ARM® mbed™ IoT 入門範本套件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/arm-mbed-iot-starter-kit-part-1/){:new_window}
* [將 Raspberry Pi 連接至 {{site.data.keyword.iot_short_notm}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/raspberry-pi-4/){:new_window}

## API 參考資料
{: #api}
* [{{site.data.keyword.iot_short_notm}} API 文件](../reference/api.html)
* [開發人員文件](developer_doc_overview.html)
