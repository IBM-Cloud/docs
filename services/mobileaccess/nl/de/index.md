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


# {{site.data.keyword.amashort}} wird durch {{site.data.keyword.appid_short_notm}} ersetzt
{: #gettingstarted}


**Der {{site.data.keyword.amafull}}-Service wird durch den [{{site.data.keyword.appid_full}}-Service ersetzt](/docs/services/appid/index.html).** Weitere Details finden Sie in der Ankündigung zu <a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="_blank">{{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.
{:shortdesc}


{{site.data.keyword.amashort}} versorgte Ihre mobile App mit Sicherheit: Clientberechtigung für den Zugriff auf geschützte Back-End--Ressourcen aus Identitätsprovidern (Google und Facebook) oder angepasste Identitäten, um Benutzer zu authentifizieren und Zugriff auf geschützte Back-End-Ressourcen und Web-Apps zu gewähren.

**Anmerkung:** Der {{site.data.keyword.amashort}}-Service wurde früher als Advanced Mobile Access bezeichnet.


## Migration auf {{site.data.keyword.appid_short_notm}}

Mit {{site.data.keyword.appid_short_notm}} können Sie mobile Anwendungen schützen, indem Sie Identitätsprovider (Google und Facebook) einsetzen. Es ist ebenfalls möglich, Back-End-Ressourcen mit Clientberechtigung zu schützen. 

1. Stellen Sie die Serviceinstanz aus dem {{site.data.keyword.Bluemix_notm}}-Katalog bereit. Konfigurieren Sie die Instanz und klicken Sie auf **Erstellen**. 
2. Verwenden Sie die Beispiele im Dashboard der Serviceinstanz, in denen die Einführung in {{site.data.keyword.appid_short_notm}} Schritt für Schritt beschrieben wird. 
3. Laden Sie die {{site.data.keyword.appid_short_notm}}-SDKs herunter und richten Sie die Anwendung ein. Verwenden Sie hierzu entweder das [Android-SDK](/docs/services/appid/getting-started-android.html#android-sdk) oder das [iOS-Swift-SDK](/docs/services/appid/getting-started-ios-swift-sdk.html#getting-started-ios).
4. Konfigurieren Sie die [Identitätsprovider](/docs/services/appid/identity-providers.html).
5. Passen Sie das [Anmelde-Widget](/docs/services/appid/login-widget.html) an.
6. Stellen Sie sicher, dass die App korrekt funktioniert.
    * Überprüfen Sie das Service-Dashboard, um sicherzustellen, dass die App aktiv ist.
    * Rufen Sie im Service-Dashboard **Kürzliche Aktivität** auf, um laufende Authentifizierungen zu überwachen. 
7. Heben Sie die Bereitstellung der Instanzen von {{site.data.keyword.amashort}} auf und entfernen Sie sie. 



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
