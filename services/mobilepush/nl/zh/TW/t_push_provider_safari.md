
---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# 配置 Safari Web 瀏覽器的認證
{: #configure-credential-for-safari}
前次更新：2016 年 11 月 15 日
{: .last-updated}

IBM {{site.data.keyword.mobilepushshort}} Service 現在擴充功能，可將通知傳送至您的 Safari 瀏覽器。 

請確定您具有 Apple Developer 帳戶。您需要登錄一個 Website Push ID 並產生一個憑證，才能配置 Safari 瀏覽器來接收通知。下列步驟將協助您開始使用。

1. 在 Apple Developer Member Center 中，按一下 **Certificates, ID & Profiles**。 
2. 依序按一下 **Identifiers** 及 **Website Push IDs**。
3. 選取加號圖示來選擇建立新的項目。
  ![Push 儀表板](images/safari_1.jpg)

4. 在 Register Website Push ID 畫面中，提供適當的 Website Push ID 說明及識別 ID。建議採用反向網域名稱格式，起始於 'web'。例如：web.com.example.dailyweatherreports。
5. 登錄 Website Push ID。
6. 選取 **Edit** 來更新 Website Push ID。
7. 在 Certificate Information 的 Certificate Assistant 視窗中，提供您的電子郵件 ID 及通用名稱。讓 Certificate Authority 的電子郵件位址保留為空白。
8. 按一下 **Save to disk**，然後選取 **Continue**。
9. 選擇將憑證儲存至適當的資料夾。

 
