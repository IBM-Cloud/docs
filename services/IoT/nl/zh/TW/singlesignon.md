---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 配置及使用 {{site.data.keyword.ssoshort}}

{{site.data.keyword.ssofull}} 服務可以配置成支援 {{site.data.keyword.iot_full}} 的替代使用者鑑別提供者。
{: .shortdesc}

{{site.data.keyword.ssoshort}} 支援 SAML 2.0、IBM Cloud Directory、社交提供者（Facebook、LinkedIn、Google+）及 Github。
如需 {{site.data.keyword.Bluemix_notm}} SSO 服務的相關資訊，請參閱[開始使用 Single Sign On ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://console.{DomainName}/docs/services/SingleSignOn/index.html){:new_window}。

## 設定 {{site.data.keyword.ssoshort}}

若要設定 {{site.data.keyword.ssoshort}}，請遵循下列步驟：

1. 在 {{site.data.keyword.Bluemix}} 儀表板中，新增 {{site.data.keyword.ssoshort}} 服務。
2. 配置要供 {{site.data.keyword.ssoshort}} 服務使用的鑑別提供者。

## 建立虛擬的應用程式，並將它連結至 {{site.data.keyword.ssoshort}} 服務

{{site.data.keyword.ssoshort}} 服務無法直接連結至其他服務，因此必須建立虛擬的應用程式，才能從 {{site.data.keyword.ssoshort}} 服務擷取必要的配置資料。

1. 從 {{site.data.keyword.Bluemix_notm}} 儀表板中，新增 {{site.data.keyword.sdk4nodefull}} 應用程式。
2. 從 {{site.data.keyword.Bluemix_notm}} 儀表板中，按一下 {{site.data.keyword.sdk4nodefull}} 應用程式，然後按一下**連結服務或 API**。
3. 選取 {{site.data.keyword.ssoshort}} 服務，然後按一下**新增**。
4. 現在必須重新編譯打包 {{site.data.keyword.sdk4nodefull}} 應用程式。
5. 從 {{site.data.keyword.Bluemix_notm}} 儀表板中，按一下 {{site.data.keyword.sdk4nodefull}} 應用程式。
6. 選取 {{site.data.keyword.ssoshort}} 服務，然後按一下**整合**。
7. 輸入 Return-to-URL：
`https://<orgid>.internetofthings.ibmcloud.com/get-ibmsso-access-token`，其中 `<orgid>` 是 {{site.data.keyword.iot_short_notm}} 組織 ID。

## 配置 {{site.data.keyword.ssoshort}} 的 {{site.data.keyword.iot_short_notm}}

連結及配置 {{site.data.keyword.sdk4nodefull}} 應用程式和 {{site.data.keyword.ssoshort}} 服務之後，必須配置 {{site.data.keyword.iot_short_notm}}。使用 {{site.data.keyword.iot_short_notm}} 使用者介面或使用 {{site.data.keyword.iot_short_notm}} API，可以配置 {{site.data.keyword.iot_short_notm}}。使用使用者介面或 API 配置之前，必須採取下列步驟：

1. 從 {{site.data.keyword.Bluemix_notm}} 儀表板中，按一下 {{site.data.keyword.sdk4nodefull}} 應用程式。
2. 從導覽列中，按一下**環境變數**。
3. 將顯示的 JSON 複製到暫存文字檔。JSON 的格式應該如下：
```
{
  "SingleSignOn": [
    {
        "name": "ssoServiceTest",
        "label": "SingleSignOn",
        "plan": "standard"
        "credentials": {
          "secret": "string",
          "tokenEndpointUrl": "string",
          "authorizationEndpointUrl": "string",
          "issuerIdentifier": "string",
          "clientId": "string",
          "serverSupportedScope": [
              "openid"
          ]
        }
    }
}
```

### 使用使用者介面配置 {{site.data.keyword.ssoshort}} 的 {{site.data.keyword.iot_short_notm}}

1. 開啟 {{site.data.keyword.iot_short_notm}} 儀表板。
2. 從導覽列中，按一下**延伸規格**。
3. 按一下 {{site.data.keyword.ssoshort}} 圖示下方的**設定**。
4. 在 clientID、secret 及 issuerIdentifier 欄位中，輸入暫存文字檔中的配置資料。
5. 按一下**完成**。

### 使用 API 配置 {{site.data.keyword.ssoshort}} 的 {{site.data.keyword.iot_short_notm}}

若要使用 API 配置 {{site.data.keyword.ssoshort}} 的 {{site.data.keyword.iot_short_notm}}，方法必須是 `POST`、URL 必須是 `https://<orgID>.internetofthings.ibmcloud.com/api/v0002/authentication/ssoconfig`，其中 `<orgID>` 是 {{site.data.keyword.iot_short_notm}} 組織 ID。授權必須是使用 API 金鑰 ID 及記號的「無鑑別」或「基本鑑別」。內文必須以下列格式包含 JSON 形式的 `secret`、`clientId` 及 `issuerIdentifier` 配置資料：
```
{
 "secret": "myclientpwd",
 "clientId": "myclientid",
 "issuerIdentifier": "mybmssoinstance.iam.ibmcloud.com"
}
```

如果 API 呼叫成功，則會傳回狀態 200。
