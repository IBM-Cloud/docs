---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 配置 Safari Web 瀏覽器的認證
{: #configure-credential-for-safari}
前次更新：2016 年 12 月 6 日
{: .last-updated}

IBM {{site.data.keyword.mobilepushshort}} Service 現在擴充功能，可將通知傳送至您的 Safari 瀏覽器。請注意，支援的版本為 Safari 10.0。

## 產生憑證
  {: #certificate-generation}

請確定您具有 Apple Developer 帳戶。您需要登錄一個 Website Push ID 並產生一個憑證，才能配置 Safari 瀏覽器來接收通知。下列步驟將協助您開始使用。

1. 在 Apple Developer Member Center 中，按一下 **Certificates, ID & Profiles**。 
2. 依序按一下 **Identifiers** 及 **Website Push IDs**。
3. 選取加號圖示來選擇建立新的項目。
  ![Push 儀表板](images/safari_1.jpg)

4. 在 Register Website Push ID 畫面中，提供適當的 Website Push ID 說明及識別 ID。建議採用反向網域名稱格式，起始於 'web'。例如：web.com.example.dailyweatherreports。
5. 登錄 Website Push ID。您現在有了自己的 Website Push ID。 
6. 選取 **Edit** 以建立憑證，用於 Website Push ID。
7. 在 Certificate Information 的 Certificate Assistant 視窗中，提供您的電子郵件 ID 及通用名稱。讓 Certificate Authority 的電子郵件位址保留為空白。
8. 按一下 **Save to disk**，然後選取 **Continue**。
9. 選擇將憑證儲存至適當的資料夾。
10. 選擇在精靈中被提示產生憑證時，在磁碟上建立的 `.certSigningRequest`。請確定您下載以 `. cer` 格式建立的網站推送憑證。
11. 在 KeyChain Access 工具中開啟憑證。按一下滑鼠右鍵並匯出為 p12 憑證。請記下在產生 p12 憑證的期間所提供的密碼。


## 配置通知
  {: #configuration-notification}
 
產生憑證之後，您可以配置服務以傳送通知給 Safari。 

請完成下列步驟：

1. 在 Push Notifications 服務儀表板中，按一下**配置**。 
2. 選取 Web 標籤。 
3. 在 Safari Push 區段中，使用必要的資訊更新表單。 
	- **網站名稱**：這是您在通知中心提供的名稱。
	- **Website Push ID**：使用 Website Push ID 的反向網域字串來更新。例如，web.com.example.www。
	- **網站 URL**：提供應該訂閱推送通知的網站 URL。例如，https://www.example.com。
	- **接受的網域**這是選用性的參數。這是向使用者要求許可權的網站清單。請確定 URL 是以逗點區隔的值。請注意，如果未提供此值，將會使用網站 URL 的值。 
	- **URL 格式字串**：按一下通知時要解析的 URL。例如，["https://www.example.com"]。請確定 URL 使用 http 或 https 方法。
	- **Safari Web 推送憑證**：上傳 .p12 憑證並提供密碼。
4. 按一下**儲存**。	

![Push 儀表板](images/push_configure_safari.jpg)	

現在，您已配置好將推送通知傳送到 Safari 瀏覽器。

	
