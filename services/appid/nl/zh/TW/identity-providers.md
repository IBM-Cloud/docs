---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# 配置身分提供者
{: #setting-up-idp}

您可以配置 Facebook 及（或）Google 來鑑別應用程式，以及授權受保護後端資源的存取權。
{:shortdesc}


## Facebook
{: #facebook}

配置 {{site.data.keyword.appid_short}} 服務，以使用 Facebook 作為身分提供者。

<!--- ### Sequence diagram
{: #facebook-sequence-diagram}--->

### 從 Facebook 取得應用程式 ID 及密碼
{: #getting-facebook-appid}

若要使用 Facebook 作為行動或 Web 應用程式上的身分提供者，您必須在 Facebook 應用程式上新增及配置網站平台。

1. 在 Facebook for Developers 網站上登入您的帳戶。如需建立新 Facebook 應用程式的相關資訊，請參閱<a href="https://developers.facebook.com/docs/apps/register" target="_blank">建立應用程式 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。
2. 記下 Facebook 應用程式 ID 及密碼。在服務儀表板中，您需要這些值來配置 Web 專案以進行鑑別。
3. 新增 Web 平台，並輸入網站 URL。
4. 從產品清單中，選取 **Facebook 登入**。
5. 在「有效 OAuth 重新導向 URL」欄位中，輸入授權伺服器回呼端點 URL。您可以在後續步驟中配置 {{site.data.keyword.appid_short_notm}} 服務之後，再新增此值。
6. 按一下**儲存變更**。

### 配置 {{site.data.keyword.appid_short_notm}} 進行 Facebook 鑑別
{: #configuring-facebook-appid}

若您具有 Facebook 應用程式 ID 及密碼，並已配置 Facebook for Developers 應用程式來服務 Web 用戶端，即可在服務儀表板中編輯 Facebook 鑑別。

1. 從服務儀表板的**管理**標籤中，選取 **Facebook**，然後按一下**編輯**。
2. 輸入自 Facebook for Developers 網站取得的 Facebook 應用程式 ID 及密碼。
3. 複製 **Facebook for Developers 的重新導向 URI** 欄位中的 URI。將 URI 貼入 Facebook Developers 入口網站的 **Facebook 登入**區段中的**有效 OAuth 重新導向 URI** 欄位。
4. 按一下**儲存**。
5. 選用項目：若要配置 Web 應用程式的鑑別，請在「Web 應用程式重新導向 URI」中輸入重新導向 URI。此值是由開發人員所判定，並且用來在授權處理程序完成之後存取重新導向 URI。


## Google
{: #google}

配置 {{site.data.keyword.appid_short_notm}} 服務，以使用 Google 作為身分提供者。

<!--- ### Sequence diagram
{: #google-sequence-diagram}--->

### 從 Google 取得用戶端 ID 及密碼
{: #google-client-id}

若要使用 Google 作為身分提供者，請取得 Google 用戶端 ID 及密碼，並在 Google Developer Console 中建立專案。

1. 在 Google Developer Console 中，開啟 Google 應用程式。
2. 新增 Google+ API。
3. 使用 OAuth 建立認證。在**應用程式類型**欄位中，選取 **Web 應用程式**。在**授權重新導向 URI** 欄位中，輸入「應用程式 ID 重新導向 URI」。您可以從服務儀表板的 Google 配置畫面中取得「應用程式 ID 重新導向授權 URI」。
4. 儲存變更。記下 Google 用戶端 ID 及密碼。




### 配置 {{site.data.keyword.appid_short_notm}} 進行 Google 鑑別
{: #google-client-appid}

若您具有 Google 用戶端及密碼，並已配置 Google Developers 主控台來服務 Web 用戶端，即可在服務儀表板中編輯 Google 鑑別。

1. 從服務儀表板的**管理**標籤中，選取 **Google**，然後按一下**編輯**。
3. 輸入自 Google Developers 主控台取得的「Google 用戶端 ID」及「密碼」。
4. 複製 **Google for Developers 的重新導向 URI** 欄位中的 URI。將 URI 貼入**授權重新導向 URI** 欄位，此欄位位於 Google Developers 入口網站的 **Web 應用程式的用戶端 ID** 區段的**限制**下方。
5. 按一下**儲存**。
6. 選用項目：若要配置 Web 應用程式的鑑別，請在「Web 應用程式重新導向 URI」欄位中輸入重新導向 URI。此值是由開發人員所判定，並且用來在授權處理程序完成之後存取重新導向 URI。



<!---[## Bring your own OAuth2/OIDC identity provider
{: #oauth2}

### About
{: #oauth2-about}
### Sequence diagram
{: #oauth2-sequence-diagram}
### Configuring AppID for BYOIDP OAuth2 authentication
{: #oauth2-appid} SHAWNA: Is this Interconnect?]--->
