---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# 授權過濾器及標頭
{: #auth}

{{site.data.keyword.appid_short}} 伺服器 SDK 提供策略來保護兩種類型的資源：API 及 Web 應用程式。
{:shortdesc}


## 授權過濾器
{: #auth-filter}

API 保護策略會傳回 HTTP 401 回應，其具有可取得未經鑑別用戶端授權的範圍清單。Web 應用程式保護策略會傳回 HTTP 302 重新導向。重新導向會將未經鑑別的用戶端傳送至 {{site.data.keyword.appid_short_notm}} 服務所管理的登入頁面，或直接傳送至身分提供者登入頁面（視您的配置而定）。



### API 策略
{: #api}

API 策略預期要求要包含具有有效存取記號的授權標頭。回應也可以包括身分記號，但它不是必要項目；請參閱[存取及身分記號](/docs/services/appid/access-identity.html#access-and-identity)。

如果記號無效或過期，則 API 策略會傳回包含下列資訊的 HTTP 401 錯誤：Www-Authenticate=Bearer scope="{scope}" error="{error}"。`error` 是選用元件。

如果要求傳回有效的記號，則會將控制權傳遞給下一個中介軟體，並將 `appIdAuthorizationContext` 內容注入要求物件。此內容包含原始存取及身分記號，以及作為一般 JSON 物件的解碼有效負載資訊。


### Web 應用程式策略
{: #web}

Web 應用程式策略類別偵測到未經鑑別的受保護資源存取嘗試時，會自動將使用者的瀏覽器重新導向至鑑別頁面。成功鑑別之後，使用者會回到 Web 應用程式的回呼 URL。此服務會使用 Web 應用程式策略類別來取得存取及身分記號。取得這些記號之後，Web 應用程式策略類別會將它們儲存在 HTTP 階段作業的 `WebAppStrategy.AUTH_CONTEXT` 下方。使用者可以決定是否將存取及身分記號儲存在應用程式資料庫中。

## 授權標頭
{: #auth-header}

送入要求中的授權標頭包含三個由空格區隔的部分：Bearer、Access Token 及 ID Token。Access Token 是必要元件，而 ID Token 是選用元件。預期的標頭結構為：Authorization=Bearer {access_token} [{id_token}]
