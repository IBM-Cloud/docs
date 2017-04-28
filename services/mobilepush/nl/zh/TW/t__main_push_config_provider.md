
---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 配置通知提供者的認證
{: #create-push-credentials}
前次更新：2017 年 4 月 12 日
{: .last-updated}

針對行動裝置，若要設定 {{site.data.keyword.mobilepushshort}} Service，您必須先從推送通知提供者（Firebase Cloud Messaging (FCM) 或 Apple Push Notification Service (APNs)）取得需要的認證。 

您可以使用 **IBM Bluemix 服務**儀表板或使用 [REST API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://mobile.{DomainName}/imfpush/){: new_window}，設定 {{site.data.keyword.mobilepushshort}}。


## 配置 FCM 的認證
{: #create-push-enable-gcm}

Firebase Cloud Messaging (FCM) 是用來將推送通知遞送至 Android 裝置及 Google Chrome 的閘道。FCM 是新版本的 Google Cloud Messaging (GCM)。若要在儀表板上設定 {{site.data.keyword.mobilepushshort}} 服務，您需要取得 FCM 認證。請確定將 FCM 配置用於新的應用程式。現有應用程式將繼續使用 GCM 配置運作。

### 取得傳送端 ID 及 API 金鑰
{: #android-senderid-apikey}

API 金鑰會安全地儲存並供 {{site.data.keyword.mobilepushshort}} Service 用來連接至 FCM 伺服器，而適用於 Google Chrome 及 Mozilla Firefox 的 Android SDK 及 JS SDK 在用戶端上使用「傳送端 ID」（專案號碼）。 

若要設定 FCM 以及產生 API 金鑰和「傳送端 ID」，請完成下列步驟：

1. 造訪 [Firebase 主控台 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.firebase.google.com/?pli=1){: new_window}。
2. 選取**建立新專案**。 
3. 在「建立專案」視窗中，提供專案名稱、選擇國家/地區，然後按一下**建立專案**。
3. 在導覽窗格中，按一下「設定」圖示，然後選取**專案設定**。
4. 選擇 Cloud Messaging 標籤，以產生「伺服器 API 金鑰」及「傳送端 ID」。

### 設定適用於 Android 及 Chrome Apps and Extensions 的 Push Notification Service
{: #setup-push-android}

**附註：**您將需要「FCM/GCM API 金鑰」及「傳送端 ID」（專案號碼）。

1. 開啟 Bluemix 儀表板，然後按一下您已建立的 {{site.data.keyword.mobilepushfull}} Service 實例來開啟儀表板。即會顯示 Push 儀表板。若要設定適用於 Android 的未連結 {{site.data.keyword.mobilepushshort}} Service，請選取「未連結 {{site.data.keyword.mobilepushshort}} Service」圖示來開啟 {{site.data.keyword.mobilepushshort}} Service 儀表板。 

![Push 儀表板](images/push_unbound.jpg)

2. 按一下**設定 Push** 按鈕，以配置適用於 Android 應用程式及 Google Chrome Apps and Extensions 的 FCM/GCM 認證。
3. 在**配置**頁面上，對於 Android，移至 **Mobile** 標籤，然後配置「傳送端 ID」（GCM 專案號碼）及「API 金鑰」。對於 Google Chrome Apps and Extensions，移至 **Web** 標籤，然後適當地配置「傳送端 ID」（FCM/GCM 專案號碼）及「API 金鑰」。
4. 按一下**儲存**。
5. 後續步驟。[啟用 Android 的通知](c_enable_push.html)或[啟用 Google Chrome Apps & Extensions 的通知](c_web_extensions.html)。


## 配置 APNs 的認證
{: #create-push-credentials-apns}

Apple Push Notification Service (APNs) 容許應用程式開發人員將遠端通知從 Bluemix（提供者）上的 {{site.data.keyword.mobilepushshort}} Service 實例傳送給 iOS 裝置及應用程式。訊息會傳送至裝置上的目標應用程式。 

請取得並配置 APNs 認證。APNs 憑證是透過 {{site.data.keyword.mobilepushshort}} Service 安全地進行管理，並且用來以提供者身分連接至 APNs 伺服器。

<!-- 1. Obtain an [Apple Developers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.apple.com/){: new_window} account.-->

<!--2. [Register an App ID](#create-push-credentials-apns-register)
3. [Create a development and distribution APNs SSL certificate](#create-push-credentials-apns-ssl)
4. [Create a development provisioning profile](#create-push-credentials-dev-profile)
5. [Create a store distribution provisioning profile](#create-push-credentials-apns-distribute_profile)
6. [Creating .p12 push certificate file for Bluemix push](#create-p12-push-certificate-file-for-Bluemix-push)
7. [Set up APNs on the Push Dashboard](#create-push-credentials-apns-dashboard)
-->


### 登錄應用程式 ID
{: #create-push-credentials-apns-register}


「應用程式 ID」（軟體組 ID）是可識別特定應用程式的唯一 ID。每一個應用程式都需要「應用程式 ID」。{{site.data.keyword.mobilepushshort}} Service 這類服務會配置成「應用程式 ID」。

1. 請確定您有一個 [Apple Developers ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.apple.com/){: new_window} 帳戶。
2. 移至 [Apple Developer ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.apple.com){: new_window} 入口網站，按一下 **Member Center**，然後選取 **Certificates, Identifiers & Profiles**。
3. 移至 [Apple Developer Library ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW991){: new_window} 中的 **Registering App IDs** 區段，遵循指示登錄 App ID。

登錄「應用程式 ID」時，請選取下列選項：

* Push Notifications
![應用程式服務](images/appID_appservices_enablepush.jpg)
* 明確 ID 字尾
![明確 ID](images/appID_bundleID.jpg)
4. 建立開發及配送 APNs SSL 憑證。

### 建立開發及配送 APNs SSL 憑證
{: #create-push-credentials-apns-ssl}

您必須先產生憑證簽署要求 (CSR) 並將它提交給 Apple（憑證管理中心 (CA)），才能取得 APNs 憑證。CSR 所含的資訊可識別您的公司，以及用來簽署 Apple Push Notifications 的公開和私密金鑰。然後，在「iOS 開發者入口網站」上產生 SSL 憑證。憑證以及其公開和私密金鑰都儲存在「金鑰鏈存取」中。

<!-- ###Before you begin -->
<!-- {: before-you-begin-certificate} -->

<!--[Register an App ID](#create-push-credentials-apns-register)-->

您可以透過兩種模式使用 APNs： 

* 沙盤推演模式，用於進行開發及測試。
* 正式作業模式，在透過「應用程式市集」（或其他企業配送機制）配送應用程式時使用。

您必須取得開發及配送環境的個別憑證。憑證是與接收遠端通知之應用程式的「應用程式 ID」相關聯。對於正式作業，您最多可以建立兩個憑證。Bluemix 使用憑證來建立與 APNs 的 SSL 連線。

<!-- Create a development and distribution SSL certificate. -->

1. 移至 [Apple Developer ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.apple.com){: new_window} 網站，按一下 **Member Center**，然後選取 **Certificates, Identifiers & Profiles**。
2. 在 **Identifiers** 區域中，按一下 **App IDs**。
3. 從 App IDs 清單中，選取 <!--newly created--> App ID，然後選取 **Settings**。
4. 在 **Push Notifications** 區域中，依序建立「開發 SSL」憑證及「正式作業 SSL」憑證。

	![Push Notification SSL 憑證](images/certificate_createssl.jpg)

5. 顯示**關於建立憑證簽署要求 (CSR)** 畫面時，請在 Mac 上啟動**金鑰鏈存取**應用程式，以建立「憑證簽署要求 (CSR)」。
6. 從功能表中，選取**金鑰鏈存取 > 憑證助理 > 從憑證管理中心要求憑證...** 
7. 在**憑證資訊**中，輸入與「應用程式開發人員」帳戶及通用名稱相關聯的電子郵件位址。請提供有意義的名稱，協助您識別它是用於開發（沙盤推演）還是配送（正式作業）的憑證；例如，*sandbox-apns-certificate* 或 *production-apns-certificate*。
8. 選取**儲存至磁碟**，以將 `.certSigningRequest` 檔案下載至您的桌面，然後按一下**繼續**。
9. 在**另存新檔**功能表選項中，命名 `.certSigningRequest` 檔案，然後按一下**儲存**。
10. 按一下**完成**。您現在有 CSR。
11. 回到**關於建立憑證簽署要求 (CSR)** 視窗，然後按一下**繼續**。 
12. 從**產生**畫面中，按一下**選擇檔案...**，然後選取您儲存在桌面上的 CSR 檔案。然後，按一下**產生**。![產生憑證](images/generate_certificate.jpg)
13. 您的憑證備妥之後，請按一下**完成**。
14. 在 **Push Notifications** 畫面上，按一下**下載**以下載您的憑證，然後按一下**完成**。![下載憑證](images/certificate_download.jpg)
15. 在 Mac 上，移至**金鑰鏈存取 > 我的憑證**，然後尋找新安裝的憑證。按兩下憑證，以將它安裝至「金鑰鏈存取」。
16. 選取憑證及私密金鑰，然後選取**匯出**，以將憑證轉換為個人資訊交換格式（`.p12` 格式）。
![匯出憑證及金鑰](images/keychain_export_key.jpg)
17. 在**另存新檔**欄位中，提供有意義的憑證名稱（例如，`sandbox_apns.p12_certifcate` 或 `production_apns.p12`），然後按一下**儲存**。
![匯出憑證及金鑰](images/certificate_p12v2.jpg)
18. 在**輸入密碼**欄位中，輸入密碼以保護匯出的項目，然後按一下**確定**。您可以使用此密碼，在 Push 儀表板上配置 APNs 設定。
{: #step18}
	![匯出憑證及金鑰](images/export_p12.jpg)
19. **Key Access.app** 會提示您從**金鑰鏈**畫面匯出金鑰。請輸入您的管理密碼，以便 Mac 容許您的系統匯出這些項目，然後選取**一律容許**選項。`.p12` 憑證會在桌面上產生。


### 建立開發佈建設定檔
{: #create-push-credentials-dev-profile}

佈建設定檔與「應用程式 ID」搭配使用，以判定可安裝及執行應用程式的裝置以及您的應用程式可存取的服務。對於每一個「應用程式 ID」，您可以建立兩個佈建設定檔：一個用於開發，另一個用於配送。Xcode 使用開發佈建設定檔來判定容許建置應用程式的開發人員，以及容許在應用程式上進行測試的裝置。

請確定您已登錄「應用程式 ID」、已針對 {{site.data.keyword.mobilepushshort}} 服務予以啟用，以及配置它來使用開發及正式作業 APNs SSL 憑證。

建立開發佈建設定檔，如下所示：

1. 移至 [Apple Developer ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.apple.com){: new_window} 入口網站，按一下 **Member Center**，然後選取 **Certificates, Identifiers & Profiles**。
2. 移至 [Mac Developer Library ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW62site){: new_window}，捲動至 **Creating Development Provisioning Profiles** 區段，並遵循指示以建立開發設定檔。
**附註**：配置開發佈建設定檔時，請選取下列選項：
	* **iOS 應用程式開發**
	* **對於 iOS 及 watchOS 應用程式**


### 建立市集配送佈建設定檔
{: #create-push-credentials-apns-distribute_profile}

使用市集佈建設定檔，將要進行配送的應用程式提交給「應用程式市集」。

1. 移至 [Apple Developer ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.apple.com){: new_window} 入口網站，按一下 **Member Center**，然後選取 **Certificates, Identifiers & Profiles**。
2. 按兩下下載的佈建設定檔，以將它安裝至 Xcode。

### 在 Push Notification 儀表板上設定 APNs
{: #create-push-credentials-apns-dashboard}

若要使用 {{site.data.keyword.mobilepushshort}} Service 來傳送通知，請上傳 Apple Push Notification Service (APNs) 所需的 SSL 憑證。您也可以使用 REST API 來上傳 APNs 憑證。

<!-- Get your development and production APNs SSL certificate and the password associated with each type of certificate. For information, see Creating and configuring push credentials for APNs.-->

APNs 需要的憑證為 `.p12` 憑證。這些憑證包含私密金鑰以及建置和發佈應用程式所需的 SSL 憑證。您必須從 Apple Developer 網站的 Member Center 產生憑證（這需要有效的 Apple Developer 帳戶）。開發環境（沙盤推演）和正式作業（配送）環境需要個別憑證。

**附註**：`.cer` 檔案位於您的金鑰鏈存取之後，請將它匯出至您的電腦，以建立 `.p12` 憑證。

如需有關使用 APNs 的相關資訊，請參閱 [iOS Developer Library: Local and Push Notification Programming Guide ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html#//apple_ref/doc/uid/TP40008194-CH104-SW4){: new_window}。

若要在 Push Notification Service 儀表板上設定 APNs，請完成以下步驟：

1. 在 Push Notification Service 儀表板上，選取**配置**。
2. 選擇 **Mobile** 選項，以更新 **APNs Push 認證**表單中的資訊。
3. 適當地選取**沙盤推演**（開發）或**正式作業**（配送），然後上傳您使用前一個[步驟](#step18)所建立的 `p.12` 憑證。
![設定 Push Notifications 儀表板](images/wizard.jpg)
3. 在**密碼**欄位中，輸入與 `.p12` 憑證檔案相關聯的密碼，然後按一下**儲存**。


使用有效的密碼順利上傳憑證之後，您就可以開始傳送通知。

## 配置 Web 瀏覽器的認證
{: #configure-credential-for-browsers}

IBM {{site.data.keyword.mobilepushshort}} 服務現在已擴充功能，可將通知傳送至您的瀏覽器。 

{{site.data.keyword.mobilepushshort}} 服務需要您網站的網站 URL 或網域名稱，以識別需要被容許的要求。{{site.data.keyword.mobilepushshort}} 服務實例一次僅支援一個網域名稱。因此，請確保針對 Chrome、Firefox 及 Safari 設定相同的值。 

Chrome 及 Safari 瀏覽器需要其他配置才能進行 Web 推送。您將需要 FCM API 金鑰用作 FCM 端點，用來在 Chrome 中遞送訊息。 


### Chrome 及 Firefox Web 推送的配置 
{: #config-chrome-firefox}

1. 在「Push 儀表板」畫面中，選取**配置**。
2. 選取 Web 標籤。
![WebPush 配置](images/webpush_configure.jpg)
3. 配置 FCM/GCM API 金鑰，以及將登錄以接收推送通知的網站 URL。
4. 按一下**儲存**。
5. 後續步驟。[啟用 Google Chrome 及 Mozilla Firefox 瀏覽器的通知](c_chrome_firefox_enable.html)。


### Safari Web 推送的配置 
{: #configure-safari}

Safari 上 {{site.data.keyword.mobilepushshort}} 服務的支援版本為 10.0。需要透過您的 Apple Developer 帳戶產生憑證，才能配置您的瀏覽器來接收通知。

#### 產生憑證
{: #certificate-generation}

請確定您具有 Apple Developer 帳戶。您需要登錄一個 Website Push ID 並產生一個憑證，才能配置 Safari 瀏覽器來接收通知。下列步驟將協助您開始使用。

1. 在 Apple Developer Member Center 中，按一下 **Certificates, ID & Profiles**。 
2. 依序按一下 **Identifiers** 及 **Website Push IDs**。
3. 選取加號圖示來選擇建立新的項目。
  ![Push 儀表板](images/safari_1.jpg)

4. 在 Register Website Push ID 畫面中，提供適當的 Website Push ID 說明及識別 ID。建議採用反向網域名稱格式，起始於 `web`。例如：`web.com.example.dailyweatherreports`。
5. 登錄 Website Push ID。您現在有了自己的 Website Push ID。 
6. 選取 **Edit** 以建立憑證，用於 Website Push ID。
7. 在 Certificate Information 的 Certificate Assistant 視窗中，提供您的電子郵件 ID 及通用名稱。讓 Certificate Authority 的電子郵件位址保留為空白。
8. 按一下 **Save to disk**，然後選取 **Continue**。
9. 選擇將憑證儲存至適當的資料夾。
10. 選擇在精靈中被提示產生憑證時，在磁碟上建立的 `.certSigningRequest`。請確定您下載以 `. cer` 格式建立的網站推送憑證。
11. 在 KeyChain Access 工具中開啟憑證。按一下滑鼠右鍵並匯出為 p12 憑證。請記下在產生 p12 憑證的期間所提供的密碼。


#### 配置通知
{: #configuration-notification}
 
產生憑證之後，您可以配置服務以傳送通知給 Safari。 

請完成下列步驟：

1. 在 Push Notifications 服務儀表板中，按一下**配置**。 
2. 選取 Web 標籤。 
3. 在 Safari Push 區段中，使用必要的資訊更新表單。 
	- **網站名稱**：這是您在通知中心提供的名稱。
	- **Website Push ID**：使用 Website Push ID 的反向網域字串來更新。例如，`web.com.example.www`。
	- **網站 URL**：提供應該訂閱推送通知的網站 URL。例如，`https://www.example.com`。
	- **接受的網域**這是選用性的參數。這是向使用者要求許可權的網站清單。請確定 URL 是以逗點區隔的值。請注意，如果未提供此值，將會使用網站 URL 的值。 
	- **URL 格式字串**：按一下通知時要解析的 URL。例如，["`https://www.example.com`"]。請確定 URL 使用 http 或 https 方法。
	- **Safari Web 推送憑證**：上傳 .p12 憑證並提供密碼。
4. 按一下**儲存**。	

![Push 儀表板](images/push_configure_safari.jpg)	

現在，您已配置好將推送通知傳送到 Safari 瀏覽器。
