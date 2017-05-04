---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 啟用 Chrome Apps and Extensions 來接收推送通知
{: #web_notifications}
前次更新：2017 年 4 月 12 日
{: .last-updated}

您可以啟用 Chrome Apps and Extensions 來接收 {{site.data.keyword.mobilepushshort}}。請確定您已通過[配置通知提供者的認證](t__main_push_config_provider.html)，再繼續進行下列步驟。

## 安裝適用於 Push Notifications 的用戶端 SDK
{: #web_install}

本主題說明如何安裝及使用用戶端 JavaScript Push SDK 來進一步開發 Chrome Apps and Extensions。

### 在 Google Chrome Apps and Extensions 中起始設定
{: #initialize_google_extn_app}

若要在 Chrome Apps and Extensions 中安裝 Javascript SDK，請完成下列步驟：

請從 [Bluemix Web Push SDK ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master){: new_window}，下載 `BMSPushSDK.js` 及 `manifest_Chrome_Ext.json`（適用於 Chrome Extensions）或 `manifest_Chrome_App.json`（適用於 Chrome Apps）。



- 若為 Chrome Apps，請配置資訊清單檔：
 1. 在 `manifest_Chrome_App.json` 檔案中，提供名稱、說明及圖示。
 2. 在 `app.background.scripts` 中，新增 `BMSPushSDK.js`。
 3. 將 `manifest_Chrome_App.json` 變更為 `manifest.json`。

- 若為 Chrome Extensions，請配置資訊清單檔：
 1. 在 `manifest_Chrome_Ext.json` 檔案中，提供名稱、說明及圖示。
 2. 在 `background.scripts` 中，新增 `BMSPushSDK.js`。
 3. 將 `manifest_Chrome_Ext.json` 變更為 `manifest.json`。

在 `background.js` 檔案中，新增下列這幾行，以接收推送通知： 
```
chrome.gcm.onMessage.addListener(BMSPushBackground.onMessageReceived)
chrome.notifications.onClicked.addListener(BMSPushBackground.notification_onClicked);
chrome.notifications.onButtonClicked.addListener(BMSPushBackground.notifiation_buttonClicked); 
```
	{: codeblock}



### 起始設定 Push SDK 
{: #web_initialize}

使用 Bluemix {{site.data.keyword.mobilepushshort}} Service `app GUID` 及 `app Region` 來起始設定 Push SDK。  

若要取得應用程式 GUID，請在導覽窗格中選取已起始設定之 Push 服務的**配置**選項，然後按一下**行動選項**。修改程式碼 Snippet，以使用 Bluemix Push Notifications Service appGUID 參數。

`App Region` 指定管理 {{site.data.keyword.mobilepushshort}} Service 的位置。您可以使用下列三個值的其中一個：

 - 美國達拉斯：`.ng.bluemix.net`
 - 英國：`.eu-gb.bluemix.net`
 - 雪梨：`.au-syd.bluemix.net`

```
    var bmsPush = new BMSPush();
    function callback(response) {
        alert(response.response)
    }
    var initParams = {
      "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
   "clientSecret":"clientSecret of your push service"
    }
  bmsPush.initialize(params, callback)
```
	{: codeblock}

### 登錄 Chrome Apps and Extensions
{: #web_register}

使用 `register()` API，以向 {{site.data.keyword.mobilepushshort}} Service 登錄裝置。若要從 Google Chrome 登錄，請在 Bluemix {{site.data.keyword.mobilepushshort}} Service Web 配置儀表板中新增 Firebase Cloud Messaging (FCM) API 金鑰及網站 URL。如需相關資訊，請參閱[配置通知提供者的認證](t__main_push_config_provider.html)。 

若要從 Mozilla Firefox 登錄，請在 Bluemix {{site.data.keyword.mobilepushshort}} Service Web 配置儀表板的 Firefox 設定下新增網站 URL。

使用下列程式碼 Snippet，在 Bluemix {{site.data.keyword.mobilepushshort}} Service 中登錄。
```
    var bmsPush = new BMSPush();
    function callback(response) {
        alert(response.response)
    }
    var initParams = {
      "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
  "clientSecret":"clientSecret of your push service"
  }
  bmsPush.initialize(params, callback)
    bmsPush.register(function(response) {
      alert(response.response)
  })
```
    {: codeblock}


## 將基本通知傳送至 Chrome Apps and Extensions 
{: #web_extensions_notifications}

開發應用程式之後，您可以傳送推送通知。 

1. 選取**傳送通知**，然後選擇 **Web 通知**作為**傳送至**選項來編寫訊息。 
2. 在**訊息**欄位中，鍵入需要遞送的訊息。
3. 您可以選擇提供選用設定：
  - **通知標題**：這是將顯示為訊息警示標題的文字。
  - **通知圖示 URL**：如果需要使用應用程式通知圖示來遞送您的訊息，請在此欄位中提供該圖示的鏈結。
  - **收合金鑰**：收合金鑰會附加至通知。如果多個具有相同收合金鑰的通知在裝置離線時循序到達，則會予以收合。當裝置上線時，會接收到來自 FCM/GCM 伺服器的通知，並且只會顯示含有相同收合金鑰的最新通知。如果未設定收合金鑰，則會儲存新舊訊息，以供未來遞送。
  - **存活時間**：此值是以秒為單位來設定。如果未指定此參數，則 FCM/GCM 伺服器會儲存訊息四週，並嘗試遞送。有效性會在四週後到期。可能值範圍是從 0 到 2,419,200 秒。
  - **閒置時延遲**：將此值設為 `true` 時，指示 FCM/GCM 伺服器不要在裝置閒置時遞送通知。將此值設為 `false`，則可確保遞送通知，即使裝置閒置也是一樣。
  - **其他有效負載**：指定通知的自訂有效負載值。

下列影像顯示儀表板中的 Chrome Apps and Extensions 通知選項。

  ![通知畫面](images/push_chrome_extns.jpg)
  
### 後續步驟
{: #next_steps_tags}

順利設定基本通知之後，即可選擇配置標籤型通知及進階選項。

將這些 {{site.data.keyword.mobilepushshort}} Service 特性新增至您的應用程式。若要使用標籤型通知，請參閱[標籤型通知](c_tag_basednotifications.html)。若要使用進階通知選項，請參閱[進階通知](t_advance_badge_sound_payload.html)。



