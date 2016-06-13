
---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# 配置 Google Cloud Messaging (GCM) 的認證
{: #create-push-enable-gcm}

取得 Google Cloud Messaging (GCM) 認證，然後在 Push 儀表板上設定 Push Notification Service。

##取得傳送端 ID 及 API 金鑰

API 金鑰會安全地儲存並供 Push Notification Service 用來連接至 GCM 伺服器，而 Android SDK 在用戶端上使用傳送端 ID（專案號碼）。如需傳送端 ID 的相關資訊，請參閱 [Google Cloud Message](https://developers.google.com/cloud-messaging/gcm#arch)。

1. 在 [Google Dev Console](https://console.developers.google.com/start){: new_window} 上取得一個 Google Development 帳戶。如需 Google Cloud Messaging (GCM) 的相關資訊，請參閱[建立 Google API 專案](https://developers.google.com/console/help/new/){: new_window}。

2. 在 Google Developers Console 上，建立新的專案。例如，"hello world"。

	![建立專案](images/gcm_createproject.jpg)

3. 在**專案名稱**中，輸入您專案的名稱，然後按一下**建立**按鈕。
4. 按一下**首頁**，以檢視專案號碼。請記錄您的專案號碼。

	![GCM 專案號碼](images/gcm_projectnumber.jpg)

	**附註**：當您建立專案時，會建立專案號碼（傳送端 ID）。使用此號碼，可在 Push 儀表板畫面上設定 Push Notification Service。

5. 按一下 **API 及鑑別**，然後按一下**行動式 API** 區段中的 **Cloud Messaging for Android**。

	![API](images/gcm_mobileapi.jpg)

6. 按一下 **API**，然後按一下**啟用 API** 按鈕，以建立您專案的 API 金鑰。

	![啟用 API ](images/gcm_enable_api.jpg)

7. 移至 **API 及鑑別 -> 認證**畫面。按一下**新增認證**，然後按一下 **API 金鑰**。

	![API 認證](images/api_credentials.jpg)

8. 按一下**伺服器金鑰**選項，以在 Bluemix Push 儀表板上產生您將使用的 GCM API 金鑰。
9. 在**名稱**欄位中，輸入伺服器 API 金鑰的名稱。

	![GCM 伺服器金鑰](images/gcm_serverkey.jpg)

10. 按一下**建立**按鈕。即會顯示 API 金鑰。

	![GCM API 金鑰](images/gcm_apikey.jpg)

11. 複製 GCM API 金鑰，然後按一下**確定**按鈕。您將需要專案號碼（傳送端 ID）及 API 金鑰，以在「Bluemix Push Notification 儀表板配置」畫面上配置認證。 
12. 後續步驟。設定適用於 Android 的 Push Notifications Service。

##設定適用於 Android 的 Push Notifications Service

**開始之前**

取得 GCM API 金鑰及傳送端 ID（專案號碼）。 

1. 在 Bluemix 儀表板中開啟後端應用程式，然後按一下 IBM Push Notifications 服務來開啟 Push Notifications Service 儀表板。
 
	![Push 儀表板](images/bluemixdashboard_push.jpg)

	即會顯示 Push 儀表板。
	
	![Push 設定](images/setup_push_main.jpg)

2. 按一下**設定 Push** 按鈕，以配置 GCM 認證。
1. 在**配置**標籤上，移至 **Google Cloud Messaging** 區段，然後配置「傳送端 ID」（GCM 專案號碼）及「API 金鑰」。

4. 按一下**儲存**按鈕。 
5. 後續步驟。[啟用 Android 的通知](c_enable_push.html)。
