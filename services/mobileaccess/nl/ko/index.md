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


# {{site.data.keyword.amashort}}가 {{site.data.keyword.appid_short_notm}}로 대체됨
{: #gettingstarted}


**{{site.data.keyword.amafull}} 서비스가 [{{site.data.keyword.appid_full}} 서비스](/docs/services/appid/index.html)로 대체되었습니다.** 세부사항은 <a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="_blank">{{site.data.keyword.appid_short_notm}} 공지사항 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>을 참조하십시오.
{:shortdesc}


{{site.data.keyword.amashort}}가 모바일 앱에 보안을 제공했습니다(ID 제공자(Google 및 Facebook)로부터 보호된 백엔드 리소스에 액세스하기 위한 클라이언트 권한 및 사용자를 인증하고 보호된 백엔드 리소스와 웹 앱에 대한 액세스를 부여하기 위한 사용자 정의 ID).

**참고:** {{site.data.keyword.amashort}} 서비스를 이전에는 Advanced Mobile Access라고 했습니다.


## {{site.data.keyword.appid_short_notm}}로 마이그레이션

{{site.data.keyword.appid_short_notm}}에서 ID 제공자(Google 및 Facebook)를 사용하여 모바일 애플리케이션을 보호할 수 있습니다. 클라이언트 권한 부여로 백엔드 리소스를 보호할 수도 있습니다.

1. {{site.data.keyword.Bluemix_notm}} 카탈로그에서 서비스 인스턴스를 프로비저닝하십시오. 인스턴스를 구성하고 **작성**을 클릭하십시오. 
2. 서비스 인스턴스 대시보드에서 단계별 샘플을 사용하여 {{site.data.keyword.appid_short_notm}}를 시작하십시오. 
3. {{site.data.keyword.appid_short_notm}} SDK를 다운로드하고 [Android SDK](/docs/services/appid/getting-started-android.html#android-sdk) 또는 [iOS Swift SDK](/docs/services/appid/getting-started-ios-swift-sdk.html#getting-started-ios)를 사용하여 애플리케이션을 설정하십시오. 
4. [ID 제공자](/docs/services/appid/identity-providers.html)를 구성하십시오. 
5. [로그인 위젯](/docs/services/appid/login-widget.html)을 사용자 정의하십시오. 
6. 앱이 올바르게 작동하는지 확인하십시오. 
    * 서비스 대시보드를 확인하여 앱이 실행 중인지 확인하십시오. 
    * 서비스 대시보드에서 **최근 활동**을 보고 진행 중인 인증을 모니터하십시오. 
7. {{site.data.keyword.amashort}}의 인스턴스를 디프로비저닝하고 제거하십시오. 



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
