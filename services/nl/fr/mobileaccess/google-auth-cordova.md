---

Copyright : 2015, 2016

---

# Activation de l'authentification Google dans les applis Cordova
{: #google-auth-cordova}
Pour configurer l'intégration de l'authentification Google dans les applications Cordova, vous devez faire des modifications en Java, Objective-C ou Swift dans le code natif de l'application Cordova. Chaque plateforme doit être configurée séparément. Utilisez l'environnement de développement natif pour modifier le code natif, par exemple, dans Android Studio ou Xcode.

## Avant de commencer
{: #before-you-begin}
* Vous devez disposer d'une ressource protégée par {{site.data.keyword.amashort}} et d'un projet Cordova instrumenté avec le SDK client de {{site.data.keyword.amashort}}.  Pour plus d'informations, voir [Initiation à {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) et [Configuration du plug-in Android](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).  
* Protégez manuellement votre application de back end avec le SDK serveur de {{site.data.keyword.amashort}}. Pour plus d'informations, voir [Protection des ressources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).
* (Facultatif) Familiarisez-vous avec les sections suivantes :
   * [Activation de l'authentification Google dans les applis Android](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [Activation de l'authentification Google dans les applis iOS](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)


## Configuration de la plateforme Android
{: #google-auth-cordova-android}

Les étapes requises pour configurer l'intégration de l'authentification Google dans la plateforme Android d'une application Cordova sont très semblables à celles qui sont requises pour les applications natives. Pour plus d'informations, voir [Activation de l'authentification Google dans les applis Android](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html). Configurez les éléments suivants :

* Configuration d'un projet Google pour la plateforme Android
* Configuration de {{site.data.keyword.amashort}} pour l'authentification Google
* Configuration du SDK client de {{site.data.keyword.amashort}} pour Android

La seule différence lorsque vous configurez des applications Cordova est que vous devez initialiser le SDK client de {{site.data.keyword.amashort}} dans votre code JavaScript plutôt que dans le code Java. L'API `GoogleAuthenticationManager` doit toujours être enregistrée dans le code natif.

## Configuration de la plateforme iOS
{: #google-auth-cordova-ios}

Les étapes requises pour configurer l'intégration de l'authentification Google dans la plateforme iOS d'une application Cordova sont semblables à celles qui sont requises pour les applications natives. La différence principale est que l'interface de ligne de commande Cordova ne prend actuellement pas en charge le gestionnaire de dépendances CocoaPods.  Vous devez ajouter manuellement les fichiers requis pour l'intégration avec l'authentification Google. Pour plus d'informations, voir [Activation de l'authentification Google dans les applis iOS](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html). Exécutez les étapes suivantes :

* Configuration d'un projet Google pour la plateforme iOS
* Configuration de {{site.data.keyword.amashort}} pour l'authentification Google

### Installation manuelle du SDK {{site.data.keyword.amashort}} pour l'authentification Google et du SDK Google
{: #google-auth-cordova-ios-sdk}
1. Téléchargez l'archive contenant le SDK [{{site.data.keyword.Bluemix}} Mobile Services pour iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)

1. Accédez au répertoire `Sources/Authenticators/IMFGoogleAuthentication` et copiez (faites glisser) tous les fichiers dans votre projet iOS dans Xcode. Les fichiers que vous devez copier sont les suivants :

	> * IMFDefaultGoogleAuthenticationDelegate.h
	> * IMFDefaultGoogleAuthenticationDelegate.m
	> * IMFGoogleAuthenticationDelegate.h
	> * IMFGoogleAuthenticationHandler.h
	> * IMFGoogleAuthenticationHandler.m

Cochez la case **Copy files.... (Copier les fichiers)**.

1. Téléchargez et installez le [logiciel SDK iOS Google+](http://goo.gl/9cTqyZ).

1. Suivez l'étape 2 des tutoriels [Start integrating Google+ into your iOS app](https://developers.google.com/+/mobile/ios/getting-started) pour intégrer le SDK Google+ iOS dans votre projet Xcode.

Continuez à la section **Configuration d'un projet iOS pour l'authentification Google** de
[Configuration d'une plateforme iOS pour l'authentification Google](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html). Enregistrez `IMFGoogleAuthenticationHandler` en code natif comme indiqué à la section `Initialisation du SDK client de {{site.data.keyword.amashort}}`. Il n'est pas nécessaire d'initialiser `IMFClient` dans votre code natif, car cette opération sera bientôt faite dans le code JavaScript.

Ajoutez la ligne suivante à la méthode `application:openURL:sourceApplication:annotation` de votre délégué d'application. Cette ligne informe tous les plug-ins Cordova de leurs événements respectifs.

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```

## Initialisation du logiciel SDK client de {{site.data.keyword.amashort}}
{: #google-auth-cordova-initialize}

Utilisez le code JavaScript suivant dans votre application Cordova pour initialiser le SDK client de {{site.data.keyword.amashort}}.

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```

Remplacez *applicationRoute* et *applicationGUID* par les valeurs de **Route** et **Identificateur global
unique de l'application** de la section **Options pour application mobile** de votre application dans le tableau de bord .

## Test de l'authentification
{: #google-auth-cordova-test}
Lorsque le SDK client est initialisé, vous pouvez commencer à envoyer des demandes à votre système de back end mobile.

### Avant de commencer
{: #google-auth-cordova-testing-before}
Vous devez utiliser le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} et disposer au préalable d'une ressource protégée par {{site.data.keyword.amashort}} sur le noeud final `/protected`. Pour configurer un noeud final `/protected`, voir la rubrique [Protection des ressources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Essayez d'envoyer une demande à un noeud final protégé de votre back end mobile dans votre navigateur de bureau en ouvrant
`{applicationRoute}/protected`, par exemple : `http://my-mobile-backend.mybluemix.net/protected`

1. Le noeud final `/protected` d'un système de back end mobile créé avec le conteneur boilerplate MobileFirst Services est protégé par {{site.data.keyword.amashort}}, par conséquent, seules les applications mobiles instrumentées avec le logiciel SDK client de {{site.data.keyword.amashort}} peuvent y accéder. Pour cette raison, le message `Unauthorized` s'affiche dans votre navigateur de bureau.

1. A l'aide de votre application Cordova, envoyez une demande au même noeud final. Ajoutez le code ci-dessous après avoir initialisé `BMSClient` :

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
	request.send(success, failure);
	```


1. Lancez votre application. Un écran de connexion Google s'affiche.

	![image](images/android-google-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![image](images/ios-google-login.png)
	Cet écran peut être légèrement différent si l'appli Facebook n'est pas installée sur votre périphérique, ou si vous n'y êtes pas connecté.
1. Cliquez sur **OK** pour autoriser {{site.data.keyword.amashort}} à utiliser votre ID utilisateur Google pour l'authentification.

1. 	Votre demande doit aboutir. Selon la plateforme que vous utilisez, vous devez voir le résultat suivant dans la console LogCat ou Xcode.

	![image](images/android-google-login-success.png)

	![image](images/ios-google-login-success.png)
