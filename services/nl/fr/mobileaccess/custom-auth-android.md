---

Copyright : 2015, 2016

---

# Configuration du SDK client de {{site.data.keyword.amashort}} pour Android
{: #custom-android}
Configurez votre application Android qui utilise l'authentification personnalisée de manière qu'elle utilise le SDK client de {{site.data.keyword.amashort}} et connectez-la à {{site.data.keyword.Bluemix}}.

## Avant de commencer
{: #before-you-begin}
Vous devez disposer d'une ressource protégée par une instance du service {{site.data.keyword.amashort}} qui est configuré pour utiliser un fournisseur d'identité personnalisé.  Votre appli mobile doit aussi être instrumentée à l'aide du SDK client de {{site.data.keyword.amashort}}.  Pour plus d'informations, voir les sujets suivants :
 * [Initiation à {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Configuration du SDK Android](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html)
 * [Utilisation d'un fournisseur d'identité personnalisé](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Création d'un fournisseur d'identité personnalisé](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configuration de {{site.data.keyword.amashort}} pour l'authentification personnalisée](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## Initialisation du logiciel SDK client de {{site.data.keyword.amashort}}
{: #custom-android-initialize}
1. Si votre projet Android est dans Android Studio, ouvrez le fichier `build.gradle` du module de votre appli.
<br/>**Astuce :** Votre projet Android peut contenir deux fichiers `build.gradle` : un pour le projet et un autre pour le module de l'application. Utilisez le fichier du module de l'application.

1. Dans le fichier `build.gradle`, recherchez la section `dependencies` et vérifiez si elle contient la dépendance de compilation suivante. Ajoutez cette dépendance si elle n'existe pas.

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

1. Synchronisez votre projet avec Gradle. Cliquez sur **Tools (Outils) > Android > Sync Project with Gradle Files (Synchroniser le projet avec les fichiers Gradle)**.

1. Ouvrez le fichier `AndroidManifest.xml` de votre projet Android.
Ajoutez le droit d'accès à Internet sous l'élément `<manifest>` :

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```

1. Initialisez le logiciel SDK.  
En général, vous pouvez placer le code d'initialisation dans la méthode `onCreate` de l'activité
principale dans votre application Android, bien que cet emplacement ne soit pas obligatoire.
Remplacez *applicationRoute* et *applicationGUID* par les valeurs de **Route** et **Identificateur global
unique de l'application** obtenues lorsque vous cliquez sur **Options pour application mobile** dans votre application sur le tableau
de bord {{site.data.keyword.Bluemix_notm}}.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");					
	```

## Interface du programme d'écoute d'authentification
{: #custom-android-authlistener}

Le SDK client de {{site.data.keyword.amashort}} fournit l'interface `AuthenticationListener` qui vous permet d'implémenter un flux d'authentification personnalisé. L'interface `AuthenticationListener` expose trois méthodes qui sont appelées dans différentes phases du processus d'authentification.

### Méthode onAuthenticationChallengeReceived
{: #custom-onAuth}
Appelez cette méthode lorsqu'une demande d'authentification personnalisée reçue provient du service {{site.data.keyword.amashort}}.

```Java
void onAuthenticationChallengeReceived(AuthenticationContext authContext, JSONObject challenge, Context context);
```
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

### Méthode onAuthenticationFailure
{: #custom-android-authlistener-onfail}
Appelez cette méthode en cas d'échec de l'authentification. Les arguments comprennent le contexte Android et un objet JSON facultatif contenant des informations détaillées sur l'échec de l'authentification.
```Java
void onAuthenticationFailure(Context context, JSONObject info);
```

## Interface AuthenticationContext
{: #custom-android-authcontext}

`AuthenticationContext`` est fourni comme argument de la méthode `onAuthenticationChallengeReceived` d'une interface `AuthenticationListener` personnalisée. Vous devez collecter les données d'identification et utiliser les méthodes `AuthenticationContext`` pour renvoyer des données d'identification au SDK client de {{site.data.keyword.amashort}} ou pour signaler un incident. Utilisez l'une des méthodes suivantes.

```Java
void submitAuthenticationChallengeAnswer(JSONObject answer);
```
```Java
void submitAuthenticationFailure (JSONObject info);
```

## Exemple d'implémentation d'un programme d'écoute d'authentification personnalisé
{: #custom-android-samplecustom}

Cet exemple de programme d'écoute d'authentification est conçu pour fonctionner avec un fournisseur d'identité personnalisé. Vous pouvez le télécharger depuis le [référentiel Github](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample).

```Java
package com.ibm.helloworld;
import android.content.Context;
import android.util.Log;
import com.ibm.mobilefirstplatform.clientsdk.android.security.api.AuthenticationContext;
import com.ibm.mobilefirstplatform.clientsdk.android.security.api.AuthenticationListener;
import org.json.JSONException;
import org.json.JSONObject;

public class CustomAuthenticationListener implements AuthenticationListener {
	@Override
	public void onAuthenticationChallengeReceived (AuthenticationContext authContext,
											JSONObject challenge, Context context) {

		log("onAuthenticationChallengeResceived :: " + challenge.toString());

		// Dans cet exemple, AuthenticationListener renvoie immédiatement un
		// jeu de données d'identification codé en dur. Dans un scénario réel, c'est ici que le développeur
		// afficherait un écran de connexion, collecterait les données d'identification et appellerait
		// l'API authContext.submitAuthenticationChallengeAnswer()

		JSONObject challengeResponse = new JSONObject();
		try {
			challengeResponse.put("username", "john.lennon");
			challengeResponse.put("password", "12345");
			authContext.submitAuthenticationChallengeAnswer(challengeResponse);
		} catch (JSONException e){

			// En cas d'échec de la collecte des données d'identification, vous devez le signaler
			// à AuthenticationContext. Sinon le SDK client d'accès de client mobile
			// demeure indéfiniment à l'état d'attente de données
			// d'identification

			log("Cette situation ne devrait jamis se produire...");
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

## Enregistrement d'un programme d'écoute d'authentification personnalisé
{: #custom-android-register}

Après avoir créé un programme d'écoute d'authentification personnalisé, enregistrez-le auprès de `BMSClient` avant de commencer à l'utiliser. Ajoutez le code suivant à votre application. Ce code doit être appelé avant l'envoi de demandes à vos ressources protégées.

```Java
BMSClient.getInstance().registerAuthenticationListener(realmName,
									new CustomAuthenticationListener());
```

Utilisez le nom de domaine que vous avez défini dans le tableau de bord {{site.data.keyword.amashort}}.


## Test de l'authentification
{: #custom-android-testing}
Lorsque le SDK client est initialisé et qu'un programme d'écoute d'authentification est enregistré, vous pouvez commencer à envoyer des demandes à votre système de back end mobile.

### Avant de commencer
{: #custom-android-testing-before}
Vous devez disposer d'une application créée avec un conteneur boilerplate {{site.data.keyword.mobilefirstbp}} et d'une ressource protégée par {{site.data.keyword.amashort}} sur le noeud final `/protected`.


1. Envoyez une demande à un noeud final protégé de votre système de back end mobile dans votre navigateur en ouvrant
`{applicationRoute}/protected`, par exemple : `http://my-mobile-backend.mybluemix.net/protected`.

1. Le noeud final `/protected` d'un système de back end mobile qui a été créé avec le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} est protégé par {{site.data.keyword.amashort}}. Ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}. En conséquence, un message `Unauthorized` s'affiche dans le navigateur.

1. A l'aide de votre application Android, envoyez une demande au même noeud final. Ajoutez le code ci-dessous après avoir initialisé `BMSClient` et enregistré votre programme d'écoute d'authentification.

	```Java
	Request request = new Request("/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp", AuthorizationManager.getInstance().getUserIdentity().toString());
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

1. 	Lorsque votre demande aboutit, la sortie suivante figure dans l'outil LogCat :

	![image](images/android-custom-login-success.png)

1. Vous pouvez également ajouter une fonctionnalité de déconnexion en ajoutant le code suivant :

 ```Java
 AuthorizationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 Si vous appelez ce code alors qu'un utilisateur est connecté, l'utilisateur est déconnecté. Lorsque l'utilisateur tente de se reconnecter, il doit à nouveau
soumettre ses données d'identification.

 La valeur `listener` (programme d'écoute) transmise à la fonction de déconnexion peut être Null.
