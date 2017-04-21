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


# O {{site.data.keyword.amashort}} foi substituído pelo {{site.data.keyword.appid_short_notm}}
{: #gettingstarted}


**O serviço {{site.data.keyword.amafull}} foi substituído pelo [serviço {{site.data.keyword.appid_full}}](/docs/services/appid/index.html).** Para obter mais detalhes, consulte  <a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="_blank"> Anúncio do {{site.data.keyword.appid_short_notm}}
<img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.
{:shortdesc}


O {{site.data.keyword.amashort}} fornecia segurança para seu aplicativo móvel: autorização do cliente para acessar recursos de backend protegidos por meio de provedores de identidade (Google e Facebook) ou identidades customizadas para autenticar usuários e conceder acesso a aplicativos da web e recursos de backend protegidos.

**Nota:** o serviço {{site.data.keyword.amashort}} era conhecido anteriormente como Advanced Mobile Access. 


## Migrando para {{site.data.keyword.appid_short_notm}}

Com o {{site.data.keyword.appid_short_notm}}, é possível assegurar seus aplicativos móveis usando provedores de identidade (Google e Facebook). Também é possível proteger recursos de backend com autorização do cliente.

1. Provisione sua instância de serviço no catálogo do {{site.data.keyword.Bluemix_notm}}. Configure sua instância e clique em **Criar**.
2. No painel da sua instância de serviço, use as amostras passo a passo para começar a usar o {{site.data.keyword.appid_short_notm}}.
3. Faça o download dos SDKs do {{site.data.keyword.appid_short_notm}} e configure seu aplicativo usando [o SDK de Android](/docs/services/appid/getting-started-android.html#android-sdk) ou [o SDK Swift de iOS](/docs/services/appid/getting-started-ios-swift-sdk.html#getting-started-ios).
4. Configure seus [provedores de identidade](/docs/services/appid/identity-providers.html).
5. Customize seu [widget de login](/docs/services/appid/login-widget.html).
6. Verifique se seu app está funcionando corretamente.
    * Verifique o seu painel de serviços para assegurar que o app esteja executando.
    * Em seu painel de serviços, visualize **atividade recente** para monitorar qualquer autenticação em andamento.
7. Desproveja e remova suas instâncias do {{site.data.keyword.amashort}}.



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
