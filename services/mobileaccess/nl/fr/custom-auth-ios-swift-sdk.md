---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-16"

---

{:codeblock:.codeblock}


# Configuration d'une authentification personnalisée pour votre application {{site.data.keyword.amashort}} iOS (SDK Swift)
{: #custom-ios}

Configurez votre application iOS qui utilise l'authentification personnalisée afin qu'elle se serve du SDK client de {{site.data.keyword.amafull}} et connectez-la à {{site.data.keyword.Bluemix}}.  


## Avant de commencer
{: #before-you-begin}

Avant de commencer, vous devez disposer des éléments suivants :

* Ressource protégée par une instance du service {{site.data.keyword.amashort}} qui est configurée pour utiliser un fournisseur d'identité personnalisé (voir [Configuration de l'authentification personnalisée](custom-auth-config-mca.html)).  
* Valeur de votre **TenantID**. Ouvrez votre service dans le tableau de bord de {{site.data.keyword.amashort}}. Cliquez sur le bouton **Options pour application mobile**. La valeur `tenantId` (qui porte également le nom d'`appGUID`) est affichée dans la zone **App GUID / TenantId**. Vous aurez besoin de cette valeur pour initialiser le Gestionnaire des autorisations.
* Nom de votre **Realm**. Il s'agit de la valeur que vous avez spécifiée dans la zone **Nom du domaine** de la section **Personnalisé** dans l'onglet **Gestion** du tableau de bord de {{site.data.keyword.amashort}}.
* L'URL de votre application back-end (**Route de l'application**). Vous aurez besoin de ces valeurs pour envoyer des requêtes aux noeuds finaux protégés de votre application back end.
* Votre **région** {{site.data.keyword.Bluemix_notm}}. Vous pouvez trouver votre région {{site.data.keyword.Bluemix_notm}} actuelle dans l'en-tête, en regard de l'icône **Avatar**![icône Avatar](images/face.jpg "icône Avatar"). La valeur de région qui apparaît doit être l'une des suivantes : **US South**, **United Kingdom** ou **Sydney** et correspondre aux constantes requises dans le code : `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` ou `BMSClient.Region.sydney`.

