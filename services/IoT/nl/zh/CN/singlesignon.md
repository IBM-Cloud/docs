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

# 配置和使用 {{site.data.keyword.ssoshort}}

{{site.data.keyword.ssofull}} 服务可配置为支持将替代用户认证服务提供者用于 {{site.data.keyword.iot_full}}。
{: .shortdesc}

{{site.data.keyword.ssoshort}} 支持 SAML 2.0、IBM Cloud Directory、社交提供者（Facebook、LinkedIn 和 Google+）以及 Github。
有关 {{site.data.keyword.Bluemix_notm}} SSO 服务的更多信息，请参阅[单点登录入门 ![外部链接图标](../../icons/launch-glyph.svg)](https://console.{DomainName}/docs/services/SingleSignOn/index.html){:new_window}。

## 设置 {{site.data.keyword.ssoshort}}

要设置 {{site.data.keyword.ssoshort}}，请执行以下步骤：

1. 在 {{site.data.keyword.Bluemix}}“仪表板”中，添加 {{site.data.keyword.ssoshort}} 服务。
2. 配置将由 {{site.data.keyword.ssoshort}} 服务使用的认证服务提供者。

## 创建哑元应用程序，并将其绑定到 {{site.data.keyword.ssoshort}} 服务

{{site.data.keyword.ssoshort}} 服务无法直接绑定到其他服务，所以必须创建哑元应用程序以从 {{site.data.keyword.ssoshort}} 服务检索必需的配置数据。

1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中，添加 {{site.data.keyword.sdk4nodefull}} 应用程序。
2. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中，单击 {{site.data.keyword.sdk4nodefull}} 应用程序，然后单击**绑定服务或 API**。
3. 选择 {{site.data.keyword.ssoshort}} 服务，然后单击**添加**。
4. 现在，{{site.data.keyword.sdk4nodefull}} 应用程序必须重新编译打包。
5. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中，单击 {{site.data.keyword.sdk4nodefull}} 应用程序。
6. 选择 {{site.data.keyword.ssoshort}} 服务，然后单击**集成**。
7. 输入 Return-to-URL：`https://<orgid>.internetofthings.ibmcloud.com/get-ibmsso-access-token`，其中 `<orgid>` 是您的 {{site.data.keyword.iot_short_notm}} 组织标识。

## 针对 {{site.data.keyword.ssoshort}} 配置 {{site.data.keyword.iot_short_notm}}

绑定并配置 {{site.data.keyword.sdk4nodefull}} 应用程序和 {{site.data.keyword.ssoshort}} 服务后，必须配置 {{site.data.keyword.iot_short_notm}}。可以使用 {{site.data.keyword.iot_short_notm}} UI 或使用 {{site.data.keyword.iot_short_notm}} API 对 {{site.data.keyword.iot_short_notm}} 进行配置。使用 UI 或 API 进行配置之前，必须执行以下步骤：

1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中，单击 {{site.data.keyword.sdk4nodefull}} 应用程序。
2. 单击导航栏中的**环境变量**。
3. 将显示的 JSON 复制到临时文本文件。此 JSON 应该采用以下格式：
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

### 使用 UI 针对 {{site.data.keyword.ssoshort}} 配置 {{site.data.keyword.iot_short_notm}}

1. 打开 {{site.data.keyword.iot_short_notm}} 仪表板。
2. 单击导航栏中的**扩展**。
3. 单击 {{site.data.keyword.ssoshort}} 图标下的**设置**。
4. 在 clientID、secret 和 issuerIdentifier 字段中，输入临时文本文件中的配置数据。
5. 单击**完成**。

### 使用 API 针对 {{site.data.keyword.ssoshort}} 配置 {{site.data.keyword.iot_short_notm}}

要使用 API 针对 {{site.data.keyword.ssoshort}} 配置 {{site.data.keyword.iot_short_notm}}，方法必须为 `POST`，URL 必须为 `https://<orgID>.internetofthings.ibmcloud.com/api/v0002/authentication/ssoconfig`，其中 `<orgID>` 是您的 {{site.data.keyword.iot_short_notm}} 组织标识。授权必须为“无授权”或使用 API 密钥的标识和令牌的“基本授权”。主体必须将 `secret`、`clientId` 和 `issuerIdentifier` 配置数据包含为以下格式的 JSON：
```
{
 "secret": "myclientpwd",
 "clientId": "myclientid",
 "issuerIdentifier": "mybmssoinstance.iam.ibmcloud.com"
}
```

如果 API 调用成功，将返回状态 200。
