---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Note to writers - index.md and iot4egettingstarted.md are (almost) duplicates and a change to one should be made to both. index.md appears within the product app as the getting started page. iot4egettingstarted.md appears as the top level topic in the docs toc. -->

# 使用 {{site.data.keyword.iotelectronics}} Starter 建立應用程式

{{site.data.keyword.iotelectronics_full}} 是整合式的完整解決方案，可讓您的應用程式與已連接的應用裝置通訊，以及控制、分析及更新已連接的應用裝置。入門範本包括一個可用來建立模擬應用裝置的入門範本應用程式，也包括一個可用來從行動裝置控制那些應用裝置的範例行動應用程式。
{:shortdesc}

## 開始之前

開始之前，您必須在 {{site.data.keyword.Bluemix_notm}} 組織中部署 {{site.data.keyword.iotelectronics}} 實例。部署實例，會自動部署入門範本的元件應用程式及服務。

 您可以在 {{site.data.keyword.Bluemix_notm}} 型錄的「樣板」區段中[尋找 {{site.data.keyword.iotelectronics}} 入門範本](https://console.{DomainName}/catalog/starters/iot-for-electronics-starter/)。

## 開始使用 {{site.data.keyword.iotelectronics}}
若要開始使用，請完成下列作業：

1. 使用 {{site.data.keyword.iotelectronics}} 入門範本 Web 應用程式，以[建立模擬應用裝置](iot4ecreatingappliances.html)。會使用洗衣機作為 {{site.data.keyword.iotelectronics}} 入門範本內的模擬應用裝置，來進行示範。您選擇連接的應用裝置可以是任何類型的智慧型電子裝置。
2. （選用性）[使用 {{site.data.keyword.appid_full}} 配置行動登入選項](https://console.ng.bluemix.net/docs/services/appid/index.html)。您可以自訂行動應用程式中呈現的登入畫面外觀。您也可以選擇性地啟用或停用社交登入認證的使用。根據預設值，{{site.data.keyword.appid_short_notm}} 會啟用 Facebook 和 Google+ 授權，行動應用程式使用者可以使用自己的社交認證，或者他們可以跳過登入處理程序，試用應用程式而不登入。
3. [下載及連接](iotelectronics_config_mobile.html)範例行動應用程式。


## 下一步為何？
看看您能用 {{site.data.keyword.iotelectronics}} 做什麼。

- [探索入門範本應用程式](iot4ecreatingappliances.html)，體驗企業製造商如何監視連接至 {{site.data.keyword.iot_short_notm}} 的應用裝置。
- [探索範例行動應用程式](iotelectronics_config_mobile.html)，體驗應用裝置擁有者如何登錄其應用裝置，以及與應用裝置進行互動。
- 在 {{site.data.keyword.iot_short_notm}} 中[探索及管理](iotelectronics_dashboard.html)已登錄應用裝置的資料。
- [探索 API ![外部鏈結圖示](../../icons/launch-glyph.svg)](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html){:new_window}，以查看如何自訂及展開您自己的 {{site.data.keyword.iotelectronics}} 應用程式。