Pour plus d'informations, voir les sujets suivants :
 * [Initiation à {{site.data.keyword.amashort}}](index.html)
 * [Configuration du SDK Swift iOS](getting-started-ios-swift-sdk.html)
 * [Utilisation d'un fournisseur d'identité personnalisé](custom-auth.html)
 * [Création d'un fournisseur d'identité personnalisé](custom-auth-identity-provider.html)
 * [Configuration de {{site.data.keyword.amashort}} pour l'authentification personnalisée](custom-auth-config-mca.html)

### Activez le partage de chaîne de certificats pour iOS
{: #enable_keychain}

Activez le partage de chaîne de certificats, `Keychain Sharing`. Accédez à l'onglet `Capabilities` et basculez `Keychain Sharing` sur `On` dans votre projet Xcode.


### Initialisation du logiciel SDK client
{: #custom-ios-sdk-initialize}

Initialisez le logiciel SDK en transmettant le paramètre `applicationGUID` (**TenantId**). En général, vous pouvez placer le code d'initialisation dans la méthode `application:didFinishLaunchingWithOptions` du délégué de l'application, bien que cet emplacement ne soit pas obligatoire.

1. Importez les structures requises dans la classe où vous comptez utiliser le SDK client {{site.data.keyword.amashort}}.

	```Swift
	import UIKit
	import BMSCore
	import BMSSecurity
	```
	{: codeblock}

1. Initialisez le SDK client {{site.data.keyword.amashort}}, remplacez le gestionnaire d'autorisation par `MCAAuthorizationManager`, définissez un délégué d'authentification et enregistrez-le.

```Swift

	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>
	let customRealm = "<yourProtectedRealm>"

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: 
		[UIApplicationLaunchOptionsKey: Any]?) -> Bool {

		let mcaAuthManager = MCAAuthorizationManager.sharedInstance
	    		mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
	 //the regionName should be one of the following BMSClient.Region constants: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney   
		BMSClient.sharedInstance.authorizationManager = mcaAuthManager

	//Auth delegate for handling custom challenge
 class MyAuthDelegate : AuthenticationDelegate {
		func onAuthenticationChallengeReceived(_ authContext: AuthenticationContext, challenge: AnyObject){
		    print("onAuthenticationChallengeReceived")
		    let answer = try? Utils.parseJsonStringtoDictionary( "{\"userName\":\"" + "test" + "\",\"password\":\"" + "test" + "\"}")
			authContext.submitAuthenticationChallengeAnswer(answer)
		}

		func onAuthenticationSuccess(_ info: AnyObject?) {
		    print("onAuthenticationSuccess info = \(info)")
           print("onAuthenticationSuccess")
      }

		func onAuthenticationFailure(_ info: AnyObject?){
		     print("onAuthenticationFailure info = \(info)")
        print("onAuthenticationFailure")
      }
	     }

	     let delegate = MyAuthDelegate()
	     mcaAuthManager.registerAuthenticationDelegate(delegate, realm: customRealm)

	     return true
      }


```
{: codeblock}

Dans le code :
* Remplacez `MCAServiceTenantId` par la valeur **TenantId** et `<applicationBluemixRegion>` par votre **Région** {{site.data.keyword.amashort}} (voir [Avant de commencer](##before-you-begin)).
* Utilisez le nom de domaine, `realmName`, que vous avez spécifié dans le tableau de bord {{site.data.keyword.amashort}} (voir [Configuration de l'authentification personnalisée](custom-auth-config-mca.html)).
* Remplacez `<applicationBluemixRegion>` par la région dans laquelle votre application {{site.data.keyword.Bluemix_notm}} est hébergée. Pour afficher votre région {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône Avatar ![icône Avatar](images/face.jpg "icône Avatar") dans la barre de menu pour ouvrir le widget **Compte et support**.  La valeur de région qui apparaît doit être l'une des suivantes : **US South**, **United Kingdom** ou **Sydney** et correspondre aux constantes requises dans le code : `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` ou `BMSClient.Region.sydney`.


## Test de l'authentification
{: #custom-ios-testing}

Après avoir initialisé le SDK client et enregistré un délégué d'authentification personnalisé, vous pouvez commencer à envoyer des requêtes à votre application de back end mobile.

### Avant de commencer
{: #custom-ios-testing-before}

 Vous devez disposer d'une application créée avec un conteneur boilerplate {{site.data.keyword.mobilefirstbp}} et d'une ressource protégée par {{site.data.keyword.amashort}} sur le noeud final `/protected`.

1. Envoyez une demande à un noeud final protégé de votre application de back end mobile dans votre navigateur en ouvrant `{applicationRoute}/protected`. Remplacez `{applicationRoute}` par la valeur extraite depuis **Options pour application mobile** (voir [Configuration de Mobile Client Access pour l'authentification personnalisée](#custom-auth-ios-configmca)). Exemple : `http://my-mobile-backend.mybluemix.net/protected`.

 Le noeud final `/protected` d'une application de back end mobile qui a été créée avec le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} est protégé par {{site.data.keyword.amashort}}. Ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}. En conséquence, un message `Unauthorized` s'affiche dans le navigateur.

1. A l'aide de votre application iOS, envoyez une demande au même noeud final. Ajoutez le code ci-dessous après avoir initialisé `BMSClient` et enregistré votre délégué d'authentification personnalisé :

    ```Swift

	let protectedResourceURL = "<your protected resource absolute path>"
	let request = Request(url: protectedResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
 if error == nil {
	       print ("response:\(response?.responseText), aucune erreur")
  } else {
	       print ("erreur : \(error)")
  }
	}

	request.send(completionHandler: callBack)
     ```
     {: codeblock}

1. Lorsque vos demandes aboutissent, la sortie suivante figure dans la console Xcode :

	 ```
	 onAuthenticationSuccess info = Optional({
     attributes =     {
	     };
     deviceId = don;
     displayName = "Don+Lon";
     isUserAuthenticated = 1;
     userId = don;
 })
	 response:Optional("Bonjour Don Lon"), no error
	 ```
	 {: codeblock}

1. Vous pouvez également ajouter une fonctionnalité de déconnexion en ajoutant le code suivant :

	 ```
	 MCAAuthorizationManager.sharedInstance.logout(callBack)
	 ```
	 {: codeblock}

 Si vous appelez ce code alors qu'un utilisateur est connecté, l'utilisateur est déconnecté. Lorsque l'utilisateur tente de se reconnecter, il doit à nouveau soumettre ses données d'identification.

 La transmission de `callBack` à la fonction de déconnexion est facultative. Vous pouvez également transmettre la valeur `nil`.
