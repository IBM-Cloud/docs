---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.amashort}} 概説
       
{: #gettingstarted}

{{site.data.keyword.amafull}} サービスを使用して、セキュリティーをモバイル・アプリに追加します。{{site.data.keyword.Bluemix}} で実行されている保護されたバックエンド・リソースにアクセスするためのクライアント許可を構成できます。ID プロバイダー (Google および Facebook) またはカスタム ID を使用して、ユーザーを認証し、保護されたバックエンド・リソースおよび Web アプリに対するアクセスを許可します。
{:shortdesc}

**注:** {{site.data.keyword.amashort}} サービスの以前の名称は Advanced Mobile Access でした。


{{site.data.keyword.amashort}} サービスを起動して稼働させるには、次のようにします。

1. 以下のいずれかのオプションを使用して、バインドまたはアンバインドされたサービスを作成します。
 * カタログから **MobileFirst Services Starter** ボイラープレートを使用して、{{site.data.keyword.Bluemix_notm}} アプリケーションを作成します。これにより、{{site.data.keyword.Bluemix_notm}} バックエンド・アプリケーションにバインドされた {{site.data.keyword.amashort}} サービスが作成されます。
 * {{site.data.keyword.amashort}} コンソールを使用して、{{site.data.keyword.amashort}} サービスを作成します。サービスを既存のバックエンド・アプリケーションにバインドし、{{site.data.keyword.amashort}} コンソールで構成することができます。

   MobileFirst Services Starter を使用すると、カスタム・バックエンド・ロジックを実装するために、IBM {{site.data.keyword.Bluemix_notm}} で稼働する Node.js ランタイムのインスタンスを取得します。セキュリティー、データ、プッシュ、およびモニターの各機能を提供する一連のコア・モバイル・サービスは、その Node.js アプリにバインドされています。{{site.data.keyword.Bluemix_notm}} Node.js アプリが作成されたら、 開発環境をセットアップし、{{site.data.keyword.Bluemix_notm}} モバイル・サービスの SDK の使用を開始できます。SDK を使用すると、単純な API 呼び出しを使用して、クラウド・アプリにバインドされているサービスにアクセスできます。

	プロジェクト、アプリケーション、およびサービスの作成方法と処理方法について詳しくは、[IBM Bluemix モバイル・ダッシュボード](https://console.{DomainName}/docs/mobile/index.html)を参照してください。

2. サーバー・サイド・リソースを保護します。

   Node.js ランタイムまたは Liberty for Java&trade; ランタイムで稼働しているモバイル・バックエンド・リソースを、モバイル対応の OAuth セキュリティーによって保護します。詳しくは、[リソースの保護](protecting-resources.html)を参照してください。デフォルトのモバイル・バックエンド・アプリケーションについての詳細は、[bms-hellotodo-strongloop ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop "外部リンク・アイコン"){: new_window} サンプル・アプリケーションを参照してください。

3. コア {{site.data.keyword.amashort}} 開発環境をセットアップします。

  ####クライアント開発
  {: #client-development}

	以下のように、既存の Android アプリ、iOS アプリ、または Cordova アプリに {{site.data.keyword.amashort}} SDK を追加できます。
   * Android: ([Android SDK のセットアップ](getting-started-android.html)) [サンプル![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication "外部リンク・アイコン"){: new_window}
    * iOS (Swift SDK): ([iOS Swift SDK のセットアップ](getting-started-ios-swift-sdk.html)) [サンプル![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "外部リンク・アイコン"){: new_window}    
   * Cordova: ([Cordova plug-in のセットアップ](getting-started-cordova.html)) [サンプル![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication "外部リンク・アイコン"){: new_window}


 ####Web 開発
 {: #web-development}

   {{site.data.keyword.amashort}} サービスは、特別な SDK を必要とせずに、Web アプリケーションを保護することができます。{{site.data.keyword.amashort}} サービスによって提供される保護に加えて、さまざまな ID プロバイダーを活用できます。{{site.data.keyword.amashort}} 統合によって、実装されているテクノロジーに関係なくどのような Web アプリケーションであっても、OAuth2 プロトコルを利用することが可能になります。さまざまな ID プロバイダーを使用して {{site.data.keyword.amashort}} サービスにアクセスするための {{site.data.keyword.amashort}} Web アプリケーションのセットアップについて詳しくは、以下を参照してください。

   * [Web アプリケーション用の Facebook 認証の使用可能化](facebook-auth-web.html)
   * [Web アプリケーション用の Google 認証の使用可能化](google-auth-web.html)
   * [Web アプリケーション用のカスタム認証の使用可能化](custom-auth-web.html)

**オプション:** アプリケーションの ID プロバイダーを構成します。アプリケーションごとに 1 つの ID プロバイダーを構成できます。ID プロバイダーを構成すると、モバイル・アプリのユーザーは既存の Facebook または Google+ のアカウントを使用してログインできるようになります。あるいは、カスタム認証を作成してユーザーのログイン方法を定義できます。
   * [Facebook 資格情報を使用したユーザーの認証](facebook-auth-overview.html)
   * [Google 資格情報を使用したユーザーの認証](google-auth-overview.html)
   * [カスタム ID プロバイダーを使用したユーザーの認証](custom-auth.html)

## チュートリアルおよびサンプル
{: #samples}

* [android-helloauthentication sample ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication "外部リンク・アイコン"){: new_window}
* [ios-helloauthentication sample (Swift SDK) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "外部リンク・アイコン"){: new_window}

## SDK
{: #sdk}

* [Core SDK (Android) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core "外部リンク・アイコン"){: new_window}

* [ios-helloauthentication sample (Swift SDK) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "外部リンク・アイコン"){: new_window}

* [カスタム認証 - 簡単なサンプル![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "外部リンク・アイコン"){: new_window}

* [カスタム認証 - 高度なサンプル![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management "外部リンク・アイコン"){: new_window}


