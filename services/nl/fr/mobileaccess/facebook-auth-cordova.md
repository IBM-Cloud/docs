---

Copyright : 2015, 2016

---

# Activation de l'authentification Facebook dans les applis Cordova
{: #facebook-auth-cordova}
Pour configurer l'intégration de l'authentification Facebook dans les applications Cordova, vous devez faire des modifications en Java, Objective-C ou Swift dans le code natif de l'application Cordova. Chaque plateforme doit être configurée séparément. Utilisez l'environnement de développement natif pour modifier le code natif, par exemple, dans Android Studio ou Xcode.

## Avant de commencer
{: #facebook-auth-before}
* Vous devez disposer d'une ressource protégée par {{site.data.keyword.amashort}} et d'un projet Cordova instrumenté avec le SDK client de {{site.data.keyword.amashort}}.  Pour plus d'informations, voir [Initiation à {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) et [Configuration du plug-in Android](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).
* Protégez manuellement votre application de back end avec le SDK serveur de {{site.data.keyword.amashort}}. Pour plus d'informations, voir [Protection des ressources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).
* Créez un ID d'application Facebook. Pour plus d'informations, voir
[Acquisition d'un ID d'application Facebook sur le
portail Facebook Developer](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).
* (Facultatif) Familiarisez-vous avec les sections suivantes :
   * [Activation de l'authentification Facebook dans les applis Android](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html)
   * [Activation de l'authentification Facebook dans les applis iOS](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)


## Configuration de la plateforme Android
{: #facebook-auth-cordova-android}

Les étapes requises pour configurer l'intégration de l'authentification Facebook dans la plateforme Android d'une application Cordova sont très semblables à celles qui sont requises pour les applications natives Android. Pour plus d'informations, voir [Activation de l'authentification Facebook dans les applis Android](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html). Exécutez les étapes suivantes :

* Configuration d'une application Facebook pour la plateforme Android
* Configuration de {{site.data.keyword.amashort}} pour l'authentification Facebook
* Configuration du SDK client de {{site.data.keyword.amashort}} pour Android

La seule différence lorsque vous configurez des applications Cordova est que vous devez initialiser le SDK client de {{site.data.keyword.amashort}} dans votre code JavaScript plutôt que dans le code Java. L'API `FacebookAuthenticationManager` doit toujours être enregistrée dans le code natif.

## Configuration de la plateforme iOS
{: #facebook-auth-cordova-ios}

Les étapes requises pour configurer l'intégration de l'authentification Facebook dans la plateforme iOS d'une application Cordova sont très semblables à celles qui sont requises pour les applications natives iOS. La différence principale est que l'interface de ligne de commande Cordova ne prend actuellement pas en charge le gestionnaire de dépendances CocoaPods. Vous devez ajouter manuellement les fichiers requis pour l'intégration del'authentification Facebook. Pour plus d'informations, voir [Activation de l'authentification Facebook dans les applis iOS](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html). Exécutez les étapes suivantes :

* Configuration d'une application Facebook pour la plateforme iOS
* Configuration de {{site.data.keyword.amashort}} pour l'authentification Facebook

### Installation manuelle du SDK {{site.data.keyword.amashort}} pour l'authentification Facebook et du SDK Facebook
{: #facebook-auth-cordova-ios-sdk}
1. Téléchargez l'archive contenant le SDK [{{site.data.keyword.Bluemix_notm}} Mobile Services pour iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).

1. Accédez au répertoire `Sources/Authenticators/IMFFacebookAuthentication` et copiez (faites glisser) tous les fichiers dans votre projet iOS dans Xcode. Copiez les fichiers suivants :
	* IMFDefaultFacebookAuthenticationDelegate.h
  * IMFDefaultFacebookAuthenticationDelegate.m
	* IMFFacebookAuthenticationDelegate.h
	* IMFFacebookAuthenticationHandler.h
	* IMFFacebookAuthenticationHandler.m

	Lorsque vous y êtes invité par Xcode, sélectionnez **Copy files... (Copier les fichiers...)**.

1. Téléchargez et installez [Facebook SDK v3.19](https://developers.facebook.com/resources/facebook-ios-sdk-3.19.pkg).

1. Le SDK Facebook sera installé dans le répertoire `~/Documents/FacebookSDK`. Accédez à ce répertoire et copiez (faites glisser) le fichier
`FacebookSDK.framework` dans votre projet iOS dans Xcode.

1. 	Cliquez sur la racine de votre projet dans le panneau gauche de Xcode et sélectionnez **Build Phases (Phases de génération)**.

1. Ajoutez le fichier `FacebookSDK.framework` à la liste des bibliothèques liées dans **Link binary with libraries (Lier le binaire
aux bibliothèques)**.

 Voir [Configuration de la plateforme iOS pour
authentification Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html). Enregistrez l'API IMFFacebookAuthenticationHandler dans le code natif comme indiqué dans la section
**Initialisation du SDK Client de {{site.data.keyword.amashort}}**. N'initialisez pas `IMFClient` dans votre code
natif.

Ajoutez la ligne suivante à la méthode `application:openURL:sourceApplication:annotation` de votre délégué d'application. Ce code garantit que
tous les plug-ins Cordova soient avisés de leurs événements respectifs.

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```

## Initialisation du logiciel SDK client de {{site.data.keyword.amashort}}
{: #facebook-auth-cordova-init}

Utilisez le code JavaScript suivant dans votre application Cordova pour initialiser le SDK client de {{site.data.keyword.amashort}}.

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```

Remplacez *applicationRoute* et *applicationGUID* par les valeurs de **Route** et
**Identificateur global unique de l'application** dans la section **Options pour application mobile**.

## Test de l'authentification
{: #facebook-auth-cordova-test}
Une fois que le SDK client est initialisé et que le gestionnaire d'authentification Facebook est enregistré, vous pouvez commencer à envoyer des demandes à votre
back end mobile.

### Avant de commencer
Vous devez utiliser le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} et disposer au préalable d'une ressource protégée par {{site.data.keyword.amashort}} sur le noeud final `/protected`. Pour plus d'informations, voir [Protection des ressources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Depuis votre navigateur, tentez d'envoyer une demande à un noeud final protégé de votre nouveau système de back end mobile. Ouvrez l'URL suivante :
`{applicationRoute}/protected`. Par exemple : `http://my-mobile-backend.mybluemix.net/protected`
<br/>Le noeud final `/protected` d'un système de back end mobile qui a été créé avec le conteneur boilerplate MobileFirst Services Starter est protégé par {{site.data.keyword.amashort}}. Un message signalant l'interdiction d'accéder au site (`Unauthorized`) est renvoyé au navigateur. Ce message est renvoyé car ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}.

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

1. Lancez votre application. Un écran de connexion Facebook s'affiche :

	![image](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![image](images/ios-facebook-login.png)

	> Cet écran peut être légèrement différent si l'appli Facebook n'est pas installée sur votre périphérique, ou si vous n'y êtes pas connecté.

1. Cliquez sur **OK** pour autoriser {{site.data.keyword.amashort}} à utiliser votre ID utilisateur Facebook pour l'authentification.

1. 	Lorsque votre demande aboutit, la sortie suivante figure dans l'utilitaire LogCat ou la console Xcode :

	![Message de succès de l'authentification Facebook pour Android](images/android-facebook-login-success.png)

	![Message de succès de l'authentification Facebook pour iOS ](images/ios-facebook-login-success.png)
