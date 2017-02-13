---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-08"

---

# Web 應用程式自訂鑑別
{: #custom-web}

將自訂鑑別新增至 Web 應用程式

## 開始之前
{: #before-you-begin}

您必須具有：
* 含有 `/apps/:Guid/<RealmName>/handleChallengeAnswer` 端點的 Web 應用程式，其會在鑑別成功時傳回使用者身分。使用者身分 JSON 結構應該如下：

   ```json
  userIdentity: {
  userName: <username>,
  displayName: <displayName>;
 };
```
* {{site.data.keyword.amashort}} 服務所保護的 {{site.data.keyword.Bluemix_notm}} 應用程式實例。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端的相關資訊，請參閱[開始使用](index.html)。



## 配置 {{site.data.keyword.amashort}} 應用程式進行自訂鑑別


1. 在 {{site.data.keyword.Bluemix_notm}} 儀表板中開啟應用程式。
1. 按一下 {{site.data.keyword.amashort}} 磚。即會載入 {{site.data.keyword.amashort}} 儀表板。
1. 按一下「自訂」磚。
1. 輸入**自訂領域**、**自訂身分提供者 URL** 及 **redirect_uri**。按一下「儲存」。



## 使用 {{site.data.keyword.amashort}} 進行自訂 Web 鑑別

若要開始授權處理程序，請執行下列動作：

1. 從您的 Web 應用程式重新導向至授權伺服器的下列端點：

    https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  使用下列查詢參數：
   ```
   response_type='authorization_code'
   client_id= <bluemix\_app\_guid>
   redirect_uri= <uri for the redirect after getting an authorization code>
   scope= 'openid'
   state= <state>
   ```

    `state` 參數目前未使用中，可以將它保留空白。

    `redirect_uri` 參數決定自訂身分提供者成功或失敗鑑別之後的重新導向。

1. 重新導向至授權端點之後，您會取得登入表單。輸入要向身分提供者起始鑑別的使用者名稱和密碼，並對 `redirect_uri` 輸入重新導向。成功鑑別之後所傳回的回應包含要求查詢參數中的授權碼。

4. 對授權伺服器記號端點提出 `POST` 要求：

 https://imf-newauthserver.bluemix.net/*oauth/v2/token

 使用下列查詢參數：
 ```
 grant_type = 'authorization_code'
 client_id = <bluemix_app_guid>
 redirect_uri = <redirect_uri>
 code = <authorization code>
 ```
`redirect_uri` 參數必須符合步驟 1 中的 `redirect_uri`。授權碼是由步驟 2 中的要求所傳回。
  因為授權碼的有效時間最多為 10 分鐘，所以請一定要在 10 分鐘內傳送此 `POST` 要求。

`POST` 回應內文包含以 base64 編碼的 *access_token* 及 *id_token*。

## 測試鑑別


現在，您可以開始對受保護資源提出要求。所有對受保護資源的要求都應該包含 `access_token`。請在 `the-Authorization-request` 標頭欄位中傳送存取記號。
