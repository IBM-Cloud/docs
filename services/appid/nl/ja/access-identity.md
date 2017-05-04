---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# アクセス・トークンと識別トークン
{: #access-and-identity}

{{site.data.keyword.appid_short}} は、アクセス・トークンと識別トークンという 2 つのタイプのトークンを使用します。これらのトークンは、<a href="https://jwt.io/introduction/" target="_blank">JSON Web トークン<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>としてフォーマットされます。{:shortdesc}


## アクセス・トークン
{: #access-tokens}

アクセス・トークンによって、{{site.data.keyword.appid_short_notm}} 許可フィルターによって保護されている [バックエンド・リソース](/docs/services/appid/protecting-resources.html)との通信が可能になります。このトークンは JavaScript Object Signing and Encryption (JOSE) 仕様に準拠しています。形式は次のとおりです。

```
Header: {

    "typ": "JOSE", // ヘッダーのタイプ、仕様に従う

    "alg": "RS256", // アルゴリズム、仕様に従う

}
Payload: {

    "iss": "", // 発行者、このトークンを発行した AppID。StringOrURL。

    "sub": "", // 主体、このトークンがだれに対して発行されたのか。ほとんどの場合は userId。

    "aud": "", // 対象者、このトークンがだれのためのものか。OAuth2 client_id。

    "exp: "", // 有効期限のタイム・スタンプ、エポック時間

    "iat": "", // 発行時刻のタイム・スタンプ、エポック時間

    "tenant": "xxx", // トークンの発行対象の AppID の tenantId

    "auth_by": "appid_anon / appid_facebook / appid_google",

    "scope": "", // このトークンの発行範囲

}
```
{:screen}

## 識別トークン
{: #identity-tokens}

識別トークンには名前、E メール、性別、写真、場所などのユーザーに関する情報が含まれます。

```
Header: {

    "typ": "JOSE", // ヘッダーのタイプ、仕様に従う

    "alg": "RS256", // アルゴリズム、仕様に従う

}
Payload: {

    "iss": "", // 発行者、このトークンを発行した AppID。StringOrURL。

    "sub": "", // 主体、このトークンがだれに対して発行されたのか。AppID userid。

    "aud": "", // 対象者、このトークンがだれのためのものか。OAuth2 client_id。

    "exp: "", // 有効期限のタイム・スタンプ、エポック時間

    "iat": "", // 発行時刻のタイム・スタンプ、エポック時間

    "tenant": "xxx", // トークンの発行対象の AppID の tenantId
    "name": "John Smith", // IDP から報告されたユーザーの氏名、必須。

    "email": "js@mail.com", // IDP から報告されたユーザーの E メール、該当する場合のみ

    "gender", "male", // IDP から報告されたユーザーの性別、該当する場合のみ

    "locale": "en", // IDP から報告されたユーザーのロケール、該当する場合のみ

    "picture": "https://url.to.photo", // ユーザーの写真の URL、該当する場合のみ

    "auth_by": "appid_facebook/appid_google", // 認証に使用された IDP の名前、必須

    "identities": [

        "provider: "appid_facebook/appid_google", // 必須

        "id": "unique user id as reported by IDP", // 必須

        "profile": { ... } // IDP から返された JSON オブジェクト、必須

      },

      {...}, {...} // その他のリンクされている ID

    ],

    "oauth_client":{

      "type": "serverapp/mobileapp from client registration", // 必須

      "name": "client_name as reported during client registration", // 必須

      "software_id": "software_id as reported during client registration", // 必須

      "software_version": "software_version as reported during client registration", // 必須

      "device_id": "device_id from client registration", //モバイルのみ

      "device_model": "device_model from client registration", //モバイルのみ

      "device_os": "device_os from client registration", //モバイルのみ

    }

}
```
{:screen}
