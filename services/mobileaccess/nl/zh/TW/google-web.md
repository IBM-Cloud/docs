---

copyright:
  year: 2016, 2017
lastupdated: "2017-01-08"

---

# 啟用 Web 應用程式的 Google 鑑別
{: #google-auth-web}

在 Web 應用程式上使用「Google 登入」來鑑別使用者。


## 開始之前
{: #before-you-begin}

您必須具有：
* Web 應用程式。
* {{site.data.keyword.amashort}} 服務所保護的 {{site.data.keyword.Bluemix_notm}} 應用程式實例。如需如何建立 {{site.data.keyword.Bluemix_notm}} 後端的相關資訊，請參閱[開始使用](index.html)。

## 配置網站的 Google 應用程式
若要開始使用 Google 作為身分提供者，請在 [Google Developer Console](https://console.developers.google.com) 中建立專案。
建立專案的一部分是取得「Google 用戶端 ID」和「密碼」。「Google 用戶端 ID」和「密碼」是 Google 鑑別所使用之您的應用程式的唯一 ID，並且是設定 {{site.data.keyword.Bluemix_notm}} 應用程式的必要項目。

1. 使用 Google+ API 建立專案。
1. 使用 **OAuth** 建立認證。若要建立認證，您需要：
    * 選取 **Web 應用程式**應用程式類型。
    * 提供**授權重新導向 URI** 值：

     https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback
1. 完成認證建立作業，並記下「Google 用戶端 ID」和「密碼」。


## 配置 {{site.data.keyword.amashort}} 進行 Google 鑑別
有了「Google 應用程式 ID」和「密碼」之後，即可在 {{site.data.keyword.amashort}} 儀表板中啟用 Google 鑑別。

1. 在 {{site.data.keyword.Bluemix_notm}} 儀表板中開啟應用程式。
1. 按一下 {{site.data.keyword.amashort}} 磚。即會載入 {{site.data.keyword.amashort}} 儀表板。
1. 按一下 Google 磚。
1. 輸入「Google 用戶端 ID」和「密碼」，然後儲存。


## 使用 {{site.data.keyword.amashort}} 進行 Google Web 鑑別
若要開始授權處理程序，請執行下列動作：

1. 從您的 Web 應用程式重新導向至授權伺服器的下列端點：  
  https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  使用下列查詢參數：
	```
   response_type='authorization_code'
   client_id= <bluemix_app_guid>
   redirect_uri= <uri which you want to return to after getting a grant code>
   scope= 'openid'
   state= <state>
	```

  `state` 參數目前未在使用中，可以保留為空白。

  `redirect_uri` 參數是使用 Google 進行成功或失敗鑑別之後的重新導向 URI。重新導向之後所取得的回應包含要求查詢參數中的授權碼。
1. 對授權伺服器記號端點提出 `POST` 要求：

 https://imf-newauthserver.bluemix.net/oauth/v2/token


  使用下列查詢參數：

	```
  	grant_type='authorization_code'
    client_id= < bluemix_app_guid >
    redirect_uri= <redirect_uri >
    code= <authorization code>
	```
`redirect_uri` 參數必須符合步驟 1 中的 `redirect_uri`，而 `<authorization code>` 值是接收自回應。因為授權碼的有效時間最多為 10 分鐘，所以請一定要在 10 分鐘內傳送此 `POST` 要求。

`POST` 回應內文應該包含以 base64 編碼的 `access_token` 及 `id_token`。

## 測試鑑別

現在，您可以開始對受保護資源提出要求。所有對受保護資源的要求都應該在授權要求標頭欄位中包含存取記號。
