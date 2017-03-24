---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# 關於 {{site.data.keyword.appid_short_notm}}
{: #gettingstarted}

使用 {{site.data.keyword.appid_full}}，開發人員只要透過數行程式碼即可保護其 {{site.data.keyword.Bluemix}} 應用程式並新增對其的鑑別。開發人員也可以管理使用者特定的資料來建置個人化應用程式體驗。
{:shortdesc}


您可以透過下列方式來使用服務：

* 新增對行動及 Web 應用程式的鑑別
* 授與對受保護後端資源及 Web 應用程式的存取權
* 保護 {{site.data.keyword.Bluemix_notm}} 上所裝載的 Node.js 及 Swift 應用程式
* 儲存使用者資料（例如其公用社交設定檔中的應用程式喜好設定或資訊）
* 使用已儲存的資料來建置個人化應用程式體驗
* 保護已鑑別及匿名使用者的資源

**附註**：實作的通訊協定完全符合 OpenID Connect (OIDC) 的標準。


## 元件
{: #components}

* 儀表板 - 下載上線範例、查看活動日誌、配置各種鑑別類型及身分提供者
* 用戶端 SDK - 建置行動及 Web 應用程式，以使用服務來實作使用者鑑別
    * Android 的必要條件：API 25 或更新版本、Java 8.x、Android SDK Tools 25.2.5 或更新版本、Android SDK Platform Tools 25.0.3 或更新版本、Android Build Tools 25.0.2 版
    * iOS 的必要條件：iOS9 或更新版本、MacOS 10.11.5、Xcode 8.2
* 伺服器 SDK - 保護 {{site.data.keyword.Bluemix_notm}} 上所裝載的資源
    * 支援的運行環境是 Node.js 及 Swift

## 架構概觀

![{{site.data.keyword.appid_short_notm}} 流程](/images/appid_flow.png)

圖 1. {{site.data.keyword.appid_short_notm}} 架構圖

您可以使用 {{site.data.keyword.appid_short_notm}} 伺服器 SDK 來保護雲端資源。使用 {{site.data.keyword.appid_short_notm}} 用戶端 SDK 所提供的要求類別，以與受保護的雲端資源通訊。

* 伺服器 SDK 偵測到未獲授權的要求，並傳回 HTTP 401 授權盤查。
* 用戶端 SDK 偵測到「HTTP 401 授權」盤查，並根據身分提供者配置自動啟動鑑別處理程序。
* 根據目前配置的身分提供者來嘗試鑑別。
* 成功鑑別之後，服務會傳回授權及身分記號。
* 用戶端 SDK 將授權記號自動新增至原始要求，並將要求重新傳送至雲端資源。
* 伺服器 SDK 從要求擷取存取記號，並向 {{site.data.keyword.appid_short_notm}} 驗證它。
授與存取權，而且會將回應傳回給應用程式。

<!--## Sequence diagrams
{: #sequence-diagrams}

[Anton?]-->

## 存取及身分記號
{: #access-and-identity}

{{site.data.keyword.appid_short}} 使用兩種類型的記號：存取及身分。記號會格式化為 <a href="https://jwt.io/introduction/" target="_blank">JSON Web 記號 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。


### 存取記號
{: #access-tokens notoc}

存取記號會啟用與 {{site.data.keyword.appid_short_notm}} 授權過濾器所保護資源的通訊，請參閱[保護資源](/docs/services/appid/protecting-resources.html)。
記號符合「JavaScript 物件簽署及加密 (JOSE)」規格，並且具有下列格式：

```
Header: {

    "typ": "JOSE", // header type, according to spec

    "alg": "RS256", // algorithm, according to spec

}
Payload: {

    "iss": "", // issuer, the AppID server that issued this token. StringOrURL

    "sub": "", // subject, who this token was issued to. Most probably userId

    "aud": "", // audience, who is this token intended for. OAuth2 client_id.

    "exp: "", // expiration timestamp, epoch time

    "iat": "", // issued at timestamp, epoch time

    "tenant": "xxx", the AppID tenantId the token was issued for

    "auth_by": "appid_anon / appid_facebook / appid_google",

    "scope": "", // the scope[s] this token was issued for

}
```
{:screen}

### 身分記號
{: #identity-tokens notoc}

身分記號包含使用者的相關資訊，包括姓名、電子郵件、性別、圖片及位置。

```
Header: {

    "typ": "JOSE", // header type, according to spec

    "alg": "RS256", // algorithm, according to spec

}
Payload: {

    "iss": "", // issuer, the AppID server that issued this token. StringOrURL

    "sub": "", // subject, who this token was issued to. AppID userid.

    "aud": "", // audience, who is this token intended for. OAuth2 client_id.

    "exp: "", // expiration timestamp, epoch time

    "iat": "", // issued at timestamp, epoch time

    "tenant": "xxx", // the AppID tenantId the token was issued for

    "name": "John Smith", // user's full name as reported by IDP, mandatory,

    "email": "js@mail.com", // user's email as reported by IDP, only if available,

    "gender", "male", // user's gender as reported by IDP, only if available,

    "locale": "en", // user's locale as reported by IDP, only if available

    "picture": "https://url.to.photo", // URL to user's picture, only if available

    "auth_by": "appid_facebook/appid_google", // the name of IDP used for authentication, mandatory

    "identities": [

        "provider: "appid_facebook/appid_google", // mandatory

        "id": "unique user id as reported by IDP", // mandatory

        "profile": { ... } // JSON object returned by IDP,  mandatory

      },

      {...}, {...} // more linked identities

    ],

    "oauth_client":{

      "type": "serverapp/mobileapp from client registration", // mandatory

      "name": "client_name as reported during client registration", // mandatory

      "software_id": "software_id as reported during client registration", // mandatory

      "software_version": "software_version as reported during client registration", // mandatory

      "device_id": "device_id from client registration", //mobile only

      "device_model": "device_model from client registration", //mobile only

      "device_os": "device_os from client registration", //mobile only

    }

}
```
{:screen}


## 身分提供者概觀
{: #identity-providers-overview}

您可以在行動及 Web 應用程式中使用下列身分提供者：

* **Facebook** - 您的使用者利用其 Facebook 認證來登入行動或 Web 應用程式。
* **Google** - 您的使用者利用其 Google+ 認證來登入行動或 Web 應用程式。
<!--* **Custom** - Bring your own identity provider. The identity providers should be compliant with OIDC. -->

## 使用預設配置
{: #default-configuration}

{{site.data.keyword.appid_short_notm}} 會在您一開始設定身分提供者時提供預設配置。您只能在開發模式中使用預設配置。對於每一個身分提供者，這些認證限制為每天每個 {{site.data.keyword.appid_short_notm}} 實例可以使用 100 次。發佈應用程式之前，請將預設配置更新為您自己的認證。若要更新您的配置，請參閱[配置身分提供者](/docs/services/appid/identity-providers.html)。
