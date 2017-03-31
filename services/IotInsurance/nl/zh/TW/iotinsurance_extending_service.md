---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# 使用 API 擴充服務
{: #iot4i_extending_service}
{{site.data.keyword.iotinsurance_full}} 提供 API 來自訂及擴充 {{site.data.keyword.iotinsurance_short}} 解決方案。
{:shortdesc}

{{site.data.keyword.iotinsurance_short}} 隨附 Wink 漏水感應器的內建支援。使用提供的 API，即可自訂 {{site.data.keyword.iotinsurance_short}} 解決方案來支援新的裝置類型及供應商。{{site.data.keyword.iotinsurance_short}} 依賴雲端對雲端通訊，以取得裝置的感應器資料。建立新的轉換微服務，即可自訂 {{site.data.keyword.iotinsurance_short}} 來讀取新裝置的感應器資料，並透過 {{site.data.keyword.iot_short_notm}} 服務將它傳遞給系統的其餘部分，然後視情況採取動作。

如需一組完整範例程式碼，請參閱 [API 範例 GitHub 儲存庫 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){: new_window}。

如需 API 的完整資訊，請參閱 [API 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://iot4i-api-docs.mybluemix.net/){: new_window}。
