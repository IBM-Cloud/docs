---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# 保護後端資源
{: #protecting-resources}

{{site.data.keyword.appid_short}} 伺服器 SDK 提供策略來保護兩種類型的資源：API 及 Web 應用程式。
{:shortdesc}


## 從用戶端 SDK 存取受保護資源
{: #accessing}

呼叫受保護資源會啟動登入小組件（必要的話）。如果已取得有效記號，則不會啟動登入小組件，並且會直接存取資源。


### 使用 Swift SDK
{: #requesting-swift notoc}

1. 匯入 BMSCore。

  ```swift
  import BMSCore
  ```
  {:pre}

2. 呼叫受保護的資源要求。

  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //code handling the response here
  })
  ```
  {:pre}


### 使用 Android SDK
{: #requesting-android notoc}

1. 呼叫受保護的資源要求。

  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
	public void onSuccess (Response response) {
		//code handling the response here
  }
  @Override
	public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
		//code handling the failure here
  });
  ```
  {:pre}



## 授權過濾器
{: #auth-filter}

API 保護策略會傳回 HTTP 401 回應，其具有可取得未經鑑別用戶端授權的範圍清單。Web 應用程式保護策略會傳回 HTTP 302 重新導向。重新導向會將未經鑑別的用戶端傳送至 {{site.data.keyword.appid_short_notm}} 服務所管理的登入頁面，或直接傳送至身分提供者登入頁面（視您的配置而定）。



### API 策略
{: #api notoc}

API 策略預期要求要包含具有有效存取記號的授權標頭。回應也可以包括身分記號，但它不是必要項目；請參閱[存取及身分記號](/docs/services/appid/about.html#acess-and-identity)。

如果記號無效或過期，則 API 策略會傳回包含下列資訊的 HTTP 401 錯誤：Www-Authenticate=Bearer scope="{scope}" error="{error}"。`error` 是選用元件。

如果要求傳回有效的記號，則會將控制權傳遞給下一個中介軟體，並將 `appIdAuthorizationContext` 內容注入要求物件。此內容包含原始存取及身分記號，以及作為一般 JSON 物件的解碼有效負載資訊。


### Web 應用程式策略
{: #web notoc}

Web 應用程式策略類別偵測到未經鑑別的受保護資源存取嘗試時，會自動將使用者的瀏覽器重新導向至鑑別頁面。成功鑑別之後，使用者會回到 Web 應用程式的回呼 URL。此服務會使用 Web 應用程式策略類別來取得存取及身分記號。取得這些記號之後，Web 應用程式策略類別會將它們儲存在 HTTP 階段作業的 `WebAppStrategy.AUTH_CONTEXT` 下方。使用者可以決定是否將存取及身分記號儲存在應用程式資料庫中。

## 授權標頭
{: #auth-header}

送入要求中的授權標頭包含三個由空格區隔的部分：Bearer、Access Token 及 ID Token。Access Token 是必要元件，而 ID Token 是選用元件。預期的標頭結構為：Authorization=Bearer {access_token} [{id_token}]
