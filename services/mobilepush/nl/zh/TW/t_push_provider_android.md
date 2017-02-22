---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 配置 FCM 的認證
{: #create-push-enable-gcm}
前次更新：2017 年 1 月 16 日
{: .last-updated}

Firebase Cloud Messaging (FCM) 是用來將推送通知遞送至 Android 裝置及 Google Chrome 的閘道。FCM 是新版本的 Google Cloud Messaging (GCM)。若要在儀表板上設定 {{site.data.keyword.mobilepushshort}} 服務，您需要取得 FCM 認證。請確定將 FCM 配置用於新的應用程式。現有應用程式將繼續使用 GCM 配置運作。

##取得傳送端 ID 及 API 金鑰
{: #android-senderid-apikey}

API 金鑰會安全地儲存並供 {{site.data.keyword.mobilepushshort}} Service 用來連接至 FCM 伺服器，而適用於 Google Chrome 及 Mozilla Firefox 的 Android SDK 及 JS SDK 在用戶端上使用「傳送端 ID」（專案號碼）。 

若要設定 FCM 以及產生 API 金鑰和「傳送端 ID」，請完成下列步驟：

1. 造訪 [Firebase 主控台 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.firebase.google.com/?pli=1 "外部鏈結圖示"){: new_window}。
2. 選取**建立新專案**。 
3. 在「建立專案」視窗中，提供專案名稱、選擇國家/地區，然後按一下**建立專案**。
3. 在導覽窗格中，按一下「設定」圖示，然後選取**專案設定**。
4. 選擇 Cloud Messaging 標籤，以產生「伺服器 API 金鑰」及「傳送端 ID」。

##設定適用於 Android 及 Chrome Apps and Extensions 的 {{site.data.keyword.mobilepushshort}} Service
{: #setup-push-android}

**附註：**您將需要「FCM/GCM API 金鑰」及「傳送端 ID」（專案號碼）。

1. 開啟 Bluemix 儀表板，然後按一下您已建立的 {{site.data.keyword.mobilepushfull}} Service 實例來開啟儀表板。即會顯示 Push 儀表板。若要設定適用於 Android 的未連結 {{site.data.keyword.mobilepushshort}} Service，請選取「未連結 {{site.data.keyword.mobilepushshort}} Service」圖示來開啟 {{site.data.keyword.mobilepushshort}} Service 儀表板。
 

![Push 儀表板](images/push_unbound.jpg)

2. 按一下**設定 Push** 按鈕，以配置適用於 Android 應用程式及 Google Chrome Apps and Extensions 的 FCM/GCM 認證。
3. 在**配置**頁面上，對於 Android，移至 **Mobile** 標籤，然後配置「傳送端 ID」（GCM 專案號碼）及「API 金鑰」。對於 Google Chrome Apps and Extensions，移至 **Web** 標籤，然後適當地配置「傳送端 ID」（FCM/GCM 專案號碼）及「API 金鑰」。
4. 按一下**儲存**。
5. 後續步驟。[啟用 Android 的通知](c_enable_push.html)或[啟用 Google Chrome Apps & Extensions 的通知](c_enable_push.html)。


