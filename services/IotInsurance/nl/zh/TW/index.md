---

copyright:
  years: 2016
lastupdated: "2016-10-26"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# 開始使用 {{site.data.keyword.iotinsurance_short}}

{{site.data.keyword.iotinsurance_full}} 是一個 {{site.data.keyword.Bluemix_notm}} 服務，可用來收集、管理及分析來自所連接投保人的資料。{{site.data.keyword.iotinsurance_short}} 可讓您提供個人化風險評量、即時保護及保單成本降低。
{:shortdesc}

若要啟動並執行此服務，您必須部署必要服務及應用程式，然後配置服務。尋找服務及應用程式的概觀，以及[關於 {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html) 中的架構圖

**必要條件：**開始之前，請確定已具有下列必要條件：
- [{{site.data.keyword.iotinsurance_short}} 服務](https://console.ng.bluemix.net/catalog/services/iot-for-insurance/)實例必須存在於 {{site.data.keyword.Bluemix_notm}} 空間中。
- 您的 {{site.data.keyword.Bluemix_notm}} 組織必須有至少 2 GB 的可用記憶體，才能啟用「部署」功能。

## 部署必要服務及應用程式
{: #deploying_services}

1. 若要部署所有必要服務及應用程式，請在 [{{site.data.keyword.Bluemix_notm}} 主控台](https://console.ng.bluemix.net/#all-items)上按一下 {{site.data.keyword.iotinsurance_short}} 服務，然後按一下**部署**。

  {{site.data.keyword.iotinsurance_short}} 部署它所需的所有服務及 Node.js 應用程式。它會將應用程式自動連結至服務。

  每一個服務實例都會使用預設服務方案。您稍後可以移至服務主控台，以升級任何服務方案。您也可以刪除新實例，並將現有實例手動連結至 {{site.data.keyword.iotinsurance_short}} 服務，以使用現有服務實例。如需應用程式的相關資訊，請參閱[關於 {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html)。

2. 驗證 {{site.data.keyword.iotinsurance_short}} 儀表板運作中，並且您可以存取 API。
  1. 按一下**開啟**，以開啟 {{site.data.keyword.iotinsurance_short}} 儀表板。按一下**登入**，以接受預先填入的認證。
  2. 回到 {{site.data.keyword.iotinsurance_short}} 服務主控台，然後按一下 **API** 來檢視 API。

  **附註：**部署之後，即可在瀏覽器中輸入個別 URL 以直接存取儀表板或 API。當您使用此方法時，必須輸入 {{site.data.keyword.iotinsurance_short}} 服務認證。若要找到您的認證，請回到 {{site.data.keyword.iotinsurance_short}} 服務主控台。按一下**服務認證**標籤，然後按一下**檢視認證**。記下「使用者 ID」及「密碼」。

## 配置服務
{: #iot4i_configservices}
請執行下列作業來配置服務：

### 配置 {{site.data.keyword.amashort}}
{: #config_ama}
1. 回到 Bluemix 主控台。即會顯示 {{site.data.keyword.iotinsurance_short}} 已部署的所有應用程式及服務。

1. 複製 {{site.data.keyword.iotinsurance_short}} API 應用程式的 URL。在 API 應用程式上按一下滑鼠右鍵，然後選取**複製鏈結位置**。

2. 開啟 {{site.data.keyword.amashort}} 服務。服務提供於 {{site.data.keyword.Bluemix_notm}} 主控台的「服務」區段。

3. 按一下**開啟**，以啟用鑑別。

4. 在**自訂**區段中，按一下**配置**，然後輸入下列鑑別認證：

  - **網域名稱**：`IoT4I`

  - **自訂身分提供者 URL**：貼入您在第一個步驟中複製的 API 應用程式 URL。

  - **您的 Web 應用程式重新導向 URI**：將此欄位空白。

5. 儲存設定。您現在可以回到 {{site.data.keyword.iotinsurance_short}} 服務主控台或 {{site.data.keyword.Bluemix_notm}} 主控台。

### 配置 {{site.data.keyword.mobilepushshort}}
{: #config_push}
若要啟用現有行動應用程式的推送通知，您必須配置 {{site.data.keyword.mobilepushshort}} 服務，以及新增「公開金鑰密碼化標準 (PKCS) 12」檔案。如需行動應用程式的相關資訊，請參閱[安裝及連接範例行動應用程式](iotinsurance_mobile_app.html)。如需 {{site.data.keyword.mobilepushshort}} 的相關資訊，請參閱[開始使用推送通知](https://console.stage1.ng.bluemix.net/docs/services/mobilepush/index.html)。

  1. 開啟 {{site.data.keyword.mobilepushshort}} 服務。
  2. 按一下**配置**。
  3. 在「Apple Push Notifications 憑證」區段中，上傳行動應用程式的 PKCS 12 檔案，然後輸入密碼。


下一步
{: #whats_next}
瞭解您可以使用 {{site.data.keyword.iotinsurance_short}} 執行的作業。

- 使用「防護工具箱」中的指示及 API 來建立[使用者及防護關聯](iotinsurance_shield_toolkit.html)。
- 安裝及連接[範例行動應用程式](iotinsurance_mobile_app.html)。
- 下載或檢視 [GitHub 網站上的所有 API](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples)。

# 相關鏈結
{: #rellinks}

## 指導教學及範例
{: #samples}
* [GitHub 上的範例行動應用程式碼](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## API 參考資料
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [{{site.data.keyword.iotinsurance_short}} API 範例](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}


## 相關鏈結
{: #general}
* [{{site.data.keyword.iot_full}} 文件](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [開發人員支援討論區](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack Overflow 支援討論區](http://stackoverflow.com/questions/tagged/ibm-bluemix)
