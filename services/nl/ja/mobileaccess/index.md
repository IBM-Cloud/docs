---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# {{site.data.keyword.amashort}} 入門
       
{: #gettingstarted}
*最終更新日: 2016 年 6 月 15 日*
{: .last-updated}

{{site.data.keyword.amafull}} サービスを使用して、セキュリティー機能をモバイル・アプリに追加します。ユーザーが既存の Google アカウントまたは Facebook アカウントを使用してアプリにログインできるように、クライアント認証プロバイダーおよび ID プロバイダーを構成することが可能です。
{:shortdesc}

**注:** {{site.data.keyword.amashort}} サービスの以前の名称は Advanced Mobile Access でした。


{{site.data.keyword.amashort}} サービスを起動して稼働させるには、以下の手順に従います。

1.  {{site.data.keyword.Bluemix_notm}} ダッシュボードを使用して、モバイル・バックエンド・アプリケーションを作成するか、または、既存のものを構成します。
  - Bluemix カタログから MobileFirst Services Starter を選択することができます。
  - あるいは、サービスを既存のアプリケーションにバインドし、構成することができます。

   MobileFirst Services Starter を使用すると、カスタム・バックエンド・ロジックを実装するために、IBM {{site.data.keyword.Bluemix_notm}} で稼働する Node.js ランタイムのインスタンスを取得します。セキュリティー、データ、プッシュ、およびモニターの各機能を提供する一連のコア・モバイル・サービスは、その Node.js アプリにバインドされています。{{site.data.keyword.Bluemix_notm}} Node.js アプリが作成されたら、 開発環境をセットアップし、{{site.data.keyword.Bluemix_notm}} モバイル・サービスの SDK の使用を開始できます。SDK を使用すると、単純な API 呼び出しを使用して、クラウド・アプリにバインドされているサービスにアクセスできます。
   
  
1. サーバー・サイド・リソースを保護します。

   Node.js ランタイムまたは Liberty for Java&trade; ランタイムで稼働しているモバイル・バックエンド・リソースを、モバイル対応の OAuth セキュリティーによって保護します。詳しくは、[リソースの保護](protecting-resources.html)を参照してください。デフォルトのモバイル・バックエンド・アプリケーションについて詳しく知りたい場合は、[bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop) を参照してください。

1. コア {{site.data.keyword.amashort}} クライアント・サイド開発環境をセットアップします。

   既存の Android アプリ、Cordova アプリ、または iOS アプリに {{site.data.keyword.amashort}} SDK を追加できます。HelloAuthentication サンプル・アプリケーションをダウンロードすることもできます。
   * **Android**: ([Android SDK のセットアップ](getting-started-android.html)) ([Sample](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))
  
   * **Cordova**: ([Cordova プラグインのセットアップ](getting-started-cordova.html)) ([Sample](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))
  
   * **iOS (Swift SDK)**: ([iOS Swift SDK のセットアップ](getting-started-ios-swift-sdk.html))
      ([Sample](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))
  
   * **iOS (Objective-C SDK)**: ([iOS Object-C SDK のセットアップ](getting-started-ios.html)) ([Sample](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))
   
   **注:** Objective-C SDK は現在も現在も完全にサポートされ、Bluemix モバイル・サービス用の主要 SDK とされていますが、この SDK は今年後半には廃止され、新しい Swift SDK が後継になる予定です。アプリケーションを作成するときには、Swift SDK を使用することを強くお勧めします ([iOS Swift SDK のセットアップ](getting-started-ios-swift-sdk.html)を参照してください)。

1. **オプション:** アプリケーションの ID プロバイダーを構成します。アプリケーションごとに 1 つの ID プロバイダーを構成できます。ID プロバイダーを構成すると、モバイル・アプリのユーザーは既存の Facebook または Google+ のアカウントを使用してログインできるようになります。あるいは、カスタム認証を作成してユーザーのログイン方法を定義できます。
   * [Facebook 資格情報を使用したユーザーの認証](facebook-auth-overview.html)
   * [Google 資格情報を使用したユーザーの認証](google-auth-overview.html)
   * [カスタム ID プロバイダーを使用したユーザーの認証](custom-auth.html)

1. アプリのモニタリングおよびロギングを構成します。

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
