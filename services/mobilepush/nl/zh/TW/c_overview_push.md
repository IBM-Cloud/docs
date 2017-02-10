---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 關於 {{site.data.keyword.mobilepushshort}}
{: #overview-push}
前次更新：2017 年 1 月 18 日
{: .last-updated}

IBM {{site.data.keyword.mobilepushshort}} 是您可以用來傳送通知至裝置及平台的一種服務。通知可以使用標籤，以所有應用程式使用者或一組特定使用者及裝置為目標。您可以管理裝置、標籤及訂閱。  

您可以使用下列任一選項來建立連結服務或取消連結服務，請執行下列動作：

- 使用型錄中的 MobileFirst Services Starter 樣板建立 Bluemix 應用程式。這將建立連結至 Bluemix 後端應用程式的 Push Notifications 服務。
- 直接從 Mobile 型錄建立取消連結 Push Notifications 服務。您可以稍後連結至應用程式或甚至選擇使用它來取消連結。 
- 使用 [Mobile 儀表板 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/docs/mobile/services.html "外部鏈結圖示"){: new_window}。

請注意，{{site.data.keyword.mobilepushshort}} 監視標籤不會顯示分析資料。

{{site.data.keyword.mobilepushshort}} Service 現在已啟用 OpenWhisk。如需相關資訊，請參閱 [OpenWhisk](/docs/openwhisk/index.html)。


## {{site.data.keyword.mobilepushshort}} Service 程序
{: #overview_push_process}

行動裝置、Web 瀏覽器用戶端及 Google Chrome Apps and Extensions 可以訂閱及登錄 {{site.data.keyword.mobilepushshort}} Service。啟動時，用戶端應用程式會自行登錄及訂閱 {{site.data.keyword.mobilepushshort}} Service。通知會先分派到 Apple Push Notification Service (APNs) 或 Firebase Cloud Messaging (FCM)/Google Cloud Messaging (GCM) 伺服器，然後傳送給已登錄的行動或瀏覽器用戶端。

![推送概觀](images/overview.jpg)


###行動及瀏覽器應用程式
{: mobile-applications}

啟動時，用戶端應用程式會自行登錄及訂閱 {{site.data.keyword.mobilepushshort}} Service 以接收通知。

###後端應用程式
{: backend-applications}

後端應用程式可以位於內部部署中，也可以位於公用雲端中。後端應用程式會使用 {{site.data.keyword.mobilepushshort}} Service，以將環境定義相關通知傳送給行動及瀏覽器應用程式使用者。不需要後端應用程式，也可以維護及管理用於傳送推送通知的行動裝置、瀏覽器代理程式及使用者資訊。反之，後端應用程式可以使用對其進行管理及維護的 {{site.data.keyword.mobilepushshort}} Service。

###應用程式後端擁有者
{: app-backend-owner}

應用程式後端擁有者會建立可組合 {{site.data.keyword.mobilepushshort}} Service 實例的行動後端應用程式。應用程式後端擁有者也會配置及設定 {{site.data.keyword.mobilepushshort}} Service，以符合使用此服務的後端應用程式以及作為 {{site.data.keyword.mobilepushshort}} 目標的行動及瀏覽器應用程式。

###{{site.data.keyword.mobilepushshort}} Service
{: push-notification-service}

{{site.data.keyword.mobilepushshort}} Service 會管理用於登錄通知之行動裝置及 Web 瀏覽器用戶端的所有相關資訊。此服務讓應用程式不必處理將通知傳送給異質行動及 Web 瀏覽器平台的技術詳細資料，全都在其內進行處理。

###閘道
{: gateways}

IBM {{site.data.keyword.mobilepushshort}} Service 使用平台專用 Push Notifications 雲端服務（例如 FCM/GCM 或 Apple Push Notification Service (APNs)）將通知分派給行動及瀏覽器應用程式。

###推送安全
{: push-security}

{{site.data.keyword.mobilepushshort}} API 透過兩種類型的密碼來進行保護：

- **appSecret**：'appSecret' 會保護一般由後端應用程式所呼叫的 API（例如，傳送 {{site.data.keyword.mobilepushshort}} 的 API，以及配置設定的 API）。
- **clientSecret**：'clientSecret' 會保護一般由行動用戶端應用程式所呼叫的 API。只有一個 API 與使用需要此 'clientSecret' 的相關聯 UserId 登錄裝置有關。從行動用戶端呼叫的其他 API 都不需要 clientSecret。 

連結應用程式與 {{site.data.keyword.mobilepushshort}} Service 時，會將 'appSecret' 及 'clientSecret' 配置給每個服務實例。請參閱 [REST API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://mobile.{DomainName}/imfpush/ "外部鏈結圖示") 文件，以取得如何傳遞密碼以及針對哪些 API 傳遞的相關資訊。

**附註**：只有在使用 userId 欄位登錄或更新裝置時，才需要舊版應用程式來傳遞 clientSecret。行動及瀏覽器用戶端所呼叫的所有其他 API 都不需要 clientSecret。這些舊應用程式可以選擇性地繼續使用 clientSecret 進行裝置登錄或更新呼叫。不過，強烈建議所有用戶端 API 呼叫都強制執行 clientSecret 檢查。若要在現有應用程式中強制執行此作業，則有一個已發佈的新 'verifyClientSecret' API 可供使用。對於新的應用程式，將會對所有用戶端 API 呼叫強制執行 clientSecret 檢查，而且使用 'verfiyClientSecret' API 無法變更此行為。

預設只會在新的應用程式中強制執行用戶端密碼驗證。同時容許現有及新的應用程式，以使用 verifyClientSecret REST API 來啟用或停用用戶端密碼驗證。建議您強制執行用戶端密碼驗證，以避免向可能知道 applicationId 及 deviceId 的使用者公開裝置。

請確定 'clientSecret' 保持機密，而且絕不寫在行動應用程式中。您可以利用各種應用程式起始設定型樣，在應用程式運行環境期間動態地取回 'clientSecret'。序列圖會概述這類可能的型樣。
![Enable_Push](images/init_client_secret.jpg) 

## {{site.data.keyword.mobilepushshort}} 類型
{: #overview-push-types}

###播送
{: broadcast}

用戶端應用程式向 {{site.data.keyword.mobilepushshort}} Service 登錄自己後，就可以開始接收播送。播送通知是訊息，以針對 {{site.data.keyword.mobilepushshort}} Service 跨行動裝置、瀏覽器或者實作為 Chrome 應用程式或延伸規格實例安裝及配置的所有應用程式實例為目標。任何已啟用 {{site.data.keyword.mobilepushshort}} 的應用程式預設都會啟用播送通知。啟用 {{site.data.keyword.mobilepushshort}} Service 的應用程式都會有 Push.ALL 標籤的預先定義訂閱，伺服器會使用此標籤將通知訊息播送給所有裝置。若要傳送使用 Push REST API 的播送通知，請確定在公佈至訊息資源時，"target" 是空的 JSON 檔案。

###標籤型通知
{: tag-based-notifications}

標籤通知是指以所有訂閱特定標籤之裝置為目標的訊息。標籤型通知容許根據主旨區域或主題分段通知。只有在通知是所感興趣的主旨或主題時，通知收件者才能選擇接收通知。因此，標籤型通知提供一種方法來分段收件者。此特性會啟用定義標籤後根據標籤來傳送及接收訊息的能力。訊息只會以訂閱標籤的用戶端應用程式實例（在行動裝置或瀏覽器上，或者作為應用程式或延伸規格）為目標。您必須先建立應用程式的標籤，並設定標籤訂閱，然後起始標籤型通知。若要傳送使用 REST API 的標籤型通知，請確定在公佈至訊息資源時提供 "tagNames"。

###單點播送通知
{: unicast-notifications}

單點播送通知是指以特定裝置或使用者為目標的訊息。以裝置為目標的單點播送通知不需要任何額外的設定，而且預設會在應用程式啟用 {{site.data.keyword.mobilepushshort}} 時予以啟用。

不過，以使用者為目標的單點播送通知需要在登錄用戶端行動裝置或 Web 瀏覽器或 Chrome Apps and Extensions for {{site.data.keyword.mobilepushshort}} 時，關聯使用者 ID 與裝置。   

一般而言，用戶端應用程式會先執行鑑別週期，在此鑑別週期，會針對鑑別服務（例如 [Mobile Client Access](docs/services/mobileaccess/index.html)）鑑別行動應用程式使用者。鑑別成功時，接著會將已鑑別使用者 ID 傳遞至「推送裝置登錄 API」。
若要透過 REST API 傳送單點播送通知，請確定在公佈至訊息資源時已提供 deviceId 或 userId。

###平台型通知
{: platform-based-notifications}

可以設定通知的目標以送達特定的裝置平台。例如，只能將通知只傳送給所有 Android 使用者或 Google Chrome 使用者。若要傳送使用 REST API 的平台型通知，請確定在公佈至訊息資源時已提供目標平台。請將平台指定為陣列。支援的平台如下：
* A (Apple)
* G (Google)
* WEB_CHROME（Google Chrome 瀏覽器 Web 推送）
* WEB_FIREFOX（Mozilla Firefox 瀏覽器 Web 推送）
* WEB_SAFARI（Safari 瀏覽器 Web 推送）
* APPEXT_CHROME (Google Chrome Apps & Extensions)

## {{site.data.keyword.mobilepushshort}} 訊息大小
{: #push-message-size}

{{site.data.keyword.mobilepushshort}} 訊息有效負載大小取決於「閘道」（FCM/GCM、APNs）及用戶端平台所配置的限制。 

### iOS 及 Safari
{: ios-message-size}

若為 iOS 8 以及更新版本，接受的大小上限為 2 KB。Apple Push Notification Service 不會傳送超過此限制的通知。

###Android、Firefox 瀏覽器、Chrome 瀏覽器及 Chrome Apps & Extensions
{: android-message-size}

容許的訊息有效負載大小上限為 4 KB。  
