---

copyright:
  years: 2016

---

{:new_window: target="_blank"}

{:shortdesc: .shortdesc}


# 使用 {{site.data.keyword.iotelectronics}} Starter 建立應用程式
*前次更新：2016 年 6 月 14 日*

{{site.data.keyword.iotelectronics_full}} 是整合式的端對端解決方案，可讓您的應用程式與已連接的應用裝置通訊，以及控制、分析及更新已連接的應用裝置。入門範本包含入門範本應用程式，可讓您建立及控制模擬應用裝置，也包含一個範例行動應用程式，可讓您從行動裝置控制那些應用裝置。
{:shortdesc}

**必要條件**：  
請確定您已從 Bluemix 型錄的「樣板」區段部署 {{site.data.keyword.iotelectronics}} Starter。這樣做會自動部署入門範本的元件應用程式和服務，包括 {{site.data.keyword.amafull}}。

若要開始使用 {{site.data.keyword.iotelectronics}}，請完成下列作業，如在後續小節中所述：

1. 配置 {{site.data.keyword.amashort}}，以便啟用與範例行動應用程式的通訊。
2. 使用 {{site.data.keyword.iotelectronics}} Starter Web 應用程式建立模擬應用裝置。
3. 安裝及連接範例行動應用程式。

## 配置 {{site.data.keyword.amashort}}
{: #configureMCA}
若要使用行動應用程式，您必須配置 {{site.data.keyword.amashort}}，如下所示：
1. 在 {{site.data.keyword.Bluemix_notm}} 儀表板中，開啟 [{{site.data.keyword.amashort}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)。
2. 在**自訂**區段中，選取**配置**。
3. 輸入下列鑑別認證：
  - **領域名稱**：myRealm
  - **URL**：https://<*myIoT4eStarterApp*>.mybluemix.net  

    **提示：**請務必在 URL 中使用安全的 `https://` 字首。您可以按一下**行動選項**，找到入門範本應用程式的 URL。
4. 儲存。

  如需詳細指示，請參閱[配置 {{site.data.keyword.amashort}}](iotelectronics_config_mobile.html#iot4e_configureMCA)。

##建立模擬應用裝置
若要建立模擬應用裝置，請執行下列步驟：
1. 在 {{site.data.keyword.Bluemix_notm}} 儀表板中，啟動 {{site.data.keyword.iotelectronics}} 應用程式。
2. 等待`您的應用程式正在執行中`狀態訊息，然後按一下**檢視應用程式**以顯示入門範本應用程式。  
3. 選取**遠端控制您的已連接應用裝置**。
4. 捲動至標示為**接下來，選擇或新增模擬洗衣機**，然後按一下新增 (+) 按鈕。即會建立新的洗衣機。

## 安裝並連接範例行動應用程式
若要安裝並連接範例行動應用程式，請執行下列步驟：

*附註*：您必須具有 iOS 裝置才能使用範例行動應用程式。

1. 在您的手機上，開啟 App Store 並搜尋 `ibm iot`。選擇 **IBM IoT for Electronics** 然後安裝。
2. 藉由掃描入門範本應用程式中找到的連線 QR 碼，將您的手機連接到組織。
3. 藉由掃描入門範本應用程式中找到的應用裝置 QR 碼，連接您的模擬應用裝置。

  如需詳細指示，請參閱[將行動應用程式連接至您的 {{site.data.keyword.iotelectronics}} 環境](iotelectronics_config_mobile.html#iot4e_connecting_mobile)。

##下一步為何？
看看您能用 {{site.data.keyword.iotelectronics}} 做什麼。

- 探索入門範本應用程式，體驗企業製造商如何監視連接 {{site.data.keyword.iot_short_notm}} 的應用裝置。
- 探索範例行動應用程式，體驗應用裝置擁有者如何登錄其應用裝置，以及與應用裝置進行互動。
- 手動讓設備故障觸發警示、通知和動作，同時傳送給製造商和應用裝置擁有者。
- 將作業資料與使用者資料相關聯，以瞭解您的產品和裝置的操作情形，還有誰正在操作它們。


# 相關鏈結
{: #rellinks}
## API 文件
{: #api}
* [{{site.data.keyword.iotelectronics}}](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)
* [{{site.data.keyword.iotrtinsights_short}}](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)  
* [{{site.data.keyword.iot_short}}](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)


## 元件
{: #general}

* [{{site.data.keyword.iotelectronics_full}} 文件](iotelectronics_overview.html)
* [{{site.data.keyword.iot_full}}](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
* [{{site.data.keyword.iotrtinsights_full}}](https://new-console.ng.bluemix.net/docs/services/iotrtinsights/iotrtinsights_overview.html)
* [{{site.data.keyword.amafull}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)
* [{{site.data.keyword.sdk4nodefull}}](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)

## 範例
{: #samples}
* [範例行動應用程式](https://new-console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html)
