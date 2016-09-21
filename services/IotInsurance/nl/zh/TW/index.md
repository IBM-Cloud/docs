---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# 開始使用 {{site.data.keyword.iotinsurance_short}}（測試版）
{: #iotins_gettingstarted}
前次更新：2016 年 9 月 12 日
{: .last-updated}

{{site.data.keyword.iotinsurance_full}} 是一個 {{site.data.keyword.Bluemix_notm}} 服務，可用來收集、管理及分析來自所連接投保人的資料。{{site.data.keyword.iotinsurance_short}} 可讓您提供個人化風險評量、即時保護及保單成本降低。
{:shortdesc}

若要啟動並執行此服務，您必須部署必要服務及應用程式，然後配置服務。

**必要條件：**開始之前，請確定已具有下列必要條件：
- [{{site.data.keyword.iotinsurance_short}} 服務](https://new-console.ng.bluemix.net/catalog/services/iot-for-insurance/) 實例必須存在於 {{site.data.keyword.Bluemix_notm}} 空間中。
- 電腦上必須要有至少 10 GB 儲存空間。

## 部署必要服務及應用程式
{: #deploying_services}

1. 若要部署所有必要服務及應用程式，請在 {{site.data.keyword.Bluemix_notm}} 儀表板上按一下 {{site.data.keyword.iotinsurance_short}} 服務磚，然後按一下**部署**。

  {{site.data.keyword.iotinsurance_short}} 部署它所需的所有服務及 Node.js 應用程式。它會將應用程式自動連結至服務。

  每一個服務實例都會使用預設服務方案。您稍後可以移至服務主控台，以升級任何服務方案。您也可以刪除新實例，並將現有實例手動連結至 {{site.data.keyword.iotinsurance_short}} 服務，以使用現有服務實例。如需應用程式的相關資訊，請參閱[關於 {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html)。

2. 驗證所有服務及應用程式已建立並正確運作。在 {{site.data.keyword.Bluemix_notm}} 儀表板中，檢查所有應用程式的狀態為`執行中`。

3. 驗證 {{site.data.keyword.iotinsurance_short}} 儀表板運作中，並且您可以存取 API。
  1. 按一下 {{site.data.keyword.iotinsurance_short}} 服務磚，然後選取**服務認證**標籤。
  2. 按一下**檢視服務認證**，並記下「使用者 ID」及「密碼」。您將透過下列步驟來使用這些認證。
  3. 選取**管理**標籤，然後按一下**開啟**，以開啟 {{site.data.keyword.iotinsurance_short}} 儀表板。
  4. 按一下 **API**，以檢視 API。

## 配置服務
{: #iot4i_configservices}
請執行下列作業來配置服務：

### 配置 {{site.data.keyword.amashort}}
{: #config_ama}
1. 識別 {{site.data.keyword.iotinsurance_short}} API 應用程式的基本 URL。此 URL 會顯示在應用程式磚上，而且格式為 *appName*-api.mybluemix.net。

2. 開啟 {{site.data.keyword.amashort}} 服務。

3. 在**自訂**區段中，按一下**配置**，然後輸入下列鑑別認證：

  - **網域名稱**：`IoT4I`

  - **自訂身分提供者 URL**：下列格式的 API 應用程式 URL：
  ```
  https://appName-api.mybluemix.net
  ```

  - **您的 Web 應用程式重新導向 URI**：將此欄位空白。

### 配置 {{site.data.keyword.mobilepushshort}}
{: #config_push}
若要啟用現有行動應用程式的推送通知，您必須配置 {{site.data.keyword.mobilepushshort}} 服務，以及新增「公開金鑰密碼化標準 (PKCS) 12」檔案。如需行動應用程式的相關資訊，請參閱[安裝及連接範例行動應用程式](iotinsurance_mobile_app.html)。如需 {{site.data.keyword.mobilepushshort}} 的相關資訊，請參閱[開始使用推送通知](https://new-console.stage1.ng.bluemix.net/docs/services/mobilepush/index.html)。

  1. 開啟 {{site.data.keyword.mobilepushshort}} 服務。
  2. 按一下**設定 Push**。
  3. 在「Apple Push Notifications 憑證」區段中，上傳行動應用程式的 PKCS 12 檔案，然後輸入密碼。

下一步
{: #whats_next}
瞭解您可以使用 {{site.data.keyword.iotinsurance_short}} 執行的作業。

- 建立[使用者及防護裝置關聯](iotinsurance_create_users.html)。
- 安裝及連接[範例行動應用程式](iotinsurance_mobile_app.html)。
- 使用[進階服務](iotinsurance_advancedservices.html)來改善效能。
- 檢視 [API](https://iot4i-docs-api.mybluemix.net/dist/)。

# 相關鏈結
{: #rellinks}

## 指導教學及範例
{: #samples}
* [Github 上的範例行動應用程式碼](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## API 參考資料
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API 範例](https://iot4i-docs-api.mybluemix.net/dist/){:new_window}

## 相關鏈結
{: #general}
* [{{site.data.keyword.iot_full}} 文件](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
* [開發人員支援討論區](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack Overflow 支援討論區](http://stackoverflow.com/questions/tagged/ibm-bluemix)
