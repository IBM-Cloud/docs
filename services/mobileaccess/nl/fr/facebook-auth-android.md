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

# Activation de l'authentification Facebook pour les applications Android
{: #facebook-auth-android}

Pour utiliser Facebook comme fournisseur d'identité dans vos applications client Android {{site.data.keyword.amafull}}, ajoutez et configurez le client Android pour accéder à votre application Facebook sur le site Facebook for Developers.
{:shortdesc}

## Avant de commencer
{: #before-you-begin}

Vous devez disposer des éléments suivants :

* Une instance d'un service {{site.data.keyword.amafull}} et une application {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations sur la création d'un système de back end {{site.data.keyword.Bluemix_notm}}, voir [Initiation](index.html).
* L'URL de votre application back-end (**Route de l'application**). Vous aurez besoin de cette valeur pour envoyer des requêtes aux noeuds finaux protégés de votre application back end.
* Valeur de votre **TenantID**. Ouvrez votre service dans le tableau de bord de {{site.data.keyword.amashort}}. Cliquez sur le bouton **Options pour application mobile**. La valeur `tenantId` (qui porte également le nom d'`appGUID`) est affichée dans la zone **App GUID / TenantId**. Vous aurez besoin de cette valeur pour initialiser le Gestionnaire des autorisations.
* Votre **région** {{site.data.keyword.Bluemix_notm}}. Vous pouvez trouver votre région {{site.data.keyword.Bluemix_notm}} actuelle dans l'en-tête, en regard de l'icône **Avatar**![icône Avatar](images/face.jpg "icône Avatar"). La valeur de la région qui apparaît doit être l'une des suivantes : `US South`, `United Kingdom` ou `Sydney`, et correspondre à la valeur SDK requise dans le code Javascript de WebView : `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` ou `BMSClient.REGION_UK`. Vous aurez besoin de cette valeur pour initialiser le client {{site.data.keyword.amashort}}.
* Un projet Android qui est configuré pour fonctionner avec Gradle. Le projet n'a pas besoin d'être instrumenté avec un SDK client de {{site.data.keyword.amashort}}.  
* Une application Facebook avec une plateforme Android sur le site [Facebook for Developers ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://developers.facebook.com/){: new_window} .

**Important :** il n'est pas nécessaire d'installer séparément le SDK Facebook (`com.facebook.FacebookSdk`). Celui-ci est installé automatiquement par Gradle quand vous ajoutez le SDK client Facebook de {{site.data.keyword.amashort}}. Vous
pouvez ignorer cette étape si vous ajoutez la plateforme Android sur le site Facebook for Developers.

## Configuration de l'application sur le site Facebook for Developers
{: #facebook-auth-android-config}

A partir du site Web Facebook for Developers :

1. Connectez-vous à votre compte sur le site Web [Facebook for Developers ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developers.facebook.com){: new_window}.

1. Dans **Products List**, sélectionnez **Facebook Login**.

1. Ajoutez ou configurez la plateforme Android.

1. Entrez le nom du package de votre application Android dans l'invite Google Play Package Name (Nom du package Google Play). Pour identifier le nom de
package de votre application Android, recherchez l'entrée `<manifest ..... package="{nom_votre_package}">` dans le
fichier `AndroidManifest.xml` de projet Android Studio.

1. Entrez le nom de la classe de votre activité principale dans l'invite **Class Name (Nom de classe)**. Le nom de classe est la valeur de
la propriété `android:name` dans la section activity. Si plusieurs activités sont répertoriées dans le fichier
`AndroidManifest.xml`, recherchez celle contenant l'entrée `<intent-filter>`:

	```XML
	<activity
		android:name=".MainActivity"
		android:label="@string/app_name">
		<intent-filter>
			<action android:name="android.intent.action.MAIN"/>
			<category android:name="android.intent.category.LAUNCHER"/>
		</intent-filter>
	</activity>
	```
	{: codeblock}

1. Pour que Facebook puisse vérifier l'authenticité de votre applications, vous devez spécifier le hachage SHA1 de votre certificat de développeur.

	**Au sujet de la sécurité Android :** Sur le système d'exploitation Android, toutes les applications installées sur un appareil Android doivent être signées à l'aide d'un certificat de développeur. L'application Android peut être générée dans deux modes : Debug et Release.

	Utilisez des certificats différents pour ces deux modes.  Les certificats utilisés pour signer les applications Android en mode Debug sont fournies avec le SDK Android, qui est généralement installé automatiquement par Android Studio. Au moment de publier votre appli dans le magasin Google Play, vous devez la signer avec un autre certificat, généralement généré par vous.

	Vous pouvez entrer deux ensembles de hachages de clé avec Facebook : un pour les applications générées en mode Debug avec un certificat de débogage et un autre pour les applications générées en mode Release avec un certificat à cet effet. Pour plus d'informations, voir [Sign Your App ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://developer.android.com/tools/publishing/app-signing.html){: new_window}.

1. Le magasin de clés qui contient le certificat que vous utilisez pour l'environnement de développement est stocké dans le fichier `~/.android/debug.keystore`. Le mot de passe du magasin de clés par défaut est : `android`. Utilisez ce certificat pour générer des applications en mode Debug.

1. Extrayez le hachage de clé du certificat du mode Debug :

	```XML 	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore | openssl sha1 -binary | openssl base64
	```
	{: codeblock}

	**Astuce** : Vous pouvez utiliser la même syntaxe pour extraire le hachage de clé du certificat du mode Release. Remplacez l'alias et le chemin du magasin de clés dans la commande.

1. Copiez et collez le hachage de clé obtenu avec la commande **keytool** dans une invite
Development/Release Key Hashes sur le site Facebook for Developers.

	**Astuce** : Vous pouvez activer l'authentification unique (SSO) si vous prévoyez d'utiliser cette fonction.

1. Cliquez sur **Save Settings (Sauvegarder les paramètres)**.

## Configuration du service {{site.data.keyword.amashort}} pour l'authentification Facebook
{: #facebook-auth-android-mca}

Une fois que vous disposez de l'ID d'application Facebook et avez configuré votre application Facebook pour servir les clients
Android, vous pouvez activer l'authentification Facebook depuis le tableau de bord {{site.data.keyword.amashort}}.

1. Ouvrez votre service {{site.data.keyword.amashort}} dans le tableau de bord.
1. Dans l'onglet **Gérer**, activez **Autorisation**.
1. Développez la section **Facebook**.
1. Ajoutez l'**ID d'application Facebook**.
1. Cliquez sur **Sauvegarder**.

## Configuration du SDK Android client {{site.data.keyword.amashort}} pour l'authentification Facebook
{: #facebook-auth-android-sdk}

Pour configurer le SDK client pour Android, utilisez le gestionnaire de dépendances Gradle dans Android Studio.

1.  Ouvrez le fichier `build.gradle` du module de votre appli.
Votre projet Android peut comporter deux fichiers `build.gradle` : un pour le projet et l'autre pour le module de l'application. Utilisez le fichier du module de l'application.

1. Localisez la section des dépendances dans le fichier `build.gradle` et ajoutez une nouvelle dépendance de compilation pour le SDK client :

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',
        name:'facebookauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// autres dépendances
	}
	```
	{: codeblock}

	**Remarque :** vous pouvez retirer la dépendance sur le module `core` du groupe `com.ibm.mobilefirstplatform.clientsdk.android`, si elle figure dans votre fichier. Le module `facebookauthentication` télécharge le module `core` automatiquement, ainsi que le propre SDK de Facebook.

	Une fois que vous avez enregistré vos mises à jour, le module `facebookauthentication` télécharge et installe tous les SDK nécessaires dans votre projet Android.

1. Synchronisez votre projet avec Gradle en cliquant sur **Tools > Android > Sync project with Gradle Files**.

1. Ouvrez le fichier `res/values/strings.xml` et ajoutez une chaîne `facebook_app_id` contenant l'ID de votre application
Facebook :

	```XML
	<resources>
		<string name="app_name">HelloWorld</string>
		<string name="action_settings">Settings</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
	```
	{: codeblock}

1. Dans le fichier `AndroidManifest.xml` de votre projet Android :
	* Ajoutez le droit d'accès à Internet sous l'élément `<manifest>` :

		```XML
	<uses-permission android:name="android.permission.INTERNET" />
		```
		{: codeblock}

	* Ajoutez les métadonnées requises pour le SDK Facebook à l'élément `<application>` :

		```XML
    <application .......>

			<meta-data
			android:name="com.facebook.sdk.ApplicationId"
			android:value="@string/facebook_app_id"/>

			<activity ...../>
    <activity ...../>
    </application>
		```
		{: codeblock}

	* Ajoutez un élément Facebook activity sous vos activités existantes :

		```XML
    <application .....>
			<activity ...../>
		<activity ...../>

			<activity android:name="com.facebook.FacebookActivity"
				android:configChanges="keyboard|keyboardHidden|screenLayout|screenSize|orientation"
				android:theme="@android:style/Theme.Translucent.NoTitleBar"
				android:label="@string/app_name" />
		</application>
		```
		{: codeblock}

1. Initialisez le SDK client et enregistrez le gestionnaire d'authentification. Initialisez le logiciel SDK client {{site.data.keyword.amashort}} en transmettant les paramètres **context** et **region**.

	En général, vous pouvez placer le code d'initialisation dans la méthode `onCreate` de l'activité
principale dans votre application Android, bien que cet emplacement ne soit pas obligatoire.<br/>

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

	BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));

	FacebookAuthenticationManager.getInstance().register(this);
	```
	{: codeblock}

   * Remplacez `BMSClient.REGION_UK` par la région appropriée
   * Remplacez `<MCAServiceTenantId>` par la valeur `tenantId`.

	Pour plus d'informations sur l'obtention de ces valeurs, voir [Avant de commencer](#before-you-begin)).

	**Remarque :** si votre application Android a pour cible Android version 6.0 (API niveau 23) ou supérieure, vous devez vous assurer que l'application dispose d'un appel `android.permission.GET_ACCOUNTS` avant d'appeler `register`. Pour plus d'informations, voir [cette rubrique ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.android.com/training/permissions/requesting.html){: new_window} sur le site Android Developers.

1. Ajoutez le code suivant à votre activité :

	```Java 	@Override 	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}


## Test de l'authentification
{: #testing_auth}

Une fois que le SDK client est initialisé et que le gestionnaire d'authentification Facebook est enregistré, vous pouvez commencer à envoyer des
demandes à votre back end mobile.

### Avant de commencer à tester
{: #facebook-auth-android-testing-before}

Vous devez utiliser le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} et disposer déjà d'une ressource protégée par
{{site.data.keyword.amashort}} sur le noeud final `/protected`. Pour configurer un noeud final `/protected`, voir la rubrique [Protection des ressources](protecting-resources.html).

1. Essayez d'envoyer depuis votre navigateur une requête à un noeud final protégé de votre nouvelle application back end mobile. Ouvrez l'URL suivante :

	`{applicationRoute}/protected`. Exemple : `http://my-mobile-backend.mybluemix.net/protected`.  

	Le noeud final `/protected` d'une application back end mobile créée avec le conteneur boilerplate MobileFirst Services Starter est
protégé par {{site.data.keyword.amashort}}. Un message signalant l'interdiction d'accéder au site (`Unauthorized`) est renvoyé au navigateur. Ce message est renvoyé car ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}.

1. A l'aide de votre application Android, envoyez une demande au même noeud final. Ajoutez le code ci-dessous après avoir initialisé
le client `BMSClient` et enregistré le gestionnaire d'authentification Facebook (`FacebookAuthenticationManager`).

	```Java
	Request request = new Request("{applicationRoute}/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp",  MCAAuthorizationManager.getInstance().getUserIdentity().toString());
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

1. Lancez votre application. Un écran de connexion à Facebook s'affiche.

	![image](images/android-facebook-login.png)

	Cet écran peut être légèrement différent si l'appli Facebook n'est pas installée sur votre appareil, ou si vous n'y êtes pas connecté.

1. Cliquez sur **OK** pour autoriser {{site.data.keyword.amashort}} à utiliser votre ID utilisateur Facebook pour l'authentification.

1. Lorsque votre demande aboutit, la sortie suivante figure dans l'utilitaire LogCat :

	![image](images/android-facebook-login-success.png)

	Vous pouvez également ajouter une fonctionnalité de déconnexion en ajoutant le code suivant :

	```
	FacebookAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
	```
	{: codeblock}

	Si vous appelez ce code lorsqu'un utilisateur est connecté via Facebook, l'utilisateur est déconnecté de Facebook. Lorsque l'utilisateur tente de se
reconnecter, il doit à nouveau soumettre ses données d'identification Facebook.

	La valeur `listener` transmise à la fonction de déconnexion peut être `null`.
