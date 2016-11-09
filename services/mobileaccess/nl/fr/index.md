---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"
---


# Initiation à {{site.data.keyword.amashort}}
{: #gettingstarted}


Ajoutez une fonctionnalité de sécurité à votre application mobile avec le service {{site.data.keyword.amafull}}. Vous pouvez configurer une autorisation client pour accéder à des ressources de back end protégées s'exécutant sur {{site.data.keyword.Bluemix_notm}}. Utilisez des fournisseurs d'identité (Google et Facebook) ou des identités personnalisées pour authentifier les utilisateurs et accorder un accès aux ressources de back-end protégées et aux applications Web.
{:shortdesc}

**Remarque :** Le service {{site.data.keyword.amashort}} était dénommé auparavant Advanced Mobile
Access.


Mise en route du service {{site.data.keyword.amashort}} :

1. Utilisez le tableau de bord {{site.data.keyword.Bluemix_notm}} pour créer une application back end mobile ou configurer une application
existante.
  - Vous pouvez sélectionner le conteneur boilerplate **MobileFirst Services Starter** dans le catalogue
{{site.data.keyword.Bluemix_notm}}.
  - Vous pouvez aussi lier le service à une application existante et la configurer.

   Quand vous utilisez MobileFirst Services Starter, vous obtenez une instance du contexte d'exécution Node.js qui s'exécute sur IBM {{site.data.keyword.Bluemix_notm}} pour implémenter votre logique de back end personnalisée. Un ensemble de services mobiles de base qui fournissent des fonctions de sécurité, de données, d'envoi par commande push et de surveillance est lié à cette application
Node.js. Une fois l'application {{site.data.keyword.Bluemix_notm}} Node.js créée, vous pouvez configurer votre environnement de développement
et commencer à utiliser les logiciels SDK de {{site.data.keyword.Bluemix_notm}} Mobile Services. Vous pouvez utiliser les logiciels SDK pour accéder aux services qui sont liés à votre application en cloud à l'aide de simples appels d'API.
  
2. Sécurisez les ressources côté serveur.

   Protégez vos ressources de back end mobile s'exécutant sous les contextes d'exécution Node.js ou
Liberty for Java&trade; avec sécurité OAuth activée pour les applications mobiles. Pour plus d'informations, voir [Protection des ressources](protecting-resources.html).
   Pour plus d'informations sur l'application de back end mobile par défaut, reportez-vous à l'exemple d'application
[bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop).

3. Configurez votre environnement principal de développement {{site.data.keyword.amashort}}.
   
	####Développement client
   {: #client-development}
   
	Vous pouvez ajouter le SDK {{site.data.keyword.amashort}} à votre application Android, iOS ou Cordova existante, comme suit : 
   * Android : ([Configuration du logiciel SDK Android](getting-started-android.html)) ([Exemple](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))
  
   * iOS (SDK Swift) : ([Configuration du SDK Swift iOS](getting-started-ios-swift-sdk.html))
      ([Exemple](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))
  
   * iOS (SDK Objective-C) : ([Configuration du SDK iOS Objective-C](getting-started-ios.html)) ([Exemple](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))

   * Cordova : ([Configuration du plug-in Cordova](getting-started-cordova.html)) ([Exemple](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))
   
   **Remarque :** Bien que le SDK Objective-C continue à être totalement pris en charge et soit toujours considéré comme le SDK principal
pour {{site.data.keyword.amashort}}, il est envisagé de le retirer plus tard cette année et de le remplacer par le nouveau SDK Swift. Si vous créez une application, il est vivement recommandé d'utiliser le SDK Swift (voir [Configuration du SDK Swift iOS](getting-started-ios-swift-sdk.html)).

	####Développement Web
   {: #web-development}

   Le service {{site.data.keyword.amashort}} peut protéger votre application Web, sans requérir de SDK spécial. Vous pouvez exploiter divers
fournisseurs d'identité, en sus de la protection assurée par le service {{site.data.keyword.amashort}}. L'intégration {{site.data.keyword.amashort}} permet à toute application Web, quelle que soit la technologie qu'elle implémente, de tirer parti du protocole OAuth2. Pour plus d'informations sur la configuration de votre
application Web pour accéder au service {{site.data.keyword.amashort}} via des fournisseurs d'identité différents, voir :

    * [Activation de l'authentification Facebook pour les applications Web](facebook-auth-web.html)
              
    * [Activation de l'authentification Google pour les applications Web](google-auth-web.html)
              
    * [Activation d'une authentification personnalisée pour les applications Web](custom-auth-web.html)
              
4. **Facultatif :** configurez un fournisseur d'identité pour votre application. Vous ne pouvez configurer qu'un fournisseur d'identité par
application. La configuration d'un fournisseur d'identité permet aux utilisateurs de votre application mobile de se connecter avec leur compte Facebook
ou Google+ existant. Ou bien, vous pouvez définir le mode de connexion des utilisateurs en créant une authentification personnalisée.
   * [Authentification des utilisateurs à l'aide des données d'identification Facebook](facebook-auth-overview.html)
   * [Authentification des utilisateurs avec des données d'identification Google](google-auth-overview.html)
   * [Authentification des utilisateurs en utilisant un fournisseur d'identité personnalisé](custom-auth.html)

5. Configurez la surveillance et la journalisation de votre application.

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
