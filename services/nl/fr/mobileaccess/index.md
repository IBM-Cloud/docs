---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Initiation à {{site.data.keyword.amashort}}
{: #gettingstarted}
*Dernière mise à jour : 15 juin 2016*
{: .last-updated}

Ajoutez une fonctionnalité de sécurité à votre application mobile avec le service {{site.data.keyword.amafull}}. Vous pouvez configurer une authentification client et des fournisseurs d'identité de sorte que les utilisateurs
puissent se connecter à l'application avec leur comptes Google ou Facebook existants.
{:shortdesc}

**Remarque :** Le service {{site.data.keyword.amashort}} était dénommé auparavant Advanced Mobile
Access.


Pour démarrer et et commencer à travailler avec le service {{site.data.keyword.amashort}}, procédez comme suit :

1.  Utilisez le tableau de bord {{site.data.keyword.Bluemix_notm}} pour créer une application de back end mobile ou configurez une application existante.
  - Vous pouvez sélectionner MobileFirst Services Starter dans le catalogue Bluemix.
  - Ou, vous pouvez lier le service à une application existante et la configurer.

   Quand vous utilisez MobileFirst Services Starter, vous obtenez une instance du contexte d'exécution Node.js qui s'exécute sur IBM {{site.data.keyword.Bluemix_notm}} pour implémenter votre logique de back end personnalisée. Un ensemble de services mobiles de base qui fournissent des fonctions de sécurité, de données, d'envoi par commande push et de surveillance est lié à cette application
Node.js. Une fois l'application {{site.data.keyword.Bluemix_notm}} Node.js créée, vous pouvez configurer votre environnement de développement
et commencer à utiliser les logiciels SDK de {{site.data.keyword.Bluemix_notm}} Mobile Services. Vous pouvez utiliser les logiciels SDK pour accéder aux services qui sont liés à votre application en cloud à l'aide de simples appels d'API.
   
  
1. Sécurisez les ressources côté serveur.

   Protégez vos ressources de back end mobile qui s'exécutent en contextes d'exécution Node.js,ou Liberty for Java&trade;, avec la sécurité OAuth pour les périphériques mobiles. Pour plus d'informations, voir [Protection des ressources](protecting-resources.html).
   Pour en savoir plus sur l'application de back end mobile par défaut, voir [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop).

1. Configurez votre environnement de développement côté client {{site.data.keyword.amashort}} principal.

   Vous pouvez ajouter le SDK {{site.data.keyword.amashort}} à votre application Android, Cordova ou iOS existante. Vous pouvez également télécharger l'exemple
d'application HelloAuthentication.
   * **Android** : ([Configuration du logiciel SDK Android](getting-started-android.html)) ([Exemple](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))
  
   * **Cordova** : ([Configuration du plug-in Cordova](getting-started-cordova.html)) ([Exemple](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))
  
   * ****iOS (SDK Swift) : ([Configuration du SDK Swift iOS](getting-started-ios-swift-sdk.html))
      ([Exemple](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))
  
   * **iOS (SDK Objective-C)** : ([Configuration du SDK Objective-C pour iOS](getting-started-ios.html)) ([Exemple](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))
   
   **Remarque :** alors que le SDK Objective-C reste complètement pris en charge et est toujours considéré comme le SDK principal pour Bluemix Mobile Services, il est prévu qu'il soit interrompu plus tard dans l'année et remplacé par le nouveau SDK Swift. Si vous créez une application, il est vivement recommandé d'utiliser le SDK Swift (voir [Configuration du SDK Swift iOS](getting-started-ios-swift-sdk.html)).

1. **Facultatif :** configurez un fournisseur d'identité pour votre application. Vous ne pouvez configurer qu'un fournisseur d'identité par
application. La configuration d'un fournisseur d'identité permet aux utilisateurs de votre application mobile de se connecter avec leur compte Facebook
ou Google+ existant. Ou bien, vous pouvez définir le mode de connexion des utilisateurs en créant une authentification personnalisée.
   * [Authentification des utilisateurs à l'aide des données d'identification Facebook](facebook-auth-overview.html)
   * [Authentification des utilisateurs avec des données d'identification Google](google-auth-overview.html)
   * [Authentification des utilisateurs en utilisant un fournisseur d'identité personnalisé](custom-auth.html)

1. Configurez la surveillance et la journalisation des applications.

    Pour plus d'informations, voir [Surveillance des applications](app-monitoring.html).

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
* [Core SDK (iOS - Objective-C - Déprécié](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [Authentification personnalisée -
exemple simple](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [Authentification personnalisée -
exemple avancé](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## Référence d'API
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS (SDK Objective-C) - Déprécié](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## Liens connexes
{: #general}
* [Présentation](overview.html){: new_window}
