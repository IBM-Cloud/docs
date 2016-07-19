---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Getting started with {{site.data.keyword.amashort}}
{: #gettingstarted}
*Last updated: July 18 2016*
{: .last-updated}

Add security  functionality to your mobile app with the {{site.data.keyword.amafull}} service. You can configure client authentication and identity providers so that users can log in to the app with their existing Google or Facebook accounts.
{:shortdesc}

**Note:** The {{site.data.keyword.amashort}} service was previously known as Advanced Mobile Access.


To get up and running with the {{site.data.keyword.amashort}} service:

1.  Use the {{site.data.keyword.Bluemix_notm}}  dashboard to create a mobile back-end application, or configure an existing one.
  - You can select the **MobileFirst Services Starter** boilerplate from the {{site.data.keyword.Bluemix_notm}} catalog.
  - Or, you can bind the service to an existing application and configure it.

   When you use the MobileFirst Services Starter, you get an instance of a Node.js runtime that runs on IBM {{site.data.keyword.Bluemix_notm}} to implement your custom back-end logic. A set of core mobile services that provide security, data, push, and monitoring functions are bound to that Node.js app. After the {{site.data.keyword.Bluemix_notm}} Node.js app is created, you can set up your development environment and start to use the {{site.data.keyword.Bluemix_notm}} Mobile Services SDKs. You can use the SDKs to access the services that are bound to your cloud app with simple API calls.
  
1. Secure server-side resources.

   Protect your mobile back-end resources that are running on Node.js or Liberty for Java&trade; runtimes with mobile-enabled OAuth security. For more information, see [Protecting resources](protecting-resources.html).
   To learn more about the default mobile back-end application, see the [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop) sample application.

1. Set up your core {{site.data.keyword.amashort}} client-side or web development environment.

  **Client development:**
  
   You can add the {{site.data.keyword.amashort}} SDK to your existing Android, Cordova, or iOS app. 
   * **Android**: ([Setting up the Android SDK](getting-started-android.html)) ([Sample](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))
  
   * **Cordova**: ([Setting up the Cordova plug-in](getting-started-cordova.html)) ([Sample](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))
  
   * **iOS (Swift SDK)**: ([Setting up the iOS Swift SDK](getting-started-ios-swift-sdk.html))
      ([Sample](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))
  
   * **iOS (Objective-C SDK)**: ([Setting up the iOS Object-C SDK](getting-started-ios.html)) ([Sample](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))
   
   **Note:**  While the Objective-C SDK remains fully supported, and still considered the primary SDK for {{site.data.keyword.amashort}}, there are plans to discontinue this SDK later this year in favor of the new Swift SDK. If you are creating an application, we highly recommend that you use the Swift SDK (see [Setting up the iOS Swift SDK](getting-started-ios-swift-sdk.html)).
   
   **Web development:**

   **In addition**, the {{site.data.keyword.amashort}} service can protect your web application, requiring no special SDK. You can leverage different identity providers, in addition to protection provided by the {{site.data.keyword.amashort}} service. It enables any web application, regardless of the technology it implements, to take advantage of the OAuth2 protocol. For information on setting up your web app to access the {{site.data.keyword.amashort}} service using different identity providers, see:

    * [Enabling Facebook authentication for web applications](facebook-auth-web.html)
              
    * [Enabling Google authentication for web applications](google-auth-web.html)
              
    * [Enabling custom authentication for web applications](custom-auth-web.html)
              
1. **Optional:** Configure an identity provider for your application. You can configure one identity provider per application. Configuring an identity provider enables the users of your mobile app to log in with their existing Facebook or Google+ account. Or, you can define how users log in by creating a custom authentication.
   * [Authenticating users with Facebook credentials](facebook-auth-overview.html)
   * [Authenticating users with Google credentials](google-auth-overview.html)
   * [Authenticating users with a custom identity provider](custom-auth.html)

1. Configure your app monitoring and logging.

    For more information, see [Monitoring apps](app-monitoring.html).

# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}
* [android-helloauthentication sample](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication){: new_window}
* [ios-helloauthentication sample (Swift SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication){: new_window}
* [ios-helloauthentication sample (Objective-C SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication){: new_window}

## SDK
{: #sdk}
* [Core SDK (Android)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [Core SDK (Cordova plug-in)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
* [Core SDK (iOS - Swift) ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [Core SDK (iOS - Objective-C - Deprecated) ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [Custom authentication - simple sample](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [Custom authentication - advanced sample](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## API Reference
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS (Objective-C SDK) - Deprecated](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## Related Links
{: #general}
* [Overview](overview.html){: new_window}
