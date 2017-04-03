---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---

Le service {{site.data.keyword.amafull}} est remplacé par le service {{site.data.keyword.appid_full}}.

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Configuration d'une authentification personnalisée pour votre application {{site.data.keyword.amashort}} Android
{: #custom-android}


Configurez votre application Android avec authentification personnalisée afin d'utiliser le SDK client {{site.data.keyword.amashort}} et connectez votre application à {{site.data.keyword.Bluemix}}.

## Avant de commencer
{: #before-you-begin}
Avant de commencer, vous devez disposer des éléments suivants :

* Ressource protégée par une instance du service {{site.data.keyword.amashort}} qui est configurée pour utiliser un fournisseur d'identité personnalisé (voir [Configuration de l'authentification personnalisée](custom-auth-config-mca.html)).  
* Valeur de votre **TenantID**. Ouvrez votre service dans le tableau de bord de {{site.data.keyword.amashort}}. Cliquez sur le bouton **Options pour application mobile**. La valeur `tenantId` (qui porte également le nom d'`appGUID`) est affichée dans la zone **App GUID / TenantId**. Vous aurez besoin de cette valeur pour initialiser le Gestionnaire des autorisations.
* Nom de votre **Realm**. Il s'agit de la valeur que vous avez spécifiée dans la zone **Nom du domaine** de la section **Personnalisé** dans l'onglet **Gestion** du tableau de bord de {{site.data.keyword.amashort}}.
* L'URL de votre application back-end (**Route de l'application**). Vous aurez besoin de ces valeurs pour envoyer des requêtes aux noeuds finaux protégés de votre application back end.
* Votre **région** {{site.data.keyword.Bluemix_notm}}. Vous pouvez trouver votre région {{site.data.keyword.Bluemix_notm}} actuelle dans l'en-tête, en regard de l'icône **Avatar**![icône Avatar](images/face.jpg "icône Avatar"). La valeur de la région qui apparaît doit être l'une des suivantes : `US South`, `United Kingdom` ou `Sydney`, et correspondre aux valeurs requises dans le code Javascript de WebView : `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` ou `BMSClient.REGION_UK`. Vous aurez besoin de cette valeur pour initialiser le client {{site.data.keyword.amashort}}.

