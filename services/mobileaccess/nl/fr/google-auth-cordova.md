---

copyright:
  years: 2015, 2016

---

# Activation de l'authentification Google pour les applications Cordova
{: #google-auth-cordova}


Dernière mise à jour : 21 juillet 2016
{: .last-updated}

Pour configurer l'intégration de l'authentification Google dans les applications Cordova, vous devez apporter des modifications dans le code natif de
l'application Cordova (Java, Objective-C ou Swift). Chaque plateforme doit être configurée séparément. Utilisez l'environnement de développement natif pour modifier le code natif, par exemple, dans Android Studio ou Xcode.

## Avant de commencer
{: #before-you-begin}
Vous devez disposer des éléments suivants :
* Un projet Cordova qui est instrumenté avec le SDK client de {{site.data.keyword.amashort}}.  Pour plus d'informations, voir [Configuration du plug-in Cordova](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).  
* Une instance d'une application {{site.data.keyword.Bluemix_notm}} qui est protégée par le service {{site.data.keyword.amashort}}. Pour plus d'informations sur la création d'un système de back end {{site.data.keyword.Bluemix_notm}}, voir [Initiation](index.html).
* (Facultatif) Familiarisez-vous avec les sections suivantes :
   * [Activation de l'authentification Google dans les applis Android](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [Activation de l'authentification Google dans les applis iOS](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)


## Configuration de la plateforme Android
{: #google-auth-cordova-android}

Les étapes requises pour configurer l'intégration de l'authentification Google dans la plateforme Android d'une application Cordova sont très semblables à celles qui sont requises pour les applications natives. Pour plus d'informations, voir [Activation de l'authentification Google dans les applis Android](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html). Configurez les éléments suivants :

* Configuration d'un projet Google pour la plateforme Android
* Configuration de {{site.data.keyword.amashort}} pour l'authentification Google
* Configuration du SDK client de {{site.data.keyword.amashort}} pour Android

Pour les applications Cordova, initialisez le SDK client {{site.data.keyword.amashort}} dans votre code JavaScript au lieu du code
Java. L'API `GoogleAuthenticationManager` doit toujours être enregistrée dans le code natif.

## Configuration de la plateforme iOS
{: #google-auth-cordova-ios}

Les étapes requises pour configurer l'intégration de l'authentification Google dans la plateforme iOS d'une application Cordova sont semblables à celles qui sont requises pour les applications natives. La différence principale est que l'interface de ligne de commande Cordova ne prend actuellement pas en charge le gestionnaire de dépendances CocoaPods.  Vous devez ajouter manuellement les fichiers requis pour l'intégration avec l'authentification Google. Pour plus d'informations, voir [Activation de l'authentification Google dans les applis iOS](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html). Exécutez les étapes suivantes :

* Configuration d'un projet Google pour la plateforme iOS
* Configuration de {{site.data.keyword.amashort}} pour l'authentification Google

### Installation manuelle du SDK {{site.data.keyword.amashort}} pour l'authentification Google et du SDK Google
{: #google-auth-cordova-ios-sdk}
1. Téléchargez l'archive contenant le SDK [{{site.data.keyword.Bluemix}} Mobile Services pour iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).

1. Accédez au répertoire `Sources/Authenticators/IMFGoogleAuthentication` et copiez (faites glisser) tous les fichiers dans votre projet iOS dans Xcode. Les fichiers que vous devez copier sont les suivants :

	* IMFDefaultGoogleAuthenticationDelegate.h
	* IMFDefaultGoogleAuthenticationDelegate.m
	* IMFGoogleAuthenticationDelegate.h
	* IMFGoogleAuthenticationHandler.h
	* IMFGoogleAuthenticationHandler.m

Cochez la case **Copy files.... (Copier les fichiers)**.

1. Téléchargez et installez le [logiciel SDK iOS Google+](http://goo.gl/9cTqyZ).

1. Suivez l'étape 2 du tutoriel [Start integrating Google+ into your iOS app](https://developers.google.com/+/mobile/ios/getting-started) pour intégrer le SDK Google+ iOS dans votre projet Xcode.

Continuez à la section **Configuration d'un projet iOS pour l'authentification Google** de
[Configuration d'une plateforme iOS pour l'authentification Google](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html). Enregistrez `IMFGoogleAuthenticationHandler` en code natif comme indiqué à la section `Initialisation du SDK client de {{site.data.keyword.amashort}}`. N'initialisez
pas `IMFClient` dans votre code natif (le client est initialisé dans JavaScript dans la section suivante).

Ajoutez la ligne suivante à la méthode `application:openURL:sourceApplication:annotation` de votre délégué d'application. Ceci assure que
tous les plug-ins soient avisés de leurs événements respectifs.

```
[[NSNotificationCenter defaultCenter] postNotification:[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```

## Initialisation du logiciel SDK client de {{site.data.keyword.amashort}}
{: #google-auth-cordova-initialize}

Utilisez le code JavaScript suivant pour initialiser le SDK client de {{site.data.keyword.amashort}}.

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```

Remplacez *applicationRoute* et *applicationGUID* par les valeurs de **Route** et **Identificateur global
unique de l'application** de la section **Options pour application mobile** de votre application dans le tableau de bord .

## Test de l'authentification
{: #google-auth-cordova-test}
Une fois que le SDK client est initialisé, vous pouvez commencer à envoyer des requêtes à votre application back end mobile.

### Avant de commencer
{: #google-auth-cordova-testing-before}
Vous devez disposer d'une application de back end protégée par {{site.data.keyword.amashort}} sur le noeud final
`/protected`. Pour configurer un noeud final `/protected`, voir la rubrique [Protection des ressources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Essayez d'envoyer une demande à un noeud final protégé de votre application back end mobile dans votre navigateur de bureau en ouvrant `{applicationRoute}/protected`, par exemple : `http://my-mobile-backend.mybluemix.net/protected`.

1. Le noeud final `/protected` d'une application back end mobile créée avec le conteneur boilerplate MobileFirst Services est protégé par {{site.data.keyword.amashort}}, seules les applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}} peuvent y accéder. Pour cette raison, le message `Unauthorized` s'affiche dans votre navigateur de bureau.

1. A l'aide de votre application Cordova, envoyez une demande au même noeud final. Ajoutez le code suivant après avoir initialisé
`BMSClient`.

	```JavaScript 	var success = function(data){
    	console.log("success", data);
    } 	var failure = function(error)
    	{console.log("failure", error);
    } 	var request = new MFPRequest("/protected", MFPRequest.GET); 	request.send(success, failure);
	```


1. Lancez votre application. L'écran de connexion à Google s'affiche.

	![Ecran de connexion à Google](images/android-google-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![Ecran de connexion à Google](images/ios-google-login.png)
	Cet écran peut être légèrement différent si l'application Google n'est pas installée sur votre périphérique, ou si vous n'y êtes pas actuellement connecté.
1. En cliquant sur **OK**, vous autorisez {{site.data.keyword.amashort}} à utiliser votre identité utilisateur Google à des fins
d'authentification.

1. 	Votre demande doit aboutir. Selon la plateforme que vous utilisez, vous devez voir un résultat similaire à l'un de ceux ci-dessous dans la console LogCat ou Xcode.

	![Fragments de code sous android](images/android-google-login-success.png)

	![Fragments de code sous iOS](images/ios-google-login-success.png)
