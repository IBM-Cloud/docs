---

copyright:
  years: 2015, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Facebook 資格情報を使用したユーザーの認証
{: #facebook-auth-overview}

最終更新日: 2016 年 7 月 22 日
{: .last-updated}

Facebook を ID プロバイダーとして使用してリソースを保護するように、{{site.data.keyword.amashort}} サービスを構成できます。モバイル・アプリケーションまたは Web アプリケーションのユーザーは、ユーザー自身の Facebook 資格情報を認証に使用できます。
{:shortdesc}

**重要**: Facebook が提供する Client SDK を別個にインストールする必要はありません。Facebook SDK は、{{site.data.keyword.amashort}} Facebook Client SDK を構成するときに、依存関係マネージャーによって自動的にインストールされます。

## {{site.data.keyword.amashort}} の要求フロー
{: #mca-facebook-sequence}

### モバイル・クライアント要求フロー

{{site.data.keyword.amashort}} がモバイル・クライアント・アプリからの認証のためにどのように Facebook と統合するのかを理解するために、次のダイアグラムを参照してください。

![モバイル・クライアント要求フロー・ダイアグラム](images/mca-sequence-facebook.jpg)

* {{site.data.keyword.amashort}} Client SDK を使用して、{{site.data.keyword.amashort}} Server SDK によって保護されているバックエンド・リソースへの要求を実行します。
* {{site.data.keyword.amashort}} Server SDK が無許可の要求を検出し、HTTP 401 コードと許可スコープを返します。
* {{site.data.keyword.amashort}} Client SDK は自動的に HTTP 401 コードを検出し、認証プロセスを開始します。
* {{site.data.keyword.amashort}} Client SDK は {{site.data.keyword.amashort}} サービスに連絡し、許可ヘッダーを要求します。
* {{site.data.keyword.amashort}} サービスは、まず認証チャレンジを提供することで、Facebook で認証を行うようクライアントに要求します。
* {{site.data.keyword.amashort}} Client SDK は Facebook SDK を使用して認証プロセスを開始します。認証が成功した後、Facebook SDK は Facebook アクセス・トークンを返します。
* Facebook アクセス・トークンは認証チャレンジ応答とみなされます。このトークンは、{{site.data.keyword.amashort}} サービスに送信されます。
* 当該サービスが Facebook サーバーを使用してこの認証チャレンジ応答を検証します。
* 検証が成功した場合、{{site.data.keyword.amashort}} サービスは認証ヘッダーを生成し、それを {{site.data.keyword.amashort}} Client SDK に戻します。認証ヘッダーには 2 つのトークンが含まれます。アクセス許可情報を含むアクセス・トークンと、現行のユーザー、デバイス、およびアプリケーションについての情報を含む ID トークンです。
* この時点から、{{site.data.keyword.amashort}} Client SDK を介して実行されるすべての要求には、新しく取得した許可ヘッダーが含まれます。
* {{site.data.keyword.amashort}} Client SDK は、認証フローをトリガーしたオリジナルの要求を自動的に再送します。
* {{site.data.keyword.amashort}} Server SDK は要求から認証ヘッダーを抽出し、{{site.data.keyword.amashort}} サービスを使用してそれを検証してから、バックエンド・リソースに対するアクセスを認可します。

### {{site.data.keyword.amashort}} Web アプリケーション要求フロー
{: #mca-facebook-web-sequence}

{{site.data.keyword.amashort}} Web アプリケーション要求フローは、モバイル・クライアントのフローに似ています。ただし、{{site.data.keyword.amashort}} は、{{site.data.keyword.Bluemix_notm}} バックエンド・リソースではなくて Web アプリケーションを保護します。

  * 最初の要求は Web アプリケーションによって (例えばログイン・フォームから) 送信されます。
  * 最終のリダイレクトは、バックエンド保護リソースではなく Web アプリケーション自体の保護領域へのリダイレクトです。 


## Facebook Developer Portal からの Facebook Application ID の取得
{: #facebook-appID}

Facebook を ID プロバイダーとして使用し始めるには、Facebook Developer Portal でアプリケーションを作成する必要があります。このプロセスにおいて、ユーザーは Facebook Application ID を取得します。この ID は、どのアプリケーションが接続しようとしているのかを Facebook に知らせるための固有 ID です。

1. [Facebook Developer Portal](https://developers.facebook.com) を開きます。

1. メニューで**「マイ・アプリ」**をクリックして**「新規アプリの作成 (Create a new app)」**を選択します。
iOS アプリケーションまたは Android アプリケーションのいずれかを選択し、次の画面で**「スキップしてアプリ ID を作成 (Skip and Create App ID)」**をクリックします。

1. 任意のアプリケーション表示名を設定し、カテゴリーを選択します。**「アプリ ID の作成 (Create App ID)」**をクリックして先に進みます。

1. 表示される**「アプリ ID (App ID)」**をコピーします。この値が Facebook Application ID です。モバイル・アプリまたは Web アプリで Facebook 認証を構成する際にこの値が必要になります。

## 次のステップ
{: #next-steps}

* [Android アプリ用の Facebook 認証の使用可能化](facebook-auth-android.html)
* [iOS アプリ用の Facebook 認証の使用可能化 (Swift SDK)](facebook-auth-ios-swift-sdk.html)
* [iOS アプリ用の Facebook 認証の使用可能化 (Objective-C SDK - 非推奨)](facebook-auth-ios.html)
* [Cordova アプリ用の Facebook 認証の使用可能化](facebook-auth-cordova.html)
