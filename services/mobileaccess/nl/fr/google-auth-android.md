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

# Activation de l'authentification Google pour les applications Android
{: #google-auth-android}

Utilisez Google pour authentifier les utilisateurs sur votre application Android {{site.data.keyword.amafull}}. Ajoutez une fonctionnalité de sécurité {{site.data.keyword.amashort}}.

## Avant de commencer
{: #before-you-begin}

Vous devez disposer des éléments suivants :

* Une instance d'un service {{site.data.keyword.amafull}} et une application {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations sur la création d'un système de back end {{site.data.keyword.Bluemix_notm}}, voir [Initiation](index.html).
* L'URL de votre application back-end (**Route de l'application**). Vous aurez besoin de ces valeurs pour envoyer des requêtes aux noeuds finaux protégés de votre application back end.
* Valeur de votre **TenantID**. Ouvrez votre service dans le tableau de bord de {{site.data.keyword.amashort}}. Cliquez sur le bouton **Options pour application mobile**. La valeur `tenantId` (qui porte également le nom d'`appGUID`) est affichée dans la zone **App GUID / TenantId**. Vous aurez besoin de cette valeur pour initialiser le Gestionnaire des autorisations.
* Votre **région** {{site.data.keyword.Bluemix_notm}}. Vous pouvez trouver votre région {{site.data.keyword.Bluemix_notm}} actuelle dans l'en-tête, en regard de l'icône **Avatar**![icône Avatar](images/face.jpg "icône Avatar"). La valeur de la région qui apparaît doit être l'une des suivantes : `US South`, `United Kingdom` ou `Sydney`, et correspondre aux valeurs requises dans le code Javascript de WebView : `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` ou `BMSClient.REGION_UK`. Vous aurez besoin de cette valeur pour initialiser le client {{site.data.keyword.amashort}}.
* Un projet Android qui est configuré pour fonctionner avec Gradle. Le projet n'a pas besoin d'être instrumenté avec un SDK client de {{site.data.keyword.amashort}}.  

La configuration de l'authentification Google pour votre application Android {{site.data.keyword.amashort}} nécessite également la configuration de :

* L'application {{site.data.keyword.Bluemix_notm}}
* Votre projet Android Studio

## Création d'un projet sur Google Developer Console
{: #create-google-project}

Pour commencer à utiliser Google en tant que fournisseur d'identité, créez un projet dans la [console Google Developer ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.developers.google.com){: new_window}.
Une partie de la création d'une projet consiste à obtenir un ID client Google.  L'ID client Google est un identificateur unique pour votre application utilisé par
l'authentification Google et nécessaire pour configurer le service {{site.data.keyword.amashort}}.

Depuis la console :

1. Créez un projet en utilisant l'API **Google+**.
2. Ajoutez l'accès utilisateur **OAuth**.
3. Avant d'ajouter les données d'identification, vous devez choisir la plateforme (Android).
4. Ajoutez les données d'identification.

Pour terminer la procédure de création des données d'identification, vous devez ajouter l'**empreinte digitale du certificat signataire**.


### Configuration du certificat signataire
{: #signing_cert}

Pour que Google puisse vérifier l'authenticité de votre applications, vous devez spécifier l'empreinte digitale du certificat signataire.

Sur le système d'exploitation Android, toutes les applications installées sur un appareil Android doivent être signées avec un certificat de développeur. Une application Android peut être générée dans deux modes : Debug (débogage) et Release (publication). Il est généralement recommandé d'avoir des certificats différents pour ces deux modes.  Les certificats utilisés pour signer les applications Android en mode Debug sont fournies avec le SDK Android.  Celui-ci est généralement installé automatiquement par Android Studio. Au moment de publier votre application dans Google Play, vous devez la signer avec un autre certificat, généralement généré par vous. Pour plus d'informations, voir [Sign Your App ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://developer.android.com/tools/publishing/app-signing.html){: new_window}.

Un magasin de clés contenant un certificat pour les environnements de développement est stocké dans un fichier `~/.android/debug.keystore`. Le mot de passe du magasin de clés par défaut est `android`. Ce certificat est utilisé pour générer des applications en mode Debug.

1. Extrayez l'empreinte digitale de votre certificat signataire depuis votre environnement de développement client :

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore -list -v
	```
	{: codeblock}

	Vous pouvez utiliser la même syntaxe pour extraire le hachage de clé du certificat du mode Release. Remplacez l'alias et le chemin du magasin de clés dans la commande.

1. Dans la boîte de dialogue des données d'identification Google Console, recherchez la ligne qui commence par `SHA1` sous la rubrique relative aux empreintes digitales de certificat. Copiez la valeur d'empreinte digitale qui a été obtenue en exécutant la commande **keytool** dans la zone de texte.

###Nom du package

1. Dans la boîte de dialogue des données d'identification, entrez le nom du package de votre application Android.

	Pour trouver ce nom, ouvrez le fichier `AndroidManifest.xml` dans Android Studio et recherchez :

	```
	<manifest package="{your-package-name}">
	```
	{: codeblock}

1. Quand vous avez terminé, cliquez sur **Créer**. Ceci finalise la création des données d'identification.

###ID client Google
{: #google-client-id}

Une fois les données d'identification créées, la page relative à ces données affiche votre ID client Google. Notez cette valeur. Vous devez l'enregistrer dans l'application {{site.data.keyword.Bluemix}}.


## Configuration de {{site.data.keyword.amashort}} pour l'authentification Google
{: #google-auth-android-config}

Maintenant que vous disposez d'un ID client Google pour Android, vous pouvez activer l'authentification Google dans le tableau de bord {{site.data.keyword.amashort}}.

1. Ouvrez votre service dans le tableau de bord {{site.data.keyword.amashort}}.
1. Dans l'onglet **Gérer**, activez **Autorisation**.
1. Développez la section **Google**.
1. Dans la zone **ID client pour Android**, spécifiez votre ID client Google pour Android et cliquez sur **Sauvegarder**.

## Configuration du SDK client de {{site.data.keyword.amashort}} pour Android
{: #google-auth-android-sdk}

À partir de votre projet Android Studio.

1. Ouvrez le fichier `build.gradle` du module de votre appli.

	Votre projet Android peut contenir deux fichiers `build.gradle` : un pour le projet et un autre pour le module de l'application. Utilisez le module de l'application.

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

	**Remarque :** vous pouvez retirer la dépendance sur le module `core` du groupe `com.ibm.mobilefirstplatform.clientsdk.android`, si elle figure dans votre fichier. Le module `googleauthentication` le télécharge automatiquement. Le module `googleauthentication` télécharge et installe le SDK Google+ dans votre projet Android.

1. Synchronisez votre projet avec Gradle en cliquant sur **Tools (Outils) > Android > Sync Project with Gradle Files (Synchroniser le projet avec les fichiers Gradle)**.

1. Ouvrez le fichier `AndroidManifest.xml` de votre projet Android.

1. Ajoutez le droit d'accès à Internet sous l'élément `<manifest>` :

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	```
	{: codeblock}

1. Pour pouvoir utiliser le logiciel SDK client de {{site.data.keyword.amashort}}, vous devez l'initialiser en transmettant les paramètres **context** et **region**.

	En général, vous pouvez placer le code d'initialisation dans la méthode `onCreate` de l'activité
principale dans votre application Android, bien que cet emplacement ne soit pas obligatoire.

1. Initialisez le SDK client et enregistrez le gestionnaire d'authentification Google.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

	BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));

	GoogleAuthenticationManager.getInstance().register(this);
	```
	{: codeblock}

	* Remplacez `BMSClient.REGION_UK` par votre {{site.data.keyword.Bluemix_notm}} **Région**.
	* Remplacez `<MCAServiceTenantId>` par la valeur **TenantId**.

	Pour plus d'informations sur l'obtention de ces valeurs, voir [Avant de commencer](##before-you-begin).

	**Remarque :** si votre application Android a pour cible Android version 6.0 (API niveau 23) ou supérieure, vous devez vous assurer que l'application dispose d'un appel `android.permission.GET_ACCOUNTS` avant d'appeler `register`. Pour plus d'informations, voir [Requesting permissions at Run Time ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.android.com/training/permissions/requesting.html){: new_window}.

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

## Test de l'authentification
{: #google-auth-android-test}

Une fois que le SDK client est initialisé et que le gestionnaire d'authentification Google est enregistré, vous pouvez commencer à envoyer des demandes à votre application de back end.

Avant de commencer à tester, vous devez disposer d'une application back end mobile créée depuis le conteneur boilerplate **MobileFirst Services Starter**, ainsi que d'une ressource protégée par le noeud final {{site.data.keyword.amashort}} `/protected`. Pour plus d'informations, voir [Protection des ressources](protecting-resources.html).

1. Essayez d'envoyer une demande à un noeud final protégé de votre application back end mobile dans votre navigateur de bureau en ouvrant `{applicationRoute}/protected`, par exemple : `http://my-mobile-backend.mybluemix.net/protected`.  Pour plus d'informations sur l'obtention de la valeur `{applicationRoute}`, voir [Avant de commencer](#before-you-begin).

	Le noeud final `/protected` d'une application de back end mobile créée avec le conteneur boilerplate MobileFirst Services est protégé par {{site.data.keyword.amashort}}. Il n'est donc accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}. Pour cette raison, le message `Unauthorized` s'affiche dans votre navigateur de bureau.

1. Utilisez votre application Android pour envoyer une demande au même noeud final protégé. Ajoutez le code ci-dessous après avoir initialisé l'instance `BMSClient` et enregistré `GoogleAuthenticationManager`.

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

1. Lancez votre application. Un écran de connexion Google s'affiche. Après la connexion, l'application demande à être autorisée à accéder aux ressources :

	![image](images/android-google-login.png)

	L'interface utilisateur peut varier en fonction de votre appareil Android et selon que vous êtes, ou non, connecté actuellement à Google.

	Cliquez sur **OK** pour autoriser {{site.data.keyword.amashort}} à utiliser votre ID utilisateur Google pour l'authentification.

1. 	Lorsque votre demande aboutit, la sortie suivante figure dans l'outil LogCat :

	![image](images/android-google-login-success.png)

	Vous pouvez également ajouter une fonctionnalité de déconnexion en ajoutant le code suivant :

	```Java
 GoogleAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
	```
	{: codeblock}

	Si vous appelez ce code lorsqu'un utilisateur est connecté via Google, l'utilisateur est déconnecté de Google. Lorsque l'utilisateur tente à nouveau de se
connecter, il doit alors sélectionner le compte Google sous lequel se reconnecter. S'il tente de se reconnecter avec un ID Google qu'il a déjà utilisé, ses données
d'identification ne lui sont pas redemandées. Pour que des données d'identification de connexion lui soient réclamées à nouveau, l'utilisateur soit supprimer
son compte Google de l'appareil Android.

	La valeur `listener` transmise à la fonction de déconnexion peut être `null`.
