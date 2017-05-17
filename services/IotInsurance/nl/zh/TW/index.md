---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-02"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# 開始使用 {{site.data.keyword.iotinsurance_short}}
{: #gettingstarted}

{{site.data.keyword.iotinsurance_full}} 是一個 {{site.data.keyword.Bluemix_notm}} 服務，可用來收集、管理及分析來自所連接投保人的資料。{{site.data.keyword.iotinsurance_short}} 可讓您提供個人化風險評量、即時保護及保單成本降低。
{:shortdesc}

若要啟動並執行此服務，您必須部署必要服務及應用程式，然後配置服務。尋找服務及應用程式的概觀，以及[關於 {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html) 中的架構圖

**必要條件：**開始之前，請確定已具有下列必要條件：
- [{{site.data.keyword.iotinsurance_short}} 服務](https://console.ng.bluemix.net/catalog/services/iot-for-insurance/)實例必須存在於 {{site.data.keyword.Bluemix_notm}} 空間中。
- 您的 {{site.data.keyword.Bluemix_notm}} 組織必須有至少 2 GB 的可用記憶體，才能啟用「部署」功能。如果您是升級自舊版本，則應該有至少 2.5 GB。

## 部署必要服務及應用程式
{: #deploying_services}

1. 若要部署所有必要服務及應用程式，請在 [{{site.data.keyword.Bluemix_notm}} 主控台](https://console.ng.bluemix.net/#all-items)上按一下 {{site.data.keyword.iotinsurance_short}} 服務，然後按一下**部署**。

  {{site.data.keyword.iotinsurance_short}} 部署它所需的所有服務及 Node.js 應用程式。它會將應用程式自動連結至服務。

  每一個服務實例都會使用預設服務方案。您稍後可以移至服務主控台，以升級任何服務方案。您也可以刪除新實例，並將現有實例手動連結至 {{site.data.keyword.iotinsurance_short}} 服務，以使用現有服務實例。如需應用程式的相關資訊，請參閱[關於 {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html)。

  **重要事項：**當您部署 {{site.data.keyword.iotinsurance_short}} 試用版時，請注意同時部署之其他服務及應用程式的免費版本，其功能有所限制。{{site.data.keyword.iot_short_notm}} 最多只能有 500 個裝置，而 {{site.data.keyword.cloudant_short_notm}} 只能有 1 GB 的資料，並且具有有限的讀寫執行緒作業功能。

  **附註**：{{site.data.keyword.iotinsurance_short}} 不再部署 {{site.data.keyword.amafull}} 或 {{site.data.keyword.mobilepushfull}}。較舊版的 {{site.data.keyword.iotinsurance_short}} 使用 {{site.data.keyword.amashort}} 服務來處理來自行動應用程式的回應。這個處理程序仍然適用於所有現有的 {{site.data.keyword.iotinsurance_short}} 實例。不過，您必須建立自訂鑑別處理程序，才能使用行動應用程式搭配新的
{{site.data.keyword.iotinsurance_short}} 實例。您也可以選擇性地[建立 {{site.data.keyword.mobilepushshort}} 實例](https://console.ng.bluemix.net/docs/services/mobilepush/index.html)、配置它，然後將它連結至 {{site.data.keyword.iotinsurance_short}} API。

2. 驗證 {{site.data.keyword.iotinsurance_short}} 儀表板運作中，並且您可以存取 API。
  1. 按一下**開啟**，以開啟 {{site.data.keyword.iotinsurance_short}} 儀表板。按一下**登入**，以接受預先填入的認證。
  2. 回到 {{site.data.keyword.iotinsurance_short}} 服務主控台，然後按一下 **API** 來檢視 API。

  **附註：**部署之後，即可在瀏覽器中輸入個別 URL 以直接存取儀表板或 API。當您使用此方法時，必須輸入 {{site.data.keyword.iotinsurance_short}} 服務認證。若要找到您的認證，請回到 {{site.data.keyword.iotinsurance_short}} 服務主控台。按一下**服務認證**標籤，然後按一下**檢視認證**。記下「使用者 ID」及「密碼」。


<!--
## Configuring
{: #iot4i_configservices}



### Configuring {{site.data.keyword.amashort}}
{: #config_ama}
1. Return to your Bluemix console. All apps and services that were deployed by {{site.data.keyword.iotinsurance_short}} are displayed.

2. Copy the URL of the {{site.data.keyword.iotinsurance_short}} API application. Right-click the API application and select **Copy Link Location**.

3. Open the {{site.data.keyword.amashort}} service. The service is available in the Services section of your {{site.data.keyword.Bluemix_notm}} console.

4. Enable authentication by clicking **On**.

5. In the **Custom** section, enter the following authentication credentials:

  - **Realm name**: `IoT4I`

  - **Custom Identity Provider Url**: Paste the URL of the API application that you copied in a previous step.

  - **Your Web Application Redirect URIs**: Leave this field blank.

6. Save your settings. You can now return to the {{site.data.keyword.iotinsurance_short}} service console or your {{site.data.keyword.Bluemix_notm}} console.
-->


## 建立及配置 {{site.data.keyword.mobilepushshort}}
{: #config_push}

（選用）若要啟用現有行動應用程式的推送通知，您可以選擇性地建立 {{site.data.keyword.mobilepushshort}} 服務的實例、將它連結至 {{site.data.keyword.iotinsurance_short}} API，並新增「公開金鑰密碼化標準 (PKCS) 12」檔案。如需行動應用程式的相關資訊，請參閱[安裝及連接範例行動應用程式](iotinsurance_mobile_app.html)。如需 {{site.data.keyword.mobilepushshort}} 的相關資訊，請參閱[開始使用推送通知](https://console.ng.bluemix.net/docs/services/mobilepush/index.html)。

若要在建立之後配置服務，請執行下列步驟：

  1. 開啟 {{site.data.keyword.mobilepushshort}} 服務。
  2. 按一下**配置**。
  3. 在「Apple Push Notifications 憑證」區段中，上傳行動應用程式的 PKCS 12 檔案，然後輸入密碼。

## 使用 Weather Company data
{: #weather_company}

（選用）{{site.data.keyword.iotinsurance_short}} 提供來自 Weather Company 的一組靜態資料，而您可以基於示範用途進行檢視。您也可以選擇性地存取來自 Weather Company 的現用資料，方法是建立 [{{site.data.keyword.weatherfull}} 服務](../Weather/index.html)的實例，並將它連結至 {{site.data.keyword.iotinsurance_short}} 天氣應用程式。

**重要事項：**{{site.data.keyword.weather_short}} 服務的免費版本只能有 10,000 個要求。如果您需要更多要求，則可以升級至付費版本。

下一步
{: #whats_next}
瞭解您可以使用 {{site.data.keyword.iotinsurance_short}} 執行的作業。

- 使用「防護工具箱」中的指示及 API 來建立[使用者及防護關聯](iotinsurance_shield_toolkit.html)。
<!-- - Install and connect the [sample mobile app](iotinsurance_mobile_app.html). -->
- 下載或檢視 [GitHub 網站上的所有 API 範例 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}。
