---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# 使用者設定檔
{: #user-profile}

使用者設定檔是 {{site.data.keyword.appid_short}} 所儲存及維護的實體。設定檔會保留使用者的屬性及身分，而且可以匿名或鏈結至身分提供者所管理的身分。
{:shortdesc}

{{site.data.keyword.appid_short_notm}} 提供 API，以透過匿名方式或使用 OpenId Connect (OIDC) IdP 進行鑑別來登入，請參閱[配置身分提供者](https://console.stage1.ng.bluemix.net/docs/services/appid/identity-providers.html#setting-up-idp)。使用者設定檔屬性 API 端點是 {{site.data.keyword.appid_short_notm}} 所產生的存取記號在登入及授權處理程序期間所保護的資源。


## 儲存、讀取及刪除使用者屬性
{: #storing-data}

{{site.data.keyword.appid_short_notm}} 提供 [REST API](http://mobileclientaccess.stage1.mybluemix.net/swagger-ui/#!/Authorization_Server_V3/authorization) 以對使用者的屬性執行 CRUD 作業，以及適用於 [Android](https://github.com/ibm-cloud-security/appid-clientsdk-android) 及 [Swift](https://github.com/ibm-cloud-security/appid-clientsdk-swift) 行動用戶端的 SDK。


## OAuth 身分
{: #oauth}

呼叫 OAuth 登入 API 時，{{site.data.keyword.appid_short_notm}} 會使用 OAuth 2.0 及 OIDC 通訊協定，以透過選取的身分提供者來授權及鑑別呼叫者。鑑別之後，身分會與 {{site.data.keyword.appid_short_notm}} 使用者記錄相關聯。{{site.data.keyword.appid_short_notm}} 會傳回可用來存取使用者屬性的存取記號，以及保留身分提供者所提供的身分資訊的身分記號。從這個相同身分所鑑別的任何用戶端，都可以存取相同的使用者記錄及其屬性。


## 匿名使用者
{: #anonymous}

以匿名方式登入時，{{site.data.keyword.appid_short_notm}} 會建立標示為匿名的特定使用者記錄。{{site.data.keyword.appid_short_notm}} 會將匿名存取及身分記號傳回給呼叫者。使用匿名存取記號，使用者應用程式可以建立、讀取、更新及刪除使用者記錄中所儲存的屬性。例如，開發人員可以建立應用程式，使用者可以在其中立即開始將項目新增至購物車，而不需要登入。


## 已識別的使用者
{: #identified}

具有身分提供者所提供身分的匿名使用者可以成為已識別的使用者。下列步驟概述從匿名使用者移至已知使用者的流程：

* 開發人員將匿名存取記號傳遞給登入 API。
* {{site.data.keyword.appid_short_notm}} 向身分提供者鑑別呼叫者。
* {{site.data.keyword.appid_short_notm}} 尋找存取記號所定義的匿名使用者記錄，並指派它的身分。
    **附註**：只有在尚未將身分指派給另一位使用者時，才能將相同的身分指派給匿名記錄。如果身分已與另一個 {{site.data.keyword.appid_short_notm}} 使用者相關聯，則存取及身分記號會包含該使用者記錄的相關資訊，並提供其屬性的存取權。透過新的存取記號，無法存取前一個匿名使用者及其屬性。除非記號到期，否則仍然可以透過匿名存取記號來存取這項資訊。開發人員可以選擇要如何合併匿名使用者與已知使用者的匿名屬性。
* 接收自 {{site.data.keyword.appid_short_notm}} 的新存取及身分記號會指向已知使用者，而且身分記號會包含接收自身分提供者的公用資訊。
* 使用者的匿名記號會變成無效。

使用新的存取記號，可以存取此使用者所包含的匿名使用者屬性。您可以新增、變更或刪除新記號。從現在開始，使用者從任何用戶端使用相同的身分登入時，都可以解析及存取使用者與其屬性。


## 資料分隔及加密
{: #data}

{{site.data.keyword.appid_short_notm}} 儲存及加密使用者設定檔屬性。身為多方承租戶服務，每個承租戶都會有一個指定的加密金鑰，而且只會使用該承租戶的金鑰來加密每一個承租戶中的使用者資料。

{{site.data.keyword.appid_short_notm}} 確定專用資訊在儲存之前已進行加密。
