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


# {{site.data.keyword.amashort}} est remplacé par {{site.data.keyword.appid_short_notm}}
{: #gettingstarted}


**Le service {{site.data.keyword.amafull}} est remplacé par le service [{{site.data.keyword.appid_full}}](/docs/services/appid/index.html).** Pour plus de détails, voir l'<a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="_blank">annonce {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.
{:shortdesc}


{{site.data.keyword.amashort}} assurait la sécurité de votre application mobile : une autorisation client était requise pour accéder aux ressources de back-end depuis les fournisseurs d'identité (Google et Facebook) ou des identités personnalisées pour authentifier les utilisateurs et accorder un accès aux ressources de back-end protégées et aux applications Web.

**Remarque :** Le service {{site.data.keyword.amashort}} était dénommé auparavant Advanced Mobile Access.


## Migration vers {{site.data.keyword.appid_short_notm}}

Avec {{site.data.keyword.appid_short_notm}}, vous pouvez sécuriser vos applications mobiles en utilisant des fournisseurs d'identité (Google et Facebook). Vous pouvez également protéger vos ressources back end à l'aide de l'autorisation client.

1. Mettez à disposition votre instance depuis le catalogue {{site.data.keyword.Bluemix_notm}}. Configurez votre instance et cliquez sur **Créer**.
2. Dans le tableau de bord de votre instance de service, utilisez les exemples détaillés étape par étape pour vous initier à {{site.data.keyword.appid_short_notm}}.
3. Téléchargez les SDK {{site.data.keyword.appid_short_notm}} et configurez votre application en utilisant soit [le SDK Android](/docs/services/appid/getting-started-android.html#android-sdk), soit [le SDK Swift iOS](/docs/services/appid/getting-started-ios-swift-sdk.html#getting-started-ios).
4. Configurez vos [fournisseurs d'identité](/docs/services/appid/identity-providers.html).
5. Personnalisez votre [widget de connexion](/docs/services/appid/login-widget.html).
6. Vérifiez que votre application fonctionne correctement.
    * Vérifiez votre tableau de bord de service pour vous assurer que votre application est en cours d'exécution.
    * Dans votre tableau de bord de service, affichez l'**activité récente** pour surveiller toute authentification en cours.
7. Annulez les accès et retirez vos instances de {{site.data.keyword.amashort}}.



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
