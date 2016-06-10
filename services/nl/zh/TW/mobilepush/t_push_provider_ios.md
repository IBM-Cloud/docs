
---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# 配置 Apple Push Notifications (APNs) 的認證

{: #create-push-credentials-apns}

Apple Push Notification Service (APNs) 容許應用程式開發人員將遠端通知從 Bluemix（提供者）上的「Push 服務」實例傳送給 iOS 裝置及應用程式。訊息會傳送至裝置上的目標應用程式。請取得並配置 APNs 認證。APNs 憑證是透過 Push Notification Service 安全地進行管理，並且用來連接至作為提供者的 APNs 伺服器。

1. 取得 [Apple Developer](https://developer.apple.com/) 帳戶。
2. [登錄應用程式 ID](#create-push-credentials-apns-register)
3. [建立開發及配送 APNs SSL 憑證](#create-push-credentials-apns-ssl)
4. [建立開發佈建設定檔](#create-push-credentials-dev-profile)
5. [建立市集配送佈建設定檔](#create-push-credentials-apns-distribute_profile)
6. [在 Push 儀表板上設定 APNs](#create-push-credentials-apns-dashboard)



##登錄應用程式 ID
{: #create-push-credentials-apns-register}


「應用程式 ID」（軟體組 ID）是可識別特定應用程式的唯一 ID。每一個應用程式都需要「應用程式 ID」。Push Notifications Service 這類服務會配置為「應用程式 ID」。




1. 移至 [Apple Developer](https://developer.apple.com) 入口網站，按一下 **Member Center**，然後選取 **Certificates, Identifiers & Profiles**。
2. 移至 [Apple Developer Library](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW991) 中的 **Registering App IDs** 區段，遵循指示來登錄「應用程式 ID」。

	**附註**：登錄「應用程式 ID」時，請選取下列選項：
	* Push Notifications

	![應用程式服務](images/appID_appservices_enablepush.jpg)

	* 明確 ID 字尾

	![明確 ID](images/appID_bundleID.jpg)
3. 後續步驟。建立開發及配送 APNs SSL 憑證。

##建立開發及配送 APNs SSL 憑證
{: #create-push-credentials-apns-ssl}

您必須先產生憑證簽署要求 (CSR) 並將它提交給 Apple（憑證管理中心，CA），才能取得 APNs 憑證。CSR 所含的資訊可識別您的公司，以及您用來簽署 Apple 推送通知的公開和私密金鑰。然後，在「iOS 開發者入口網站」上產生 SSL 憑證。憑證以及其公開和私密金鑰都儲存在「金鑰鏈存取」中。

**開始之前**

[登錄應用程式 ID](#create-push-credentials-apns-register)

您可以透過兩種模式來使用 APNs：沙盤推演及正式作業。

* 沙盤推演模式是在開發及測試期間使用。
* 透過「應用程式市集」（或其他企業配送機制）配送應用程式時，會使用正式作業模式。

您必須取得開發及配送環境的個別憑證。憑證是與接收遠端通知之應用程式的「應用程式 ID」相關聯。對於正式作業，您最多可以建立兩個憑證。Bluemix 使用憑證來建立與 APNs 的 SSL 連線。

建立開發及配送 SSL 憑證。


1. 移至 [Apple Developer](https://developer.apple.com)，按一下 **Member Center**，然後選取 **Certificates, Identifiers & Profiles**。
2. 在 **Identifiers** 區域中，按一下 **App IDs**。
3. 從您的應用程式 ID 清單中，選取新建立的「應用程式 ID」，然後選取 **Settings**。
4. 在 **Push Notifications** 區域中，依序建立「開發 SSL」憑證及「正式作業 SSL」憑證。
 
	![Push Notification SSL 憑證](images/certificate_createssl.jpg)

	即會顯示「關於建立憑證簽署要求」畫面。

	![建立憑證簽署要求](images/request.jpg)

5. 在 Mac 上，啟動**金鑰鏈存取**應用程式，以建立「憑證簽署要求 (CSR)」。
6. 選取**金鑰鏈存取 > 憑證助理 > 從憑證管理中心要求憑證…** ![金鑰鏈存取](images/keychain_request_certificate.jpg)
7. 在**憑證資訊**中，輸入與「應用程式開發者」帳戶相關聯的電子郵件位址及通用名稱。請提供有意義的名稱，協助您識別它是用於開發（沙盤推演）還是配送（正式作業）的憑證；例如，**sandbox_apns_certificate** 或 **production_apns_certificate**。

8. 選取**已儲存至磁碟**，以將 **.certSigningRequest** 檔案下載至您的桌面，然後按一下**繼續**。
9. 在**另存新檔**中，命名 **.certSigningRequest** 檔案（例如 **sandbox.certSigningRequest**），然後按一下**儲存**。
10. 按一下**完成**。您現在有 CSR。
11. 從**關於建立憑證簽署要求 (CSR)** 中，按一下**繼續**。12. ![憑證簽署要求](images/request.jpg)
12. 從**產生**畫面中，按一下**選擇檔案...**，然後選取您儲存在桌面上的 CSR 檔案。然後，按一下**產生**。

	![產生憑證](images/generate_certificate.jpg)

13. 您的憑證備妥之後，請按一下**完成**。
14. 在 **Push Notifications** 畫面上，按一下**下載**以下載您的憑證，然後按一下**完成**。![下載憑證](images/certificate_download.jpg)
15. 在 Mac 上，移至**金鑰鏈存取 > 我的憑證**，然後尋找新安裝的憑證。按兩下憑證，以將它安裝至「金鑰鏈存取」。
16. 選取憑證及私密金鑰，然後選取**匯出**，以將憑證轉換為個人資訊交換格式（.p12 格式）。

	![匯出憑證及金鑰](images/keychain_export_key.jpg)

17. 在**另存新檔**欄位中，提供有意義的憑證名稱，讓您之後可以進行識別（例如 **sandbox_apns.p12_certifcate** 或 **production_apns.p12**），然後按一下**儲存**。

   	![匯出憑證及金鑰](images/certificate_p12v2.jpg)

18. 在**輸入密碼**欄位中，輸入密碼以保護匯出的項目，然後按一下**確定**。您可以使用此密碼，稍後在 Push 儀表板上配置 APNs 設定。

	![匯出憑證及金鑰](images/export_p12.jpg)
19. **Key Access.app** 會提示您從**金鑰鏈**畫面匯出金鑰。請輸入您的管理密碼，以便 Mac 容許您的系統匯出這些項目，然後選取**一律容許**選項。在桌面上會產生 .p12 憑證。


##建立開發佈建設定檔
{: #create-push-credentials-dev-profile}

佈建設定檔與「應用程式 ID」搭配使用，以判定可安裝及執行應用程式的裝置以及您的應用程式可存取的服務。對於每一個「應用程式 ID」，您可以建立兩個佈建設定檔：一個用於開發，另一個用於配送。Xcode 使用開發佈建設定檔來判定容許建置應用程式的開發人員，以及容許在應用程式上進行測試的裝置。

**開始之前**

請確定您已登錄「應用程式 ID」、已針對 Push Notification Service 予以啟用，以及配置它來使用開發及正式作業 APNs SSL 憑證。

建立開發佈建設定檔。

1. 移至 [Apple Developer](https://developer.apple.com) 入口網站，按一下 **Member Center**，然後選取 **Certificates, Identifiers & Profiles**。
2. 移至 [Mac Developer Library](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW62site)，捲動至 **Creating Development Provisioning Profiles** 區段，然後遵循指示來建立開發設定檔。

	**附註**：配置開發佈建設定檔時，請選取下列選項：
	* **iOS 應用程式開發**
	* **對於 iOS 及 watchOS 應用程式**



##建立市集配送佈建設定檔
{: #create-push-credentials-apns-distribute_profile}

使用市集佈建設定檔，將要進行配送的應用程式提交給「應用程式市集」。

1. 移至 [Apple Developer](https://developer.apple.com) 入口網站，按一下 **Member Center**，然後選取 **Certificates, Identifiers & Profiles**。
2. 按兩下下載的佈建設定檔，以將它安裝至 Xcode。

##在 Push Notifications 儀表板上設定 APNs
{: #create-push-credentials-apns-dashboard}

若要使用 Push Notification Service 來傳送通知，請上傳 Apple Push Notification Service (APNs) 所需的 SSL 憑證。您也可以使用 REST API 來上傳 APNs 憑證。


**開始之前**


請取得開發及正式作業 APNs SSL 憑證，以及與每一種憑證類型相關聯的密碼。如需相關資訊，請參閱「建立及配置 APNs 的推送認證」。

APNs 所需的憑證是 .p12 憑證，其中包含私密金鑰以及建置和發佈應用程式所需的 SSL 憑證。您必須從 Apple Developer 網站的 Member Center 產生憑證（這需要有效的 Apple Developer 帳戶）。開發環境（沙盤推演）和正式作業（配送）環境需要個別憑證。

**附註**：.**cer** 位於您的金鑰鏈存取之後，請將它匯出至您的電腦，以建立 .p12 憑證。

如需使用 APNs 的相關資訊，請參閱 [iOS Developer Library: Local and Push Notification Programming Guide](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html#//apple_ref/doc/uid/TP40008194-CH104-SW4)。

在 Push 儀表板上設定 APNs。

1. 在 Bluemix 儀表板中開啟後端應用程式，然後按一下 **IBM Push Notifications** 服務來開啟 Push 儀表板。

	![IBM Push Notifications](images/bluemixdashboard_push.jpg)

	即會顯示 Push 儀表板。
	
	![設定推送通知](images/wizard.jpg)
1
2. 在**配置**標籤上，移至 **Apple 推送憑證**區段，選取**沙盤推演**（開發）或**正式作業**（配送），然後將 p.12 憑證上傳至 Bluemix。

	![設定推送通知](images/credential_screen.jpg)
3. 在**密碼**欄位中，輸入與 **.p12** 憑證檔案相關聯的密碼，然後按一下**儲存**。
使用有效的密碼順利上傳憑證之後，您就可以開始傳送通知。

