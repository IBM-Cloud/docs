---

copyright:
  years: 2015, 2016
  
---

{:shortdesc: .shortdesc}

# {{site.data.keyword.amashort}} 入門
       
{: #getting-started}

{{site.data.keyword.amafull}} サービスは、
モバイル・アプリケーションにセキュリティーおよびモニター機能を付与します。クライアントの認証プロバイダーおよび ID プロバイダーを構成できるようになります。また、アプリケーションにモニター機能を追加することにより、クライアントのロギングおよび使用統計の両方が可能になります。

注: Mobile Client Access サービスの以前の名称は Advanced Mobile Access でした。
{: shortdesc}

1. Bluemix にモバイル・バックエンドをセットアップし、モバイル・アプリに SDK を構成します。詳しくは、[始めに (Getting started) ](getting-started.html)を参照してください。
1. サーバー・サイド・リソースを保護します。Node.js ランタイムまたは Liberty for Java&trade; ランタイムで稼働しているモバイル・バックエンド・リソースを、モバイル対応の OAuth セキュリティーによって保護します。詳しくは、[リソースの保護](protecting-resources.html)を参照してください。
1. オプション: アプリケーションの ID プロバイダーを構成します。アプリケーションごとに 1 つの ID プロバイダーを構成できます。ID プロバイダーを構成すると、モバイル・アプリのユーザーは既存の Facebook または Google+ のアカウントを使用してログインできるようになります。あるいは、カスタム認証を作成してユーザーのログイン方法を定義できます。
   * [Facebook](facebook-auth-overview.html)
   * [Google](google-auth-overview.html)
   * [カスタム](custom-auth.html)
1. アプリのモニタリングおよびロギングを構成します。詳細情報については、[アプリのモニター](app-monitoring.html)を参照してください。


># 関連リンク{:class="linklist"}
>## チュートリアルおよびサンプル{:id="samples"}
>* [android-helloauthentication](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication)
>* [ios-helloauthentication](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication)
>
># 関連リンク{:class="linklist"}
>## API 参照{:id="api"}
>* [Core API リファレンス (Android)](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
>* [Core API リファレンス (iOS)](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)
>
># 関連リンク{:class="linklist"}
>## SDK{:id="sdk"}
>* [Core SDK (iOS) ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)  
>* [bms-clientsdk-android-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)
>* [bms-clientsdk-cordova-plugin-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)
>
>{:elementKind="article" id="rellinks"}
