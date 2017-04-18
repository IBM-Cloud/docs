---

copyright:
  year: 2016, 2017
lastupdated: "2017-03-15"

---

{{site.data.keyword.amafull}} 服務取代為 {{site.data.keyword.appid_full}} 服務。

# 啟用 Web 應用程式的 Facebook 鑑別
{: #facebook_web}

在 Web 應用程式上使用 Facebook 來鑑別使用者。

## 開始之前
{: #facebook-auth-android-before}
您必須具有：
* Web 應用程式。  
* {{site.data.keyword.amashort}} 服務所保護的 {{site.data.keyword.Bluemix_notm}} 應用程式實例。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端的相關資訊，請參閱[開始使用](index.html)。
* 「Facebook 應用程式 ID」和「應用程式密碼」。如需相關資訊，請參閱[從 Facebook 開發人員入口網站取得 Facebook 應用程式 ID](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)。


## 配置網站的 Facebook 應用程式
若要使用 Facebook 作為網站上的身分提供者，您必須在 Facebook 應用程式上新增及配置網站平台。

1. 在「Facebook 開發人員入口網站」中，開啟 Facebook 應用程式。
1. 記下您應用程式的「應用程式 ID」和「應用程式密碼」。當您配置 Web 專案進行 Facebook 鑑別時，需要此值。
1. 從**設定**頁面中，按一下**新增平台**，然後選擇**網站**。
1. 儲存變更。
1. 按一下資訊看板中的 **Facebook 登入**。
1. 在**有效 OAuth 重新導向 URI** 方框中，輸入授權伺服器回呼端點：`https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback`。儲存變更。




# 配置 {{site.data.keyword.amashort}} 進行 Facebook 鑑別
具有「Facebook 應用程式 ID」和「應用程式密碼」並配置「Facebook 應用程式」來服務 Web 用戶端之後，即可在 {{site.data.keyword.Bluemix_notm}} 儀表板中啟用 Facebook 鑑別。

1. 在 {{site.data.keyword.Bluemix_notm}} 儀表板中開啟應用程式。
1. 按一下 {{site.data.keyword.amashort}} 磚。即會載入 {{site.data.keyword.amashort}} 儀表板。
1. 按一下 Facebook 磚。
1. 輸入「Facebook 應用程式 ID」和「應用程式密碼」，然後儲存。




## 使用 Mobile Client Access 進行 Facebook Web 鑑別

若要開始授權處理程序，請執行下列動作：

1. 從您的 Web 應用程式重新導向至授權伺服器的下列端點：https://imf-newauthserver.bluemix.net/oauth/v2/authorization

1. 新增下列查詢參數：
   ```
    response_type='authorization_code'
    client_id= <bluemix_app_guid>
    redirect_uri= <uri for redirecting after receiving the authorization code>
    scope= 'openid'
    state= <state>
    ```


  `state` 參數目前未在使用中，可以保留為空白。`redirect_uri` 參數是使用 Facebook 進行成功或失敗鑑別之後用於重新導向的 URI。

1. 在重新導向至授權端點之後，您將從 Facebook 取得      
   登入表單。輸入使用者名稱和密碼來重新導向至 `redirect_uri`。
   重新導向之後所取得的回應包含要求查詢參數中的授權碼。

1. 對授權伺服器的記號端點提出 `POST` 要求：

  https://imf-newauthserver.bluemix.net/oauth/v2/token

  使用下列查詢參數：
  ```
  grant_type='authorization_code'
  client_id= <bluemix_app_guid>
  code= <authorization code>
  ```
`redirect_uri` 參數必須符合步驟 2 中的 `redirect_uri`。`code` 值是在步驟 3 結束時回應中收到的授權碼。因為授權碼的有效時間最多為 10 分鐘，所以請一定要在 10 分鐘內傳送此 `POST` 要求。  `POST` 回應內文應該包含以 base64 編碼的 `access_token` 及 `id_token`。

## 測試鑑別
現在，您可以開始對受保護資源提出要求。所有對受保護資源的要求都應該在「授權要求」標頭欄位中包含 `access_token`。
