---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# 許可フィルターと許可ヘッダー
{: #auth}

{{site.data.keyword.appid_short}} サーバー SDK には、API と Web アプリケーションという 2 つのタイプのリソースを保護するための戦略が用意されています。
{:shortdesc}


## 許可フィルター
{: #auth-filter}

API の保護戦略は、非認証クライアントに対する許可を取得するために、適用範囲のリストと共に HTTP 401 応答を戻します。Web アプリケーションの保護戦略は、HTTP 302 リダイレクトを戻します。このリダイレクトにより、構成に応じて非認証クライアントは {{site.data.keyword.appid_short_notm}} サービスがホストするログイン・ページに送られるか、ID プロバイダーのログイン・ページに直接送られます。



### API 戦略
{: #api}

API 戦略では、有効なアクセス・トークンを含む許可ヘッダーが要求に含まれていなければなりません。識別トークンも要求に含めることができますが、これは必須ではありません。[アクセス・トークンと識別トークン](/docs/services/appid/access-identity.html#access-and-identity)を参照してください。

トークンが無効または期限切れの場合、API 戦略は次の情報を含む HTTP 401 エラーを返します: Www-Authenticate=Bearer scope="{scope}" error="{error}"。`error` の部分はオプションです。

要求から有効なトークンが返された場合、制御が次のミドルウェアに渡され、`appIdAuthorizationContext` プロパティーが要求オブジェクト内に挿入されます。このプロパティーには、元のアクセス・トークンと識別トークンに加えて、デコードされたペイロード情報が平文の JSON オブジェクトとして含まれます。


### Web アプリ戦略
{: #web}

Web アプリの戦略クラスは、保護リソースに対する非認証のアクセス試行を検出すると、ユーザーのブラウザーを認証ページに自動的にリダイレクトします。認証に成功すると、ユーザーは Web アプリケーションのコールバック URL に戻されます。サービスは、Web アプリの戦略クラスを使用して、アクセス・トークンと識別トークンを取得します。それらのトークンを取得した後、Web アプリの戦略クラスはそれらを `WebAppStrategy.AUTH_CONTEXT` の下の HTTP セッションに保管します。アクセス・トークンと識別トークンをアプリケーション・データベース内に保管するかどうかは、ユーザーが決定します。

## 許可ヘッダー
{: #auth-header}

着信要求の許可ヘッダーは、Bearer、Access Token、および ID Token の 3 つの部分からなり、各部分は空白で区切られます。Access Token は必須の構成要素ですが、ID Token はオプションです。予期されるヘッダー構造は次のとおりです。Authorization=Bearer {access_token} [{id_token}]