Pour plus d'informations, voir les sujets suivants :
 * [Initiation à {{site.data.keyword.amashort}}](getting-started.html)
 * [Configuration du SDK Android](getting-started-android.html)
 * [Utilisation d'un fournisseur d'identité personnalisé](custom-auth.html)
 * [Création d'un fournisseur d'identité personnalisé](custom-auth-identity-provider.html)
 * [Configuration de {{site.data.keyword.amashort}} pour l'authentification personnalisée](custom-auth-config-mca.html)



## Initialisation du logiciel SDK client de {{site.data.keyword.amashort}}
{: #custom-android-initialize}
Si vous disposez d'une application Android équipée du SDK Android {{site.data.keyword.amashort}}, vous pouvez ignorer cette section.
1. Dans votre projet Android dans Android Studio, ouvrez le fichier `build.gradle` de votre module d'application (et non pas le fichier `build.gradle` du projet).

1. Dans le fichier `build.gradle`, localisez la section `dependencies` et vérifiez que la dépendance suivante existe :

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

1. Synchronisez votre projet avec Gradle. Cliquez sur **Tools (Outils) > Android > Sync Project with Gradle Files (Synchroniser le projet avec les fichiers Gradle)**.

1. Ouvrez le fichier `AndroidManifest.xml` de votre projet Android.
Ajoutez le droit d'accès à Internet sous l'élément `<manifest>` :

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```
	{: codeblock}

1. Initialisez le logiciel SDK.  
	En général, vous pouvez placer le code d'initialisation dans la méthode `onCreate` de l'activité principale dans votre application Android, bien que cet emplacement ne soit pas obligatoire.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);
	```
	{: codeblock}

Remplacez `BMSClient.REGION_UK` par la région {{site.data.keyword.amashort}}. Pour plus d'informations sur l'obtention de ces valeurs, voir [Avant de commencer](#before-you-begin).


## Interface du programme d'écoute d'authentification
{: #custom-android-authlistener}

Le SDK client de {{site.data.keyword.amashort}} fournit l'interface `AuthenticationListener` qui vous permet d'implémenter un flux d'authentification personnalisé. L'interface `AuthenticationListener` expose trois méthodes qui sont appelées dans des phases différentes du processus d'authentification.

### Méthode onAuthenticationChallengeReceived
{: #custom-onAuth}
Appelez cette méthode lorsqu'une demande d'authentification personnalisée reçue provient du service {{site.data.keyword.amashort}}.

```Java
void onAuthenticationChallengeReceived(AuthenticationContext authContext, JSONObject challenge, Context context);
```
{: codeblock}


#### Arguments
{: #custom-android-onAuth-arg}

* `AuthenticationContext` : Fourni par le SDK client de {{site.data.keyword.amashort}} pour vous permettre de communiquer les réponses aux demandes d'authentification ou les échecs de collecte des données d'identification.  Par exemple, lorsque l'utilisateur annule la demande d'authentification.
* `JSONObject` : Contient une demande d'authentification personnalisée, renvoyée par un fournisseur d'identité personnalisé.
* `Context` : Référence au contexte Android qui a été utilisé lors de l'envoi de la demande. Cet argument représente généralement une activité Android.

En appelant la méthode `onAuthenticationChallengeReceived`, le SDK client de {{site.data.keyword.amashort}} délègue le contrôle au développeur.  Le service attend les données d'identification. Le développeur doit collecter les données d'identification et les fournir au SDK client de {{site.data.keyword.amashort}} par l'une des méthodes de l'interface `AuthenticationContext`.

### Méthode onAuthenticationSuccess
{: #custom-android-authlistener-onsuccess}
Appelez cette méthode après une authentification réussie. Les arguments comprennent le contexte Android et un objet JSON facultatif contenant des informations détaillées sur le succès de l'authentification.
```Java
void onAuthenticationSuccess(Context context, JSONObject info);
```
{: codeblock}

### Méthode onAuthenticationFailure
{: #custom-android-authlistener-onfail}
Appelez cette méthode en cas d'échec de l'authentification. Les arguments incluent le contexte Android et un objet JSON facultatif
(`JSONObject`) contenant des informations détaillées sur l'échec de l'authentification.
```Java
void onAuthenticationFailure(Context context, JSONObject info);
```
{: codeblock}

## Interface AuthenticationContext
{: #custom-android-authcontext}

`AuthenticationContext` est fourni comme argument de la méthode `onAuthenticationChallengeReceived` d'une interface `AuthenticationListener` personnalisée. Vous devez collecter les données d'identification et utiliser les méthodes `AuthenticationContext` pour renvoyer des données d'identification au SDK client de {{site.data.keyword.amashort}} ou pour signaler un incident. Utilisez l'une des méthodes suivantes.

```Java
void submitAuthenticationChallengeAnswer(JSONObject answer);
```
{: codeblock}

```Java
void submitAuthenticationFailure (JSONObject info);
```
{: codeblock}

## Exemple d'implémentation d'un programme d'écoute d'authentification personnalisé
{: #custom-android-samplecustom}

Cet exemple de programme d'écoute d'authentification est conçu pour fonctionner avec un fournisseur d'identité personnalisé. Vous pouvez télécharger cet exemple depuis le [référentiel Github ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}.

```Java
package com.ibm.helloworld;
import android.content.Context;
import android.util.Log;
import com.ibm.mobilefirstplatform.clientsdk.android.security.mca.api.AuthenticationContext;
import com.ibm.mobilefirstplatform.clientsdk.android.security.mca.api.AuthenticationListener;
import org.json.JSONException;
import org.json.JSONObject;

public class CustomAuthenticationListener implements AuthenticationListener {
	@Override
	public void onAuthenticationChallengeReceived (AuthenticationContext authContext,
											JSONObject challenge, Context context) {

		log("onAuthenticationChallengeResceived :: " + challenge.toString());

		// In this sample the AuthenticationListener immediatelly returns a hardcoded
		// set of credentials. In a real life scenario this is where developer would
		// show a login screen, collect credentials and invoke
		// authContext.submitAuthenticationChallengeAnswer() API

		JSONObject challengeResponse = new JSONObject();
		try {
			challengeResponse.put("username", "john.lennon");
			challengeResponse.put("password", "12345");
			authContext.submitAuthenticationChallengeAnswer(challengeResponse);
		} catch (JSONException e){

			// In case there was a failure collecting credentials you need to report
			// it back to the AuthenticationContext. Otherwise Mobile Client
			// Access client SDK will remain in a waiting-for-credentials state
			// forever

			log("Cette situation ne devrait jamais se produire...");
			authContext.submitAuthenticationFailure(null);
		}
	}

	@Override
	public void onAuthenticationSuccess (Context context, JSONObject info) {
		log("onAuthenticationSuccess :: " + info.toString());
	}

	@Override
	public void onAuthenticationFailure (Context context, JSONObject info) {
		log("onAuthenticationFailure :: " + info.toString());
	}

	private void log(String text){
		Log.d("CustomAuthListener", text);
	}
}
```
{: codeblock}

## Enregistrement d'un programme d'écoute d'authentification personnalisé
{: #custom-android-register}

Après avoir créé un programme d'écoute d'authentification personnalisé, enregistrez-le auprès de `BMSClient` avant de commencer à l'utiliser. Ajoutez le code suivant à votre application. Ce code doit être appelé avant l'envoi de demandes à vos ressources protégées.

```Java
MCAAuthorizationManager mcaAuthorizationManager = 
      MCAAuthorizationManager.createInstance(this.getApplicationContext(),"<MCAServiceTenantId>");
mcaAuthorizationManager.registerAuthenticationListener(realmName, new CustomAuthenticationListener());
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);

```
{: codeblock}


Dans le code :
* Remplacez `MCAServiceTenantId` par la valeur **TenantId** (voir [Avant de commencer](##before-you-begin)).
* Utilisez le nom de domaine, `realmName`, que vous avez spécifié dans le tableau de bord {{site.data.keyword.amashort}} (voir [Configuration de l'authentification personnalisée](custom-auth-config-mca.html)).


## Test de l'authentification
{: #custom-android-testing}
Une fois que le SDK client est initialisé et qu'un programme AuthenticationListener est enregistré, vous pouvez commencer à envoyer des demandes à votre application de back end mobile.

### Avant de tester
{: #custom-android-testing-before}
Vous devez disposer d'une application qui possède une ressource protégée par {{site.data.keyword.amashort}} sur le noeud final `/protected`.


1. Envoyez une requête au noeud final protégé (`{applicationRoute}/protected`) de votre application back end mobile depuis votre navigateur. Par exemple : `http://my-mobile-backend.mybluemix.net/protected`. Pour plus d'informations sur l'obtention de la valeur `{applicationRoute}`, voir [Avant de commencer](#before-you-begin).

1. Le noeud final `/protected` d'une application de back end mobile qui a été créée avec le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} est protégé par {{site.data.keyword.amashort}}. Ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}. En conséquence, un message `Unauthorized` s'affiche dans le navigateur.

1. Utilisez votre application Android pour envoyer une demande au même noeud final protégé qui inclut `{applicationRoute}`. Ajoutez le code ci-dessous après avoir initialisé `BMSClient` et enregistré votre programme d'écoute d'authentification.

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

1. 	Lorsque votre demande aboutit, la sortie suivante figure dans l'outil LogCat :

	![image](images/android-custom-login-success.png)

 Vous pouvez également ajouter une fonctionnalité de déconnexion en ajoutant le code suivant :

 ```Java
 MCAAuthorizationManager.getInstance().logout(getApplicationContext(), listener);
 ```
 {: codeblock}


 Si vous appelez ce code alors qu'un utilisateur est connecté, l'utilisateur est déconnecté. Si l'utilisateur tente à nouveau de se connecter, il doit à nouveau soumettre ses données d'identification au serveur.

 La valeur `listener` transmise à la fonction de déconnexion peut être `null`.
