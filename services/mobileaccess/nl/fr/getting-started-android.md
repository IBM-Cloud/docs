---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"
---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configuration du logiciel SDK Android
{: #getting-started-android}

Instrumentez votre application Android avec le SDK client de {{site.data.keyword.amafull}}, initialisez le SDK et envoyez des demandes à des ressources protégées et non protégées.
{: shortdesc}

## Avant de commencer
{: #before-you-begin}

Vous devez disposer des éléments suivants :

* Une instance d'une application {{site.data.keyword.Bluemix_notm}}.
* Une instance d'un service {{site.data.keyword.amafull}}.
* Valeur de votre **TenantID**. Ouvrez votre service dans le tableau de bord de {{site.data.keyword.amafull}}. Cliquez sur le bouton **Options pour application mobile**. Les valeurs `tenantId` (qui portent également le nom d'`appGUID`) sont affichées dans la zone **App GUID / TenantId**. Vous aurez besoin de cette valeur pour initialiser le Gestionnaire des autorisations.
* Votre **Application Route**. Il s'agit de l'URL de votre application back end. Vous avez besoin de cette valeur pour envoyer des demandes à ses noeuds finaux protégés.
* Votre **région** {{site.data.keyword.Bluemix_notm}}.  Vous pouvez trouver votre région {{site.data.keyword.Bluemix_notm}} actuelle dans l'en-tête, en regard de l'icône **Avatar**![icône Avatar](images/face.jpg "icône Avatar"). La valeur de la région qui apparaît doit être l'une des suivantes : `US South`, `Sydney` ou `United Kingdom`, et correspondre aux valeurs SDK requises dans le code : `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` ou `BMSClient.REGION_UK`. Vous aurez besoin de cette valeur pour initialiser le client {{site.data.keyword.amashort}}.
* Un projet Android Studio, configuré pour fonctionner avec Gradle. Pour plus d'informations sur la configuration de votre environnement de développement Android, accédez au site [Google Developer Tools ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://developer.android.com/sdk/index.html "Icône de lien externe"){: new_window}.

## Installation du SDK client de {{site.data.keyword.amashort}}
{: #install-mca-sdk}

Le SDK client de {{site.data.keyword.amashort}} est distribué avec Gradle, un gestionnaire de dépendances pour les projets Android. Gradle
télécharge automatiquement des artefacts depuis les référentiels et les rend disponibles depuis votre application Android.

1. Créez un projet Android Studio ou ouvrez un projet existant.

1. Ouvrez le fichier `build.gradle` de votre application (**et non pas** le fichier de projet `build.gradle`).

1. Localisez la section **dependencies** dans le fichier `build.gradle`.  Ajoutez une dépendance de compilation pour le SDK client de {{site.data.keyword.amashort}} :

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```
	{: codeblock}

1. Synchronisez votre projet avec Gradle. Cliquez sur **Tools (Outils) &gt; Android &gt; Sync Project with Gradle Files (Synchroniser le projet avec les fichiers Gradle)**.

1. Ouvrez le fichier `AndroidManifest.xml` de votre projet Android. Ajoutez le droit d'accès à Internet sous l'élément `<manifest>` :

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```
	{: codeblock}

## Initialisation du logiciel SDK client de {{site.data.keyword.amashort}}
{: #initalize-mca-sdk}

Initialisez le SDK client en transmettant les paramètres **context** et **region** à la méthode `initialize`. En général, vous pouvez placer le code d'initialisation dans la méthode `onCreate` de l'activité
principale dans votre application Android, bien que cet emplacement ne soit pas obligatoire.

```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));
```
{: codeblock}

* Remplacez `<applicationBluemixRegion>` par la région dans laquelle votre service {{site.data.keyword.Bluemix_notm}} est hébergé.
* Remplacez `<MCAServiceTenantId>` par la valeur **tenantId** 

 (pour plus d'informations sur ces valeurs, voir [Avant de commencer](#before-you-begin)).

## Envoi d'une demande à votre application back end mobile
{: #request}

Une fois que le SDK client {{site.data.keyword.amashort}} est initialisé, vous pouvez commencer à envoyer des requêtes à votre application back end
mobile.

1. Essayez d'envoyer une requête à un noeud final protégé de votre application back end
mobile. Dans votre navigateur, ouvrez l'URL suivante : `{applicationRoute}/protected` (`http://my-mobile-backend.mybluemix.net/protected`, par exemple).   

	Le noeud final `/protected` d'une application back end mobile créée avec le conteneur boilerplate MobileFirst Services Starter est
protégé par {{site.data.keyword.amashort}}. Un message `Non autorisé` est renvoyé dans votre
navigateur vu que ce noeud final n'est accessible que par les applications mobiles instrumentées avec le SDK client
{{site.data.keyword.amashort}}.

1. Utilisez votre application Android pour envoyer une requête au même noeud final. Ajoutez le code ci-dessous après avoir initialisé `BMSClient` :

	```Java
	Request request = new Request("http://my-mobile-backend.mybluemix.net/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
		}
		@Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
			if (null != t) {
				Log.d("Myapp", "onFailure :: " + t.getMessage());
			} else if (null != extendedInfo) {
				Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
			} else {
				Log.d("Myapp", "onFailure :: " + response.getResponseText());
			}
		}
	});
	```
	{: codeblock}

1. Si votre requête aboutit, la sortie suivante sera affichée dans l'utilitaire LogCat :

	![image](images/getting-started-android-success.png)

## Etapes suivantes
{: #next-steps}

Lorsque vous vous êtes connecté au noeud final protégé, les données d'identification n'ont pas été nécessaires. Pour obliger les utilisateurs à utiliser des données d'identification pour se connecter à votre application, vous devez configurer Facebook, Google ou l'authentification personnalisée.

* [Facebook](facebook-auth-android.html)
* [Google](google-auth-android.html)
* [Authentification personnalisée](custom-auth-android.html)
