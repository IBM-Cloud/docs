---

copyright:
 years: 2015, 2016

---

# 疑難排解
{: #errors}
前次更新：2016 年 11 月 08 日
{: .last-updated}

請使用本節作為一般 {{site.data.keyword.mobilepushshort}} 問題的疑難排解指引。


### 發生內部伺服器錯誤。請與管理者聯絡。（內部錯誤碼：PUSHD102E）

####說明

**說明**：如果您在 2015 年 11 月之前已建立 Push 實例，則可能發生此錯誤。  

####使用者回應

**動作**：若要解決此問題，請刪除 Push 實例然後建立一個新的。

**附註**：當您刪除 Push 實例時，不會保留您的標籤。


### UnauthorizedRegistration

####說明

**說明**：Chrome Web Push 無法與 Firebase Cloud Messaging (FCM) 金鑰搭配使用。如果您從 GCM 移至 FCM 之後無法在 Chrome 上接收 Web Push 通知，這是因為網站先前配置為與 GCM 專案搭配使用，但新的專案是採用 FCM 建立的。用於識別瀏覽器的產生記號是由 Chrome 瀏覽器快取。

**動作**：您可以透過移除 Cookie 並重設瀏覽器的許可權來解決此問題。這將要求許可權以啟用 Push Notifications。 

