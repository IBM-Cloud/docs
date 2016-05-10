---

Copyright : 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Initiation à {{site.data.keyword.amashort}}
{: #gettingstarted}
*Dernière mise à jour : 21 mars 2016*

Ajoutez une fonction de sécurité et de surveillance à votre application mobile avec le service
{{site.data.keyword.amafull}}. Vous pouvez configurer une authentification client et des fournisseurs d'identité de sorte que les utilisateurs
puissent se connecter à l'application avec leur comptes Google ou Facebook existants. Vous pouvez aussi ajouter à votre application une fonction de
surveillance qui active la journalisation client et les statistiques d'utilisation.
{:shortdesc}

**Remarque :** Le service {{site.data.keyword.amashort}} était dénommé auparavant Advanced Mobile
Access.


Pour démarrer et et commencer à travailler avec le service {{site.data.keyword.amashort}}, procédez comme suit :

1. Configurez votre environnement de développement côté client.
Vous pouvez ajouter le SDK {{site.data.keyword.amashort}} à votre application Android, Cordova ou iOS existante. Vous pouvez également télécharger l'exemple
d'application HelloAuthentication.
   * **Android** : ([SDK](getting-started-android.html))
([Exemple](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))
   * **Cordova** : ([SDK](getting-started-cordova.html))
([Exemple](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))
   * **iOS (SDK Swift-C)** : ([SDK](getting-started-ios-swift-sdk.html))
([Exemple](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))
   * **iOS (SDK Objective-C)** : ([SDK](getting-started-ios.html))
([Exemple](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))

1. Sécurisez les ressources côté serveur. Protégez vos ressources de back end mobile qui s'exécutent en contextes d'exécution
Node.js ou Liberty for Java&trade; avec la sécurité OAuth pour les périphériques mobiles. Pour plus d'informations, voir [Protection des ressources](protecting-resources.html).

1. Facultatif : Configurez un fournisseur d'identité pour votre application. Vous ne pouvez configurer qu'un fournisseur d'identité par
application. La configuration d'un fournisseur d'identité permet aux utilisateurs de votre application mobile de se connecter avec leur compte Facebook
ou Google+ existant. Ou bien, vous pouvez définir le mode de connexion des utilisateurs en créant une authentification personnalisée.
   * [Facebook](facebook-auth-overview.html)
   * [Google](google-auth-overview.html)
   * [Authentification personnalisée](custom-auth.html)

1. Configurez la surveillance et la journalisation des applications.  Pour plus d'informations, voir [Surveillance des applis](app-monitoring.html).

# Liens connexes
{: #rellinks}

## Tutoriels et exemples
{: #samples}
* [Exemple android-helloauthentication](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication){: new_window}
* [Exemple ios-helloauthentication (SDK Swift)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication){: new_window}
* [Exemple ios-helloauthentication (SDK Objective-C)](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication){: new_window}

## Logiciel SDK
{: #sdk}
* [Core SDK (Android)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [Core SDK (plug-in Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
* [Core SDK (iOS - Swift) ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [Core SDK (iOS - Objective-C) ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [Authentification personnalisée -
exemple simple](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [Authentification personnalisée -
exemple avancé](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## Référence d'API
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS (SDK Objective-C)](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## Liens connexes
{: #general}
* [Présentation](overview.html){: new_window}
