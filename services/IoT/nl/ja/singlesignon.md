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

# {{site.data.keyword.ssoshort}} の構成と使用

{{site.data.keyword.iot_full}} の代替ユーザー認証プロバイダーをサポートするよう {{site.data.keyword.ssofull}} サービスを構成することができます。{: .shortdesc}

{{site.data.keyword.ssoshort}} は、SAML 2.0、IBM Cloud Directory、ソーシャル・プロバイダー (Facebook、LinkedIn、Google+)、および Github をサポートします。
{{site.data.keyword.Bluemix_notm}} SSO サービスについて詳しくは、[Getting started with Single Sign On ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://console.{DomainName}/docs/services/SingleSignOn/index.html){:new_window} を参照してください。

## {{site.data.keyword.ssoshort}} のセットアップ

{{site.data.keyword.ssoshort}} をセットアップするには、以下の手順に従います。

1. {{site.data.keyword.Bluemix}} ダッシュボードで、{{site.data.keyword.ssoshort}} サービスを追加します。
2. {{site.data.keyword.ssoshort}} サービスによって使用される認証プロバイダーを構成します。

## ダミー・アプリケーションを作成して {{site.data.keyword.ssoshort}} サービスにバインドする作業

{{site.data.keyword.ssoshort}} サービスを他のサービスに直接バインドすることはできないため、{{site.data.keyword.ssoshort}} サービスから必要な構成データを取得するためにダミー・アプリを作成する必要があります。

1. {{site.data.keyword.Bluemix_notm}} ダッシュボードから、{{site.data.keyword.sdk4nodefull}} アプリケーションを追加します。
2. {{site.data.keyword.Bluemix_notm}} ダッシュボードから {{site.data.keyword.sdk4nodefull}} アプリケーションをクリックし、**「サービスまたは API のバインド」**をクリックします。
3. {{site.data.keyword.ssoshort}} サービスを選択し、**「追加」**をクリックします。
4. ここで、{{site.data.keyword.sdk4nodefull}} アプリケーションを再ステージングする必要があります。
5. {{site.data.keyword.Bluemix_notm}} ダッシュボードから、{{site.data.keyword.sdk4nodefull}} アプリケーションをクリックします。
6. {{site.data.keyword.ssoshort}} サービスを選択し、**「インテグレーション (Integrate)」**をクリックします。
7. 戻り先 URL: `https://<orgid>.internetofthings.ibmcloud.com/get-ibmsso-access-token` を入力します。`<orgid>` は {{site.data.keyword.iot_short_notm}} 組織 ID です。


## {{site.data.keyword.ssoshort}} 用の {{site.data.keyword.iot_short_notm}} の構成

{{site.data.keyword.sdk4nodefull}} アプリケーションと {{site.data.keyword.ssoshort}} サービスをバインドして構成した後、{{site.data.keyword.iot_short_notm}} を構成する必要があります。{{site.data.keyword.iot_short_notm}} は、{{site.data.keyword.iot_short_notm}} UI または {{site.data.keyword.iot_short_notm}} API を使用して構成することができます。UI または API のいずれかを使用して構成する前に、以下の手順を実行しておく必要があります。

1. {{site.data.keyword.Bluemix_notm}} ダッシュボードから、{{site.data.keyword.sdk4nodefull}} アプリケーションをクリックします。
2. ナビゲーション・バーから**「環境変数」**をクリックします。
3. 表示された JSON を一時テキスト・ファイルにコピーします。JSON は次の形式になるはずです。
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

### UI の使用による {{site.data.keyword.ssoshort}} 用の {{site.data.keyword.iot_short_notm}} の構成

1. {{site.data.keyword.iot_short_notm}} ダッシュボードを開きます。
2. ナビゲーション・バーから**「拡張」**をクリックします。
3. {{site.data.keyword.ssoshort}} アイコンの下の**「セットアップ」**をクリックします。
4. 一時テキスト・ファイルの clientID、secret、issuerIdentifier フィールドにある構成データを入力します。
5. **「完了」**をクリックします。

### API の使用による {{site.data.keyword.ssoshort}} 用の {{site.data.keyword.iot_short_notm}} の構成

API を使用して {{site.data.keyword.ssoshort}} 用に {{site.data.keyword.iot_short_notm}} を構成するには、メソッドは `POST` で、URL は `https://<orgID>.internetofthings.ibmcloud.com/api/v0002/authentication/ssoconfig` にする必要があります。`<orgID>` は、{{site.data.keyword.iot_short_notm}} 組織 ID です。API キーの ID およびトークンを使用して、許可を「認証なし (No Auth)」または「基本認証 (Basic Auth)」にする必要があります。本文には、以下の形式で JSON として、構成データ `secret`、`clientId`、`issuerIdentifier` を含める必要があります。
```
{
 "secret": "myclientpwd",
 "clientId": "myclientid",
 "issuerIdentifier": "mybmssoinstance.iam.ibmcloud.com"
}
```

API 呼び出しが正常に行われると、200 という状況が返されます。
