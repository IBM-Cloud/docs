---

copyright:
 years: 2015, 2016

---

# 關於 Push Notifications
{: #overview-push}

Push Notifications 是一項服務，您可以用來傳送通知給 iOS 及 Android 裝置。通知可以使用標籤，以所有應用程式使用者或一組特定使用者及裝置為目標。您可以管理裝置、標籤及訂閱。您也可以使用 SDK（軟體開發套件）及「具象狀態傳輸 (REST)」應用程式介面 (API) 來進一步開發用戶端應用程式。如需 Push 專用服務的相關資訊，請參閱[專用服務](../../dedicated/index.html)。 


## Push Notification Service 程序
{: #overview_push_process}

行動式用戶端可以訂閱及登錄 Push Notification Service。在啟動時，行動式應用程式會自行登錄及訂閱 Push Notification Service。通知會先分派到 Apple Push Notification Service (APNs) 或 Google Cloud Messaging (GCM) 伺服器，然後傳送給已登錄的行動式用戶端。

![推送概觀](images/overview.jpg)


###行動式應用程式

在啟動時，行動式應用程式會自行登錄及訂閱 Push Notification Service 以接收通知。

###後端應用程式

後端應用程式可以位於內部部署中，也可以位於公用雲端中。後端應用程式會使用 Push Notification Service 將環境定義相關通知傳送給行動使用者。不需要後端應用程式，也可以維護與管理用於傳送推送通知的行動式裝置及使用者資訊。相反地，後端應用程式可以使用 Push Notification Service。

###應用程式後端擁有者

已建立可組合 Push Notification Service 實例之行動式後端應用程式的角色。此人員會配置及設定 Push Notification Service，以符合使用 Push Notification Service 的後端應用程式，以及本身為推送通知目標的行動式應用程式。

###Push Notification Service

Push Notification Service 會管理與登錄通知的裝置相關的所有資訊。此服務讓應用程式不必處理將通知傳送給這些異質行動式平台的技術詳細資料，全都在其內進行處理。

###閘道

行動式裝置平台專用雲端服務（例如 Google Cloud Messaging (GCM) 或 Apple Push Notification Service (APNs)）使用 Push Notification Service 將通知分派給行動式應用程式。

## 推送通知類型
{: #overview-push-types}

###播送

當行動式應用程式向 Push Notification Service 登錄自己後，就可以開始接收播送。播送通知是指以所有已安裝應用程式並針對 Push Notification Service 進行配置之裝置為目標的通知訊息。任何已啟用推送通知的應用程式預設都會啟用播送通知。任何啟用 Push Notification Service 的應用程式都會有 Push.ALL 標籤的預先定義訂閱，而伺服器會使用此標籤將通知訊息播送給所有裝置。若要傳送使用 Push REST API 的播送通知，請確定在公佈至訊息資源時，"target" 是空的 JSON 檔案。

###標籤型通知

標籤通知是指以所有訂閱特定標籤之裝置為目標的通知訊息。標籤型通知容許根據主旨區域或主題分段通知。只有在通知是所感興趣的主旨或主題時，通知收件者才能選擇接收通知。因此，標籤型通知提供一種方法來分段收件者。此特性會啟用定義標籤後根據標籤來傳送及接收訊息的能力。訊息只會以訂閱標籤的裝置為目標。您必須先建立應用程式的標籤、設定標籤訂閱，然後起始標籤型通知。若要傳送使用 REST API 的標籤型通知，請確定在公佈至訊息資源時提供 "tagName"。

###單點播送通知

單點播送通知是以特定裝置為目標的通知訊息。單點播送通知不需要任何額外的設定，而且預設會在應用程式啟用推送通知時予以啟用。若要傳送使用 REST API 的單點播送通知，請確定在公佈至訊息資源時已提供 deviceId。

###平台型通知

可以設定通知的目標以送達特定的裝置平台。例如，可以將通知只傳送給所有 Android 使用者。若要傳送使用 REST API 的平台型通知，請確定在公佈至訊息資源時已提供目標平台。請將平台指定為陣列。支援的平台如下：
* A (Apple)
* G (Google)
