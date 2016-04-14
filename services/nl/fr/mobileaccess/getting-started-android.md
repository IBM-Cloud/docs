---

Copyright : 2015, 2016
  
---

# Configuration du logiciel SDK Android
{: #getting-started-android}

Instrumentez votre application Android avec le SDK client de {{site.data.keyword.amashort}}, initialisez le SDK et envoyez des demandes à des ressources protégées et non protégées.

## Avant de commencer
{: #before-you-begin}
* Vous devez disposer d'une instance d'une application de back end mobile protégée par le service {{site.data.keyword.amashort}}. Pour plus d'informations sur la création d'un système de back end mobile, voir [Initiation](getting-started.html).
* Configurez Android Studio et le logiciel SDK d'Android Studio. Pour plus d'informations sur la configuration de votre environnement de développement Android,
voir [Google Developer Tools](http://developer.android.com/sdk/index.html).


## Installation du SDK client de {{site.data.keyword.amashort}}
{: #install-mca-sdk}

Le SDK client de {{site.data.keyword.amashort}} est distribué avec Gradle, un gestionnaire de dépendances pour les projets Android. Gradle
télécharge automatiquement les artefacts à partir des référentiels et les met à la disposition de votre application Android.

1. Créez un projet Android Studio ou ouvrez un projet existant.

1. Ouvrez le fichier `build.gradle`.
**Astuce :** Votre projet Android peut contenir deux fichiers `build.gradle` : un pour le projet et un autre pour le module de l'application. Utilisez le fichier du module de l'application.

1. Localisez la section **Dependencies** dans le fichier `build.gradle`.  Ajoutez une dépendance de compilation pour le SDK client de {{site.data.keyword.amashort}} :

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '1.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
}
```

1. Synchronisez votre projet avec Gradle. Cliquez sur **Tools (Outils) &gt; Android &gt; Sync Project with Gradle Files (Synchroniser le projet avec les fichiers Gradle)**.

1. Ouvrez le fichier `AndroidManifest.xml` de votre projet Android. Ajoutez le droit d'accès à Internet sous l'élément `<manifest>` :

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```

## Initialisation du logiciel SDK client de {{site.data.keyword.amashort}}
{: #initalize-mca-sdk}

Initialisez le SDK en passant les paramètres suivants : le contexte (context), l'identificateur unique global de l'application (applicationGUID) et la route de l'application (applicationRoute) à la méthode `initialize`.


1. Dans la page principale du tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur votre appli. Cliquez sur **Options pour application mobile**. Les valeurs de **Route de l'application** et d'**Identificateur global unique de l'application** sont nécessaires pour initialiser le SDK.

2. Initialisez le SDK client de {{site.data.keyword.amashort}} dans votre appli Android.  En général, vous pouvez placer le code d'initialisation dans la méthode `onCreate` de l'activité
principale dans votre application Android, bien que cet emplacement ne soit pas obligatoire.
<br/>Remplacez *applicationRoute* et *applicationGUID* par les valeurs de la section **Options pour application mobile** du tableau de bord {{site.data.keyword.Bluemix_notm}}.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");
```


## Envoi d'une demande au système de back end mobile
{: #request}

Lorsque le SDK client de {{site.data.keyword.amashort}} est initialisé, vous pouvez commencer à envoyer des demandes à votre système de back end mobile.

1. Tentez d'envoyer une demande à un noeud final protégé de votre nouveau système de back end mobile. Dans votre navigateur, ouvrez l'URL suivante :
`{applicationRoute}/protected`. Par exemple : `http://my-mobile-backend.mybluemix.net/protected`
<br/>Le noeud final `/protected` d'un système de back end mobile qui a été créé avec le conteneur boilerplate MobileFirst Services Starter est protégé par {{site.data.keyword.amashort}}. Un message `Unauthorized` est renvoyé à votre navigateur car ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}.

1. A l'aide de votre application Android, envoyez une demande au même noeud final. Ajoutez le code ci-dessous après avoir initialisé `BMSClient` :

	```Java
	Request request = new Request("/protected", Request.GET);
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

1. Lorsque votre demande aboutit, la sortie suivante figure dans la console LogCat :

	![image](images/getting-started-android-success.png)

## Etapes suivantes
{: #next-steps}

Lorsque vous vous êtes connecté au noeud final protégé, les données d'identification n'ont pas été nécessaires. Pour obliger les utilisateurs à utiliser des données d'identification pour se connecter à votre application, vous devez configurer Facebook, Google ou l'authentification personnalisée.
* [Facebook](facebook-auth-android.html)
* [Google](google-auth-android.html)
* [Authentification personnalisée](custom-auth-android.html)
