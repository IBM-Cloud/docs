---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---

{:shortdesc: .shortdesc}
{:codeblock:.codeblock}

**重要: {{site.data.keyword.amafull}} サービスは {{site.data.keyword.appid_full}} サービス**に置き換えられます。

# {{site.data.keyword.amashort}} サービスを使用したバックエンド・リソースの保護
{: #protecting-resources}


{{site.data.keyword.amafull}} サービスでは、モバイル対応の OAuth セキュリティーおよびモニタリングにより、{{site.data.keyword.Bluemix_notm}} 上で稼働している、Node.js および Java ベースのバックエンド・アプリケーションを保護することができます。
{:shortdesc}

## 開始する前に
{: #before-you-begin}
開始する前に、Node.js サービスが {{site.data.keyword.Bluemix_notm}} バックエンド・アプリケーションに存在していることを確認してください。


## 許可フィルター
{: #auth-filter}
{{site.data.keyword.amashort}} Server SDK には、バックエンド・アプリケーションを保護するために使用できる許可フィルターがあります。許可フィルターは着信要求を代行受信し、許可ヘッダーがあるかどうか確認します。許可ヘッダーがないか無効な場合、フィルターは HTTP 401 で応答を返します。{{site.data.keyword.amashort}} Client SDK は、{{site.data.keyword.amashort}} Server SDK によって返される HTTP 401 応答の代行受信方法を知っており、認証フローをトリガーします。
## 許可ヘッダー
{: #auth-header}
着信要求の許可ヘッダーは、Bearer、Access Token、および ID Token の 3 つの部分からなり、各部分は空白で区切られます。`Access Token` は必須コンポーネントですが、`ID Token` はオプションです。

着信許可ヘッダーは、それぞれの許可フィルターによって処理されます。フィルターは、アクセス・トークンと ID トークンの署名、有効期限、および構造保全性を検証します。検証にパスすると、セキュリティー・コンテキスト・オブジェクトが要求オブジェクトに追加されます。セキュリティー・コンテキストの参照は、関連する API を使用して取得できます。

セキュリティー・コンテキストには、以下の構造で保管されたサブジェクト、ユーザー、デバイス、およびアプリケーション情報が含まれています。
```JSON
{
    "imf.sub":"myclientid",
    "imf.user": {
        "id":"user-name",
        "authBy":"myrealm",
        "displayName":"display-name"
    },
    "imf.device": {
        "id":"device-id",
        "platform":"iOSnative",
        "model":"device-model",
        "osVersion":"device-os"
    },
    "imf.application": {
        "id":"ios.bundle.id",
        "version":"1.0"
    }
}
```
{: codeblock}

* `imf.sub`: ID トークンのサブジェクト、または ID トークンがない場合は、クライアントの固有 ID のサブジェクトを指定します。
* `imf.user`: ID トークンから抽出されたユーザー ID を指定します。ID トークンがない場合、このフィールドには空のオブジェクトが入ります。
* `imf.device`: ID トークンから抽出されたデバイス ID を指定します。ID トークンがない場合、このフィールドには空のオブジェクトが入ります。
* `imf.application`: ID トークンから抽出されたアプリケーション ID を指定します。ID トークンがない場合、このフィールドには空のオブジェクトが入ります。

## 次のステップ
{: #next-steps}
* [Node.js リソースの保護](protecting-resources-nodejs.html)
* [Liberty for Java&trade; リソースの保護](protecting-resources-java.html)
* [ローカル開発](protecting-resources-local.html)
