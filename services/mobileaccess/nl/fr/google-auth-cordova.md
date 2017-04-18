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

**Important : Le service {{site.data.keyword.amafull}} est remplacé par le service {{site.data.keyword.appid_full}}.**

# Activation de l'authentification Google pour les applications Cordova
{: #google-auth-cordova}

Pour intégrer vos applications Cordova {{site.data.keyword.amafull}} à l'authentification Google, vous devez modifier le code de plateforme natif de l'application Cordova (Java ou Objective-C), ainsi que le WebView Cordova (Javascript). Chaque plateforme doit être configurée séparément. Utilisez l'environnement de développement natif pour modifier le code natif, par exemple, dans Android Studio ou Xcode.

## Avant de commencer
{: #before-you-begin}

Vous devez disposer des éléments suivants :

* Un projet Cordova qui est instrumenté avec le SDK client de {{site.data.keyword.amashort}}.  Pour plus d'informations, voir [Configuration du plug-in Cordova](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).  
* Une instance d'une application {{site.data.keyword.Bluemix_notm}} qui est protégée par le service {{site.data.keyword.amashort}}. Pour plus d'informations sur la création d'un service de back end {{site.data.keyword.Bluemix_notm}}, voir [Initiation](index.html).
* Route de votre application. Il s'agit de l'URL de votre application back end.
* Valeur de votre **TenantID**. Ouvrez votre service dans le tableau de bord {{site.data.keyword.Bluemix_notm}}. Cliquez sur **Options pour application mobile**. La valeur `tenantId` (qui porte également le nom d'`appGUID`) est affichée dans la zone **App GUID / TenantId**. Vous aurez besoin de cette valeur pour initialiser le Gestionnaire des autorisations.
*  Trouvez la région où votre application {{site.data.keyword.Bluemix_notm}} est hébergée. Vous pouvez trouver votre région Bluemix actuelle dans l'en-tête, en regard de l'icône **Avatar**![icône Avatar](images/face.jpg "icône Avatar"). La valeur de région doit être l'une des suivantes : **US South**, **Sydney** ou **UK**. Les valeurs des constantes SDK exactes qui correspondent à ces noms sont indiquées dans les exemples de code.
* (Facultatif) Familiarisez-vous avec les sections suivantes :
   * [Activation de l'authentification Google pour les applications Android](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [Activation de l'authentification Google pour les applications iOS](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)


## Configuration de la plateforme Android
{: #google-auth-cordova-android}

Les étapes requises pour configurer l'authentification Google dans la plateforme Android d'une application Cordova sont très semblables à celles qui sont requises pour les applications natives. Voir [Activation de l'authentification Google pour les applications Android](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html) et effectuez les opérations suivantes :

   * [Création d'un projet sur Google Developer Console](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html#create-google-project). Cela vous montre comment configurer le service d'authentification sur le site Web Google Developers.
   * [Configuration de MCA pour l'authentification Google](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html#google-auth-android-config). Cet exemple montre comment configurer votre {{site.data.keyword.amashort}} pour utiliser l'autorisation Google.

### Configuration du SDK client pour Android Cordova

1. Dans votre dossier de projet Android, ouvrez le fichier `build.gradle` pour votre module d'application (et **non pas** le projet `build.gradle`).
	Localisez la section des dépendances et ajoutez une nouvelle dépendance de compilation pour le SDK client :

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',
        name:'googleauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// autres dépendances
	}
	```
	{: codeblock}

1. Synchronisez votre projet avec Gradle en cliquant sur **Tools (Outils) > Android > Sync Project with Gradle Files (Synchroniser le projet avec les fichiers Gradle)**.

1. L'API `GoogleAuthenticationManager` doit toujours être enregistrée dans le code natif. Ajoutez le code ci-dessous à la méthode `onCreate` de l'activité principale :

	```Java
	String tenantId = "<tenantId>";
	MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
	BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
	GoogleAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
	```
	{: codeblock}

1. Ajoutez le code suivant à votre activité :

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

## Configuration de la plateforme iOS
{: #google-auth-cordova-ios}

Les étapes requises pour configurer l'intégration de l'authentification Google dans la plateforme iOS d'une application Cordova sont semblables à celles qui sont requises pour les applications natives. La différence principale est que l'interface de ligne de commande Cordova ne prend actuellement pas en charge le gestionnaire de dépendances CocoaPods. Vous devez ajouter manuellement les fichiers requis pour l'intégration avec l'authentification Google. Pour plus d'informations, voir [Activation de l'authentification Google pour les applis iOS (SDK Swift)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html). Exécutez les étapes suivantes :

   * [Préparation de votre application pour Google Sign-In](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-sign-in-ios) : prépare Google Sign-In pour l'authentification des applications iOS de {{site.data.keyword.amashort}}.

   * [Configuration de MCA pour l'authentification Google](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-auth-ios-config) : configure votre service {{site.data.keyword.amashort}} pour qu'il fonctionne avec Google Sign-In.

   * [Configuration du SDK du client MCA pour iOS](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html#google-auth-ios-sdk) : configure votre client {{site.data.keyword.amashort}} pour qu'il fonctionne avec Google Sign-In.


### Activez le partage de chaîne de certificats pour iOS
{: #enable_keychain}

Activez le partage de chaîne de certificats, `Keychain Sharing`. Accédez à l'onglet `Capabilities` et basculez `Keychain Sharing` sur `On` dans votre projet Xcode.


### Initialisation du Gestionnaire d'autorisations dans votre code iOS

Initialisez le Gestionnaire d'autorisations {{site.data.keyword.amashort}} dans Objective-C dans le fichier `AppDelgate.m`.

```
#import "<your_module_name>-Swift.h"

- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

{
	[CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];

	[[GoogleAuthenticationManager sharedInstance] register];

	self.viewController = [[MainViewController alloc] init];

	[[GoogleAuthenticationManager sharedInstance] onFinishLaunchingWithApplication:application withOptions:launchOptions];

	return [super application:application didFinishLaunchingWithOptions:launchOptions];
	}

- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {
	return [[GoogleAuthenticationManager sharedInstance] onOpenURLWithApplication:application url:url 
	sourceApplication:sourceApplication annotation:annotation];
}
```
{: codeblock}


####Remarque :
{: #note notoc}

* Remplacez `<your_module_name>` par le nom du module de votre projet. Par exemple, si le nom de votre module est `Cordova`, la ligne d'importation doit être `#import "Cordova-Swift.h"` Recherchez le nom du module. Accéder à l'onglet
`Build Settings`, `Packaging` > `Product Module Name`.
* Remplacez le `<tenantId>` par l'identifiant de votre locataire (voir [Avant de commencer](#before-you-begin)).


## Initialisation du SDK client {{site.data.keyword.amashort}} dans le WebView Cordova
{: #google-auth-cordova-initialize}

Pour toutes les plateformes, utilisez le code Javascript suivant dans votre Cordova pour initialiser le SDK client de {{site.data.keyword.amashort}}.

```JavaScript
BMSClient.initialize("<applicationBluemixRegion>");
```
{: codeblock}

Remplacez `<applicationBluemixRegion>` par votre région (voir [Avant de commencer](#before-you-begin)).

## Test de l'authentification
{: #google-auth-cordova-test}

Une fois que le SDK client est initialisé, vous pouvez commencer à envoyer des requêtes à votre application back end mobile.

### Avant de commencer
{: #google-auth-cordova-testing-before}

Vous devez disposer d'une application de back end protégée par {{site.data.keyword.amashort}} sur le noeud final
`/protected`. Pour configurer un noeud final `/protected`, voir la rubrique [Protection des ressources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Essayez d'envoyer une demande à un noeud final protégé de votre application back end mobile dans votre navigateur de bureau en ouvrant `{applicationRoute}/protected`, par exemple : `http://my-mobile-backend.mybluemix.net/protected`.

1. Le noeud final `/protected` d'une application back end mobile créée avec le conteneur boilerplate MobileFirst Services est protégé par {{site.data.keyword.amashort}}, seules les applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}} peuvent y accéder. Pour cette raison, le message `Unauthorized` s'affiche dans votre navigateur de bureau.

1. Utilisez votre application Cordova pour faire une demande sur le même noeud final, en utilisant l'URL complète (par exemple `http://my-mobile-backend.mybluemix.net/protected`). Ajoutez le code suivant après avoir initialisé
`BMSClient`.

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new BMSRequest("<your-application-route>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

1. Lancez votre application. L'écran de connexion Google s'affiche.

	![Ecran de connexion Google](images/android-google-login.png)

	![Ecran de connexion Google](images/ios-google-login.png)

	Cet écran peut être légèrement différent si l'appli Facebook n'est pas installée sur votre appareil, ou si vous n'y êtes pas connecté.

1. En cliquant sur **OK**, vous autorisez {{site.data.keyword.amashort}} à utiliser votre identité utilisateur Google à des fins
d'authentification.

1. Votre demande doit aboutir. Selon la plateforme que vous utilisez, vous devez voir un résultat similaire à l'un de ceux ci-dessous dans la console LogCat ou Xcode.

	![Fragments de code sous android](images/android-google-login-success.png)

	![Fragments de code sous iOS](images/ios-google-login-success.png)
