---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-05-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# {{site.data.keyword.amashort}} is replaced with {{site.data.keyword.appid_short_notm}}
{: #gettingstarted}


The {{site.data.keyword.amafull}} service is replaced with the [{{site.data.keyword.appid_full}} service](/docs/services/appid/index.html). For more information, see the <a href="https://www.ibm.com/blogs/bluemix/2017/03/introducing-ibm-bluemix-app-id-authentication-profiles-service-app-developers/" target="_blank">{{site.data.keyword.appid_short_notm}} announcement <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
{:shortdesc}


{{site.data.keyword.amashort}} provided security to your mobile app: client authorization for accessing protected back-end resources from identity providers (Google and Facebook) or custom identities to authenticate users and grant access to protected back-end resources and web apps.

With {{site.data.keyword.appid_short_notm}}, you can authenticate your application users and store information in a profile linked to their identity. You can use that information to customize their user experience.


## Migrating to {{site.data.keyword.appid_short_notm}}

**Note**:  With {{site.data.keyword.appid_short_notm}}, you can configure Facebook, Google, or both as identity providers. If you are using custom authentication in the MCA service, you are unable to migrate currently. Contact our support team for more information on your migration.

1. Provision an <a href="https://console.ng.bluemix.net/catalog/?category=services&taxonomyNavigation=services&env_id=ibm:yp:us-south&search=app%20id" target="_blank">instance of {{site.data.keyword.appid_short_notm}} <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> from the {{site.data.keyword.Bluemix_notm}} catalog. Configure your instance and click **Create**.
2. In your service instance dashboard, open the **Identity Providers** tab and click **Edit** for either Facebook or Google. A dialog box opens.
3. Input the information for your <a href="https://console.developers.google.com/apis/library" target="_blank">Google <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> or <a href="https://developers.facebook.com/" target="_blank">Facebook <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> application and click **Save**.
4. If you use {{site.data.keyword.amashort}} with a web app, add the redirect URL from your {{site.data.keyword.amashort}} dashboard to the **Web Redirect URL** on the **Identity Providers** tab.
5. Replace the {{site.data.keyword.amashort}} SDKs with the {{site.data.keyword.appid_short_notm}} SDKs by using either the [Android SDK](/docs/services/appid/getting-started-android.html#android-sdk) or the [iOS Swift SDK](/docs/services/appid/getting-started-ios-swift-sdk.html#getting-started-ios).
6. **Optional**: Customize your [login widget](/docs/services/appid/login-widget.html). When you configure both Facebook and Google, your users see a customizable login page.
7. Verify that your app is working correctly.
    * Check your service dashboard to ensure that your app is running.
    * In your service dashboard, view **recent activity** to monitor any ongoing authentication.
8. Unbind and delete your instances of {{site.data.keyword.amashort}}.



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
