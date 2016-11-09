---

copyright:
 years: 2015 2016

---


# 啟用 Web 應用程式來接收 {{site.data.keyword.mobilepushshort}}
{: #web_notifications}
前次更新：2016 年 10 月 17 日
{: .last-updated}

您現在可以啟用 Google Chrome 及 Mozilla Firefox Web 應用程式來接收 {{site.data.keyword.mobilepushshort}}。

## 安裝適用於 {{site.data.keyword.mobilepushshort}} 的 Web 瀏覽器用戶端 SDK
{: #web_install}

本主題說明如何安裝及使用用戶端 JavaScript Push SDK，來進一步開發 Web 應用程式。

### 在 Google Chrome Web 應用程式中起始設定

若要在 Chrome Web 應用程式中安裝 Javascript SDK，請完成下列步驟：

從 [Bluemix Web Push SDK](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master) 下載 `BMSPushSDK.js`、`BMSPushServiceWorker.js` 及 `manifest_Website.json`。

1. 編輯 `manifest_Website.json` 檔案。

若為 Google Chrome 瀏覽器，請將 `name` 變更為您網站的名稱。將 `gcm_sender_id` 變更為 Firebase Cloud Messaging (FCM) 或 Google Cloud Messaging (GCM) sender_ID。如需相關資訊，請參閱 [Google 文件](https://developers.google.com/web/fundamentals/getting-started/codelabs/push-notifications/#make_a_project_on_the_google_developer_console)。gcm_sender_id 值只包含數字。

```
 {
  "name": "YOUR_WEBSITE_NAME",
      "gcm_sender_id": "GCM_Sender_Id"
    }
```
    {: codeblock}
 
針對 Mozilla Firefox 瀏覽器，在 `manifest.json` 檔案中新增下列值。將 `name` 變更為您網站的名稱。

```
{
  "name": "YOUR_WEBSITE_NAME"
    }
```
    {: codeblock}

2. 將 `manifest_Website.json` 檔名變更為 `manifest.json`。
3. 將 `BMSPushSDK.js`、`BMSPushServiceWorker.js` 及 `manifest.json` 新增至根目錄。
3. 在 html 檔案的 `<head>` 標籤中包括 `manifest.json`。
```
 <link rel="manifest" href="manifest.json">
```
    {: codeblock}
4. 從 GitHub 中，將 Bluemix Web Push SDK 併入 Web 應用程式。
```
 <script src="BMSPushSDK.js" async></script>
```
    {: codeblock}

## 起始設定 Web Push SDK 
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

## 登錄 Web 應用程式
{: #web_register}

使用 `register()` API，以向 {{site.data.keyword.mobilepushshort}} Service 登錄裝置。若要從 Google Chrome 登錄，請在 Bluemix {{site.data.keyword.mobilepushshort}} Service Web 配置儀表板中新增 Firebase Cloud Messaging (FCM) 或 Google Cloud Messaging (GCM) API 金鑰及網站 URL。如需相關資訊，請參閱 Chrome 設定下的[配置 Google Cloud Messaging 的認證](t_push_provider_android.html)。

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

## 傳送基本 {{site.data.keyword.mobilepushshort}}
  {: #send}

開發應用程式之後，您可以傳送推送通知。 

1. 選取**傳送通知**，然後選擇 **Web 通知**作為**傳送至**選項來編寫訊息。 
2. 在**訊息**欄位中，鍵入需要遞送的訊息。
3. 您可以選擇提供選用設定：
  - **通知標題**：這是將顯示為訊息警示標題的文字。
  - **通知圖示 URL**：如果需要使用應用程式通知圖示來遞送您的訊息，請在此欄位中提供該圖示的鏈結。
  - **其他有效負載**：指定通知的自訂有效負載值。

下列影像顯示儀表板中的 Web 通知選項。

  ![通知畫面](images/DashboardWebpush.jpg)
  
## 後續步驟
  {: #next_steps_tags}

順利設定基本通知之後，您就可以配置標籤型通知及進階選項。

將這些 {{site.data.keyword.mobilepushshort}} Service 特性新增至您的應用程式。
若要使用標籤型通知，請參閱[標籤型通知](c_tag_basednotifications.html)。
若要使用進階通知選項，請參閱[進階通知](t_advance_badge_sound_payload.html)。



