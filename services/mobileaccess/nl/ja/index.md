---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"
---


# {{site.data.keyword.amashort}} 概説
       
{: #gettingstarted}


{{site.data.keyword.amafull}} サービスを使用して、セキュリティーをモバイル・アプリに追加します。{{site.data.keyword.Bluemix_notm}} で実行されている保護されたバックエンド・リソースにアクセスするためのクライアント許可を構成できます。ID プロバイダー (Google および Facebook) またはカスタム ID を使用して、ユーザーを認証し、保護されたバックエンド・リソースおよび Web アプリに対するアクセスを許可します。
{:shortdesc}

**注:** {{site.data.keyword.amashort}} サービスの以前の名称は Advanced Mobile Access でした。


{{site.data.keyword.amashort}} サービスを起動して稼働させるには、次のようにします。

1. {{site.data.keyword.Bluemix_notm}} ダッシュボードを使用して、モバイル・バックエンド・アプリケーションを作成するか、または、既存のものを構成します。
  - {{site.data.keyword.Bluemix_notm}} カタログから **MobileFirst Services Starter** を選択することができます。
  - また、サービスを既存のアプリケーションにバインドし、構成することができます。

   MobileFirst Services Starter を使用すると、カスタム・バックエンド・ロジックを実装するために、IBM {{site.data.keyword.Bluemix_notm}} で稼働する Node.js ランタイムのインスタンスを取得します。セキュリティー、データ、プッシュ、およびモニターの各機能を提供する一連のコア・モバイル・サービスは、その Node.js アプリにバインドされています。{{site.data.keyword.Bluemix_notm}} Node.js アプリが作成されたら、 開発環境をセットアップし、{{site.data.keyword.Bluemix_notm}} モバイル・サービスの SDK の使用を開始できます。SDK を使用すると、単純な API 呼び出しを使用して、クラウド・アプリにバインドされているサービスにアクセスできます。
  
2. サーバー・サイド・リソースを保護します。

   Node.js ランタイムまたは Liberty for Java&trade; ランタイムで稼働しているモバイル・バックエンド・リソースを、モバイル対応の OAuth セキュリティーによって保護します。詳しくは、[リソースの保護](protecting-resources.html)を参照してください。デフォルトのモバイル・バックエンド・アプリケーションについて詳しく知りたい場合は、[bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop) サンプル・アプリケーションを参照してください。

3. コア {{site.data.keyword.amashort}} 開発環境をセットアップします。
   
	####クライアント開発
   {: #client-development}
   
	以下のように、既存の Android アプリ、iOS アプリ、または Cordova アプリに {{site.data.keyword.amashort}} SDK を追加できます。
   * Android: ([Android SDK のセットアップ](getting-started-android.html)) ([Sample](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))
  
   * iOS (Swift SDK): ([iOS Swift SDK のセットアップ](getting-started-ios-swift-sdk.html))
      ([Sample](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))
  
   * iOS (Objective-C SDK): ([iOS Object-C SDK のセットアップ](getting-started-ios.html)) ([Sample](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))

   * Cordova: ([Cordova プラグインのセットアップ](getting-started-cordova.html)) ([Sample](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))
   
   **注:** Objective-C SDK は現在も完全にサポートされ、{{site.data.keyword.amashort}} 用の主要 SDK とされていますが、この SDK は今年後半には廃止され、新しい Swift SDK が後継になる予定です。アプリケーションを作成するときには、Swift SDK を使用することを強くお勧めします ([iOS Swift SDK のセットアップ](getting-started-ios-swift-sdk.html)を参照してください)。

	####Web 開発
   {: #web-development}

   {{site.data.keyword.amashort}} サービスは、特別な SDK を必要とせずに、Web アプリケーションを保護することができます。{{site.data.keyword.amashort}} サービスによって提供される保護に加えて、さまざまな ID プロバイダーを活用できます。{{site.data.keyword.amashort}} 統合によって、実装されているテクノロジーに関係なくどのような Web アプリケーションであっても、OAuth2 プロトコルを利用することが可能になります。さまざまな ID プロバイダーを使用して {{site.data.keyword.amashort}} サービスにアクセスするための Web アプリケーションのセットアップについて詳しくは、以下を参照してください。

    * [Web アプリケーション用の Facebook 認証の使用可能化](facebook-auth-web.html)
              
    * [Web アプリケーション用の Google 認証の使用可能化](google-auth-web.html)
              
    * [Web アプリケーション用のカスタム認証の使用可能化](custom-auth-web.html)
              
4. **オプション:** アプリケーションの ID プロバイダーを構成します。アプリケーションごとに 1 つの ID プロバイダーを構成できます。ID プロバイダーを構成すると、モバイル・アプリのユーザーは既存の Facebook または Google+ のアカウントを使用してログインできるようになります。あるいは、カスタム認証を作成してユーザーのログイン方法を定義できます。
   * [Facebook 資格情報を使用したユーザーの認証](facebook-auth-overview.html)
   * [Google 資格情報を使用したユーザーの認証](google-auth-overview.html)
   * [カスタム ID プロバイダーを使用したユーザーの認証](custom-auth.html)

5. アプリのモニタリングおよびロギングを構成します。

    詳しくは、[アプリのモニター](app-monitoring.html)を参照してください。

# 関連リンク
{: #rellinks}

## チュートリアルおよびサンプル
{: #samples}
* [android-helloauthentication サンプル](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication){: new_window}
* [ios-helloauthentication サンプル (Swift SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication){: new_window}
* [ios-helloauthentication サンプル (Objective-C SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication){: new_window}

## SDK
{: #sdk}
* [Core SDK (Android)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [Core SDK (Cordova plug-in)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
* [Core SDK (iOS - Swift) ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [Core SDK (iOS - Objective-C - 非推奨) ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [カスタム認証 - 簡単なサンプル](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [カスタム認証 - 高度なサンプル](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## API リファレンス
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS (Objective-C SDK) - 非推奨](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## 関連リンク
{: #general}
* [概要](overview.html){: new_window}
