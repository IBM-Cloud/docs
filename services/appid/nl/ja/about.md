---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# {{site.data.keyword.appid_short_notm}} の概要
{: #about}

{{site.data.keyword.appid_full}} を使用すると、開発者は 2、3 行のコードで {{site.data.keyword.Bluemix}} アプリを保護し、アプリに認証を追加することができます。開発者はユーザー固有のデータを管理し、パーソナライズされたアプリ・エクスペリエンスを構築することもできます。
{:shortdesc}


このサービスは、以下の目的のために使用できます。

* モバイル・アプリケーションや Web アプリケーションに認証を追加する
* 保護されたバックエンド・リソースや Web アプリに対するアクセス権を付与する
* {{site.data.keyword.Bluemix_notm}} でホストされている Node.js アプリケーションや Swift アプリケーションを保護する
* アプリの設定や公開用ソーシャル・プロファイルの情報などのユーザー・データを保管する
* 保管されているデータを使用して、パーソナライズされたアプリ・エクスペリエンスを構築する
* 認証ユーザーと匿名ユーザーの両方のリソースを保護する

**注**: 実装されているプロトコルは、OpenID Connect (OIDC) に完全に準拠しています。


## コンポーネント
{: #components}

* ダッシュボード - 学習用のサンプルのダウンロード、アクティビティー・ログの表示、さまざまな認証のタイプと ID プロバイダーの構成を行います。
* クライアント SDK - このサービスを使用してユーザー認証を実装するモバイル・アプリや Web アプリを構築します。
    * Android の前提条件: API 25 以上、Java 8.x、Android SDK Tools 25.2.5 以上、Android SDK Platform Tools 25.0.3 以上、Android Build Tools バージョン 25.0.2
    * iOS の前提条件: iOS9 以上、MacOS 10.11.5、Xcode 8.2
* サーバー SDK - {{site.data.keyword.Bluemix_notm}} 上でホストされているリソースを保護します。
    * サポートされているランタイムは Node.js と Swift です。

## アーキテクチャーの概要

![{{site.data.keyword.appid_short_notm}} アーキテクチャーの図](/images/appid_architecture.png)

図 1. {{site.data.keyword.appid_short_notm}} アーキテクチャーの図

{{site.data.keyword.appid_short_notm}} サーバー SDK を使用してクラウド・リソースを保護できます。保護されたクラウド・リソースと通信するには、{{site.data.keyword.appid_short_notm}} クライアント SDK に用意されている要求クラスを使用します。

* サーバー SDK は、無許可の要求を検出すると、HTTP 401 許可チャレンジを返します。
* クライアント SDK は、HTTP 401 許可チャレンジを検出すると、ID プロバイダーの構成に基づく認証プロセスを自動的に開始します。
* 現在構成されている ID プロバイダーに従って認証が試行されます。
* 認証に成功すると、許可トークンと識別トークンがサービスから返されます。
* クライアント SDK がその許可トークンを元の要求に自動的に追加し、要求をクラウド・リソースに再送します。
* サーバー SDK は、要求からアクセス・トークンを抽出し、{{site.data.keyword.appid_short_notm}} で検証します。アクセス権が付与され、アプリケーションに応答が返されます。


## 要求フロー
{: #request}

以下の図は、要求が Client SDK からバックエンド・アプリケーションおよび ID プロバイダーへどのように流れていくのかを説明したものです。

![{{site.data.keyword.appid_short_notm}} 要求フロー](/images/appidflow.png)


* {{site.data.keyword.appid_short_notm}} Client SDK を使用して、{{site.data.keyword.appid_short_notm}} Server SDK によって保護されているバックエンド・リソースへの要求を実行します。
* {{site.data.keyword.appid_short_notm}} Server SDK は、無許可の要求を検出し、HTTP 401 と許可スコープを返します。
* Client SDK は自動的に HTTP 401 を検出し、認証プロセスを開始します。
* 複数の ID プロバイダーが構成されている場合、Client SDK がサービスに連絡を取ると、Server SDK はログイン・ウィジェットを返します。{{site.data.keyword.appid_short_notm}} は、ID プロバイダーを呼び出してそのプロバイダーのログイン・フォームを提示するか、ID プロバイダーが構成されていない場合には認証のための権限付与コードを返します。
* {{site.data.keyword.appid_short_notm}} は、認証チャレンジを提供することによって、認証を行うようにクライアント・アプリに要求します。
* Facebook または Google が構成されている場合、ユーザーがログインすると、認証はそれぞれの ID プロバイダーの OAuth フローで処理されます。
* 認証が同じ権限付与コードで終了する場合、そのコードがトークン・エンドポイントに送信されます。エンドポイントは、アクセス・トークンと識別トークンという 2 つのトークンを返します。この時点以降、Client SDK で行われたすべての要求には、新しく取得された許可ヘッダーを含まれるようになります。
* Client SDK は、認証フローをトリガーしたオリジナルの要求を自動的に再送します。
* Server SDK は、要求から許可ヘッダーを抽出し、サービスを使用してそのヘッダーを検証し、バックエンド・リソースへのアクセスを認可します。

## アクセス・トークンと識別トークン
{: #access-and-identity}

{{site.data.keyword.appid_short}} は、アクセス・トークンと識別トークンという 2 つのタイプのトークンを使用します。これらのトークンは、<a href="https://jwt.io/introduction/" target="_blank">JSON Web トークン<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>としてフォーマットされます。


### アクセス・トークン
{: #access-tokens notoc}

アクセス・トークンによって、{{site.data.keyword.appid_short_notm}} 許可フィルターによって保護されているリソースとの通信が可能になります。 [バックエンド・リソースの保護](/docs/services/appid/protecting-resources.html)を参照してください。
このトークンは JavaScript Object Signing and Encryption (JOSE) 仕様に準拠しています。形式は次のとおりです。

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

### 識別トークン
{: #identity-tokens notoc}

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


## ID プロバイダーの概要
{: #identity-providers-overview}

モバイル・アプリケーションや Web アプリケーションで以下の ID プロバイダーを使用できます。

* **Facebook** - ユーザーは、Facebook の資格情報を使用してモバイル・アプリや Web アプリにログインします。
* **Google** - ユーザーは、Google+ の資格情報を使用してモバイル・アプリや Web アプリにログインします。
<!--* **Custom** - Bring your own identity provider. The identity providers should be compliant with OIDC. -->

## デフォルト構成の使用
{: #default-configuration}

初めて ID プロバイダーをセットアップするときに、{{site.data.keyword.appid_short_notm}} からデフォルト構成が示されます。このデフォルト構成は開発モードのみで使用できます。ID プロバイダーごとに、これらの資格情報は {{site.data.keyword.appid_short_notm}} インスタンスあたり毎日 100 回の使用に制限されています。アプリケーションを公開する前に、デフォルトの構成を自分の資格情報に更新してください。構成を更新するには、[ID プロバイダーの構成](/docs/services/appid/identity-providers.html)を参照してください。
