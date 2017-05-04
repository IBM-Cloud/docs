---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# {{site.data.keyword.amashort}} は {{site.data.keyword.appid_short_notm}} に置き換えられます
{: #gettingstarted}


**{{site.data.keyword.amafull}} サービスは [{{site.data.keyword.appid_full}} サービス](/docs/services/appid/index.html)に置き換えられます。** 詳細については、<a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="_blank">{{site.data.keyword.appid_short_notm}} の発表 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。
{:shortdesc}


{{site.data.keyword.amashort}} がセキュリティー (ID プロバイダー (Google および Facebook) から保護されたバックエンド・リソースにアクセスするためのクライアント許可や、ユーザーを認証して保護されたバックエンド・リソースと Web アプリへのアクセスを許可するカスタム ID) をモバイル・アプリに提供しました。

**注:** {{site.data.keyword.amashort}} サービスの以前の名称は Advanced Mobile Access でした。


## {{site.data.keyword.appid_short_notm}} へのマイグレーション

{{site.data.keyword.appid_short_notm}} では、ID プロバイダー (Google および Facebook) を使用してモバイル・アプリケーションを保護することができます。また、クライアント許可を使用してバックエンド・リソースを保護することもできます。

1. {{site.data.keyword.Bluemix_notm}} カタログからサービス・インスタンスをプロビジョンします。インスタンスを構成し、**「作成」**をクリックします。
2. サービス・インスタンス・ダッシュボードで、ステップバイステップ・サンプルを使用して {{site.data.keyword.appid_short_notm}} を開始します。
3. {{site.data.keyword.appid_short_notm}} SDK をダウンロードし、[Android SDK](/docs/services/appid/getting-started-android.html#android-sdk) または [iOS Swift SDK](/docs/services/appid/getting-started-ios-swift-sdk.html#getting-started-ios) のいずれかを使用してアプリケーションをセットアップします。
4. [ID プロバイダー](/docs/services/appid/identity-providers.html)を構成します。
5. [ログイン・ウィジェット](/docs/services/appid/login-widget.html)をカスタマイズします。
6. アプリが正しく機能しているか確認します。
    * サービス・ダッシュボードをチェックして、アプリが実行中であることを確認します。
    * サービス・ダッシュボードで**「最近のアクティビティー」**を表示して、現在実行中の認証をモニターします。
7. {{site.data.keyword.amashort}} のインスタンスをプロビジョン解除し、削除します。



<!-- Commenting out all getting started content because new users should start with App ID.

Add security to your mobile app with the {{site.data.keyword.amafull}} service. You can configure client authorization for accessing protected back-end resources running on {{site.data.keyword.Bluemix}}. Use identity providers (Google and Facebook), or custom identities to authenticate users and grant access to protected back-end resources and Web apps.
{:shortdesc}

**Note:** The {{site.data.keyword.amashort}} service was previously known as Advanced Mobile Access.


To get up and running with the {{site.data.keyword.amashort}} service:

1. Use one of the following options to create a bound or unbound service:
 * Create a {{site.data.keyword.Bluemix_notm}} application using the **MobileFirst Services Starter** boilerplate from the catalog. This creates a {{site.data.keyword.amashort}} service bound to a {{site.data.keyword.Bluemix_notm}} back-end application.
 * Create a {{site.data.keyword.amashort}} service using the  {{site.data.keyword.amashort}} console.  You can  bind the service to an existing back-end application and configure it in the {{site.data.keyword.amashort}} console.

   When you use the MobileFirst Services Starter, you get an instance of a Node.js runtime that runs on IBM {{site.data.keyword.Bluemix_notm}} to implement your custom back-end logic. A set of core mobile services that provide security, data, push, and monitoring functions are bound to that Node.js app. After the {{site.data.keyword.Bluemix_notm}} Node.js app is created, you can set up your development environment and start to use the {{site.data.keyword.Bluemix_notm}} Mobile Services SDKs. You can use the SDKs to access the services that are bound to your cloud app with simple API calls.

	For more information on how to create and work with projects, applications, and services see [IBM Bluemix Mobile dashboard](https://console.{DomainName}/docs/mobile/index.html).

2. Secure server-side resources.

   Protect your mobile back-end resources that are running on Node.js or Liberty for Java&trade; runtimes with mobile-enabled OAuth security. For more information, see [Protecting resources](protecting-resources.html).
   To learn more about the default mobile back-end application, see the [bms-hellotodo-strongloop ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop){: new_window}  sample application.

3. Set up your core {{site.data.keyword.amashort}} development environment.

  ####Client development
  {: #client-development}

	You can add the {{site.data.keyword.amashort}} SDK to your existing Android, iOS, or Cordova app, as follows:
   * Android: ([Setting up the Android SDK](getting-started-android.html)) [Sample ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication){: new_window}
    * iOS (Swift SDK): ([Setting up the iOS Swift SDK](getting-started-ios-swift-sdk.html)) [Sample ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication){: new_window}    
   * Cordova: ([Setting up the Cordova plug-in](getting-started-cordova.html)) [Sample ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication){: new_window}


 ####Web development
 {: #web-development}

   The {{site.data.keyword.amashort}} service can protect your Web application, requiring no special SDK. You can leverage different identity providers, in addition to protection provided by the {{site.data.keyword.amashort}} service. The {{site.data.keyword.amashort}} integration enables any web application, regardless of the technology it implements, to take advantage of the OAuth2 protocol. For information on setting up your {{site.data.keyword.amashort}} Web app to access the {{site.data.keyword.amashort}} service using different identity providers, see:

   * [Enabling Facebook authentication for Web applications](facebook-auth-web.html)
   * [Enabling Google authentication for Web applications](google-auth-web.html)
   * [Enabling custom authentication for Web applications](custom-auth-web.html)

**Optional:** Configure an identity provider for your application. You can configure one identity provider per application. Configuring an identity provider enables the users of your mobile app to log in with their existing Facebook or Google+ account. Or, you can define how users log in by creating a custom authentication.
   * [Authenticating users with Facebook credentials](facebook-auth-overview.html)
   * [Authenticating users with Google credentials](google-auth-overview.html)
   * [Authenticating users with a custom identity provider](custom-auth.html) --->
