---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# 仕組み
{: #about}

{{site.data.keyword.appid_short_notm}} を使用するコンポーネント、アーキテクチャー、要求フローについて説明します。
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
{: #architecture}

{{site.data.keyword.appid_short_notm}} を使用すれば、ユーザーにサインインを要求することによって、アプリケーションのセキュリティー・レベルを強化できます。Server SDK を使用してバックエンド・リソースを保護することも可能です。

{{site.data.keyword.appid_short_notm}} サービスの仕組みの概要を以下の図に示します。

![{{site.data.keyword.appid_short_notm}} アーキテクチャーの図](/images/appid_architecture2.png)

図 1. {{site.data.keyword.appid_short_notm}} アーキテクチャーの図

<dl>
  <dt> Client SDK</dt>
    <dd> Client SDK には、クラウド・リソースと通信するための要求クラスが用意されています。Client SDK は、許可チャレンジを検出すると、認証プロセスを自動的に開始します。</dd>
  <dt> Bluemix</dt>
    <dd>  サーバー SDK は、要求からアクセス・トークンを抽出し、{{site.data.keyword.appid_short_notm}} で検証します。認証が成功すると、{{site.data.keyword.appid_short_notm}} から許可トークンと識別トークンがアプリケーションに返されます。</dd>
  <dt> ID プロバイダー</dt>
    <dd> アプリの認証のために、Facebook と Google のいずれかまたは両方を構成できます。</dd>
</dl>


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
