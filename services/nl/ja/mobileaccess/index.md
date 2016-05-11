---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.amashort}} 入門
       
{: #gettingstarted}
*最終更新日: 2016 年 3 月 21 日*

{{site.data.keyword.amafull}} サービスを使用して、セキュリティーおよびモニタリング機能をモバイル・アプリに追加します。ユーザーが既存の Google アカウントまたは Facebook アカウントを使用してアプリにログインできるように、クライアント認証プロバイダーおよび ID プロバイダーを構成することが可能です。また、アプリケーションにモニター機能を追加することにより、クライアントのロギングおよび使用統計の両方が可能になります。
{:shortdesc}

**注:** {{site.data.keyword.amashort}} サービスの以前の名称は Advanced Mobile Access でした。


{{site.data.keyword.amashort}} サービスを起動して稼働させるには、以下の手順に従います。

1. クライアント・サイドの開発環境をセットアップします。既存の Android アプリ、Cordova アプリ、または iOS アプリに {{site.data.keyword.amashort}} SDK を追加できます。HelloAuthentication サンプル・アプリケーションをダウンロードすることもできます。
   * **Android**: ([SDK](getting-started-android.html)) ([Sample](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))
   * **Cordova**: ([SDK](getting-started-cordova.html)) ([Sample](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))
   * **iOS (Swift-C SDK)**: ([SDK](getting-started-ios-swift-sdk.html)) ([Sample](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))
   * **iOS (Objective-C SDK)**: ([SDK](getting-started-ios.html)) ([Sample](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))

1. サーバー・サイド・リソースを保護します。Node.js ランタイムまたは Liberty for Java&trade; ランタイムで稼働しているモバイル・バックエンド・リソースを、モバイル対応の OAuth セキュリティーによって保護します。詳しくは、[リソースの保護](protecting-resources.html)を参照してください。

1. オプション: アプリケーションの ID プロバイダーを構成します。アプリケーションごとに 1 つの ID プロバイダーを構成できます。ID プロバイダーを構成すると、モバイル・アプリのユーザーは既存の Facebook または Google+ のアカウントを使用してログインできるようになります。あるいは、カスタム認証を作成してユーザーのログイン方法を定義できます。
   * [Facebook](facebook-auth-overview.html)
   * [Google](google-auth-overview.html)
   * [カスタム](custom-auth.html)

1. アプリのモニタリングおよびロギングを構成します。詳細情報については、[アプリのモニター](app-monitoring.html)を参照してください。

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
* [Core SDK (iOS - Objective-C) ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [カスタム認証 - 簡単なサンプル](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [カスタム認証 - 高度なサンプル](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## API リファレンス
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS (Objective-C SDK)](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## 関連リンク
{: #general}
* [概要](overview.html){: new_window}
