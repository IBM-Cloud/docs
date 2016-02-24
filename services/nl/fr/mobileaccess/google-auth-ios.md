# Activation de l'authentification Google dans les applis iOS
{: #google-auth-ios}

## Avant de commencer
{: #google-auth-ios-before}
* Vous devez disposer d'une ressource protégée par {{site.data.keyword.amashort}} et d'un projet iOS instrumenté avec le SDK client de {{site.data.keyword.amashort}}.
Pour plus d'informations, voir [Initiation à {{site.data.keyword.amashort}}](getting-started.html) et [Configuration du SDK iOS](getting-started-ios.html).  
* Protégez manuellement votre application de back end avec le SDK serveur de {{site.data.keyword.amashort}}. Pour plus d'informations, voir [Protection des ressources](protecting-resources.html).


## Configuration d'un projet Google pour la plateforme iOS
{: #google-auth-ios-project}
Pour commencer à utiliser Google en tant que fournisseur d'identité, vous devez créer un projet dans Google Developer Console pour obtenir un ID client Google.
Cet ID client est un identificateur unique qui permet à Google de savoir quelle application tente de se connecter.  Si vous avez déjà un projet Google, vous pouvez passer les étapes qui décrivent la création du projet et commencer par l'ajout des droits d'accès.

1. Ouvrez [Google Developer Console](https://console.developers.google.com).

1. Créez un projet. Cliquez sur **Create project (Créer un projet)**.

1. Sélectionnez votre projet et cliquez sur **Use Google APIs (Utiliser les API Google)**.
Vous pouvez aussi cliquer sur **Enable APIs and get credentials like keys (Activer les API et obtenir des données d'identification telles que des clés)**.

1. Dans la liste des API, sélectionnez l'API Google+ et cliquez sur **Enable API (Activer l'API)**.

1. Cliquez sur **Credentials (Données d'identification) > Add credentials (Ajouter des données d'identification)** et sélectionnez **OAuth 2.0 client ID (ID client OAuth 2.0)**.

1. Vous pouvez être invité à définir un nom de produit dans la console d'accord. Faites-le.

1. Puis, vous serez invité à choisir un type d'application. Sélectionnez **iOS**.

1. Donnez un nom parlant à votre client iOS. Entrez l'ID de bundle (*bundleId*) de votre application iOS. Pour le trouver, recherchez la valeur de **Bundle Identifier (ID de bundle)** dans le fichier `info.plist` ou dans l'onglet **General** du projet Xcode.

1. Notez l'ID de votre nouveau client iOS. Vous aurez besoin de cette valeur lors de la configuration de l'application dans {{site.data.keyword.Bluemix_notm}}.


## Configuration de {{site.data.keyword.amashort}} pour l'authentification Google
{: #google-auth-ios-config}

Maintenant que vous disposez d'un ID client iOS, vous pouvez activer l'authentification Google dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.

1. Ouvrez le tableau de bord {{site.data.keyword.Bluemix}} et cliquez sur votre application {{site.data.keyword.Bluemix_notm}}.

1. Cliquez sur **Options pour application mobile** et notez les valeurs de *applicationRoute* et de *applicationGUID*.
Vous aurez besoin de ces valeurs pour initialiser le SDK.

1. Cliquez sur la vignette {{site.data.keyword.amashort}}.

1. Vous arrivez sur le tableau de bord {{site.data.keyword.amashort}}.

1. Cliquez sur **Configurer l'authentification**.

1. Cliquez sur **Google**.

1. Entrez l'ID client pour iOS obtenu lors d'une étape précédente et cliquez sur **Enregistrer**.

## Configuration du SDK client de {{site.data.keyword.amashort}} pour iOS
{: #google-auth-ios-sdk}

### Installation du logiciel SDK client de {{site.data.keyword.amashort}} avec Cocoapods
{: #google-auth-ios-sdk-cocoapods}

1. Naviguez jusqu'à votre projet iOS.

1. Editez le fichier `Podfile` et ajoutez la ligne suivante à la cible requise.

	```
	pod 'IMFGoogleAuthentication'
	```

1. Sauvegardez le fichier `Podfile` et exécutez `pod install` depuis la ligne de commande. 

1. Cocoapods installe les dépendances qui ont été ajoutées. La progression et les composants ajoutés s'affichent.

	> A partir de ce moment, vous devrez toujours ouvrir votre projet à l'aide d'un fichier `xcworkspace` généré par Cocoapods. Son nom est généralement `{your-project-name}.xcworkspace`.  

1. Exécutez `open {your-project-name}.xcworkspace` depuis la ligne de commande pour ouvrir l'espace de travail de votre projet iOS.

### Configuration d'un projet iOS pour l'authentification Google
{: #google-auth-ios-googleauth}

1. Localisez le fichier `info.plist`, généralement situé sous le dossier `Supporting files` de votre projet Xcode.

1. Configurez l'intégration Google en ajoutant les deux schémas d'URL suivants à votre fichier `info.plist`. 

	![image](images/ios-google-infoplist-settings.png)

	> Pour obtenir le premier schéma d'URL, inversez l'ordre des composants de l'ID client issu de Google Developer Console.
Ainsi, si votre ID client est `123123-abcabc.apps.googleusercontent.com`, votre schéma d'URL doit être `com.googleusercontent.apps.123123-abcabc`.

	> Le second schéma d'URL est l'ID de bundle de votre application

1. Vous pouvez aussi mettre à jour le fichier `info.plist` en cliquant avec le bouton droit, en sélectionnant `Open as (Ouvrir en tant que)` -> `Source code (Code source)`, et en ajoutant le code XML suivant :

	```XML
	<key>CFBundleURLTypes</key>
	<array>
		<dict>
			<key>CFBundleTypeRole</key>
			<string>Editor</string>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>com.googleusercontent.apps.123123-abcabc</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeRole</key>
			<string>Editor</string>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>com.ibm.HelloWorld</string>
			</array>
		</dict>
	</array>

	```
	> Mettez à jour les deux schémas d'URL comme indiqué ci-dessus.
	> Veillez à ne pas remplacer les propriétés existantes du fichier `info.plist`.
Si certaines propriétés se chevauchent, vous devez les fusionner manuellement. Pour plus d'informations, consultez la section [Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start) de la documentation Google.

## Initialisation du logiciel SDK client de {{site.data.keyword.amashort}}
{: #google-auth-ios-initialize}

Pour pouvoir utiliser le logiciel SDK client de {{site.data.keyword.amashort}}, vous devez l'initialiser en
passant les paramètres suivants : l'identificateur unique global de l'application (applicationGUID) et la route de l'application (applicationRoute).

> En général, vous pouvez placer le code d'initialisation dans la méthode `application:didFinishLaunchingWithOptions` du délégué de l'application, bien que cet emplacement ne soit pas obligatoire.

1. Ouvrez la page principale du tableau de bord {{site.data.keyword.Bluemix_notm}} et cliquez sur l'appli que vous avez créée.
Le tableau de bord de votre appli de back end mobile s'ouvre.

2. Cliquez sur `Options pour application mobile` dans l'angle supérieur droit du tableau de bord. Les valeurs de *Route de l'application* et d'*Identificateur global unique de l'application* sont affichées.

1. Importez l'infrastructure requise dans la classe qui doit utiliser le SDK client de {{site.data.keyword.amashort}} en ajoutant les en-têtes suivants :

	Applications Objective-C :

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```

	Applications Swift :

	Le SDK client de {{site.data.keyword.amashort}} est implémenté à l'aide d'Objective-C. Il peut donc être nécessaire d'ajouter un en-tête de pontage à votre projet Swift pour pouvoir l'utiliser.

	* Cliquez avec le bouton droit sur votre projet dans Xcode, puis sélectionnez `New File... (Nouveau fichier...)`.
	* Dans la catégorie `iOS Source (Source iOS)`, sélectionnez `Header file (Fichier d'en-tête)`.
	* Nommez-le `BridgingHeader.h`.
	* Ajoutez les importations suivantes à votre en-tête de pontage :

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```
	* Cliquez sur votre projet dans Xcode et sélectionnez l'onglet `Build Settings (Paramètres de génération)`.
	* Recherchez `Objective-C Bridging Header`.
	* Définissez la valeur sur l'emplacement de votre fichier `BridgingHeader.h`, par exemple : `$(SRCROOT)/MyApp/BridgingHeader.h`.
	* Assurez-vous que l'en-tête est prélevée pontage Xcode par bâtiment par votre projet. Vous ne devez voir aucun message d'erreur. 

3. Utilisez le code ci-dessous pour initialiser le SDK client.

	Applications Objective-C :

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	Applications Swift :

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```

	> Remplacez applicationRoute et applicationGUID par les valeurs issues de **Options pour application mobile**.

1. Enregistrez le gestionnaire d'authentification Facebook en ajoutant le code suivant à la méthode `application:didFinishLaunchingWithOptions` dans le délégué de votre appli. Il est recommandé de le faire juste après avoir initialisé l'instance IMFClient.

	Applications Objective-C :

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```

	Applications Swift :

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```

1. Ajoutez le code suivant au délégué de votre appli.

	Applications Objective-C :

	```Objective-C
	- (void)applicationDidBecomeActive:(UIApplication *)application {
		[[IMFGoogleAuthenticationHandler sharedInstance] handleDidBecomeActive];
	}

	- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url
					sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

		BOOL shouldHandleGoogleURL = [GPPURLHandler handleURL:url sourceApplication:sourceApplication annotation:annotation];

		[[IMFGoogleAuthenticationHandler sharedInstance] handleOpenURL:shouldHandleGoogleURL];
		return  shouldHandleGoogleURL;
	}
	```

	Applications Swift :

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		let shouldHandleGoogleURL = GPPURLHandler.handleURL(url,
				sourceApplication: sourceApplication, annotation: annotation)

		IMFGoogleAuthenticationHandler.sharedInstance().handleOpenURL(shouldHandleGoogleURL)

		return shouldHandleGoogleURL;
	}
```

## Test de l'authentification
{: #google-auth-ios-testing}
Lorsque le SDK client est initialisé, vous pouvez commencer à envoyer des demandes à votre système de back end mobile.

### Avant de commencer
{: #google-auth-ios-testing-before}
Vous devez utiliser le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} et disposer au préalable d'une ressource protégée par {{site.data.keyword.amashort}} sur le noeud final `/protected`. Pour configurer un noeud final `/protected`, voir la rubrique [Protection des ressources](protecting-resources.html).


1. Essayez d'envoyer une demande à un noeud final protégé de votre système de back end mobile dans votre navigateur de bureau en ouvrant
`http://{appRoute}/protected`, par exemple `http://my-mobile-backend.mybluemix.net/protected`

1. Le noeud final `/protected` d'un système de back end mobile créé avec le conteneur boilerplate MobileFirst Services est protégé par {{site.data.keyword.amashort}}, par conséquent, seules les applications mobiles instrumentées avec le logiciel SDK client de {{site.data.keyword.amashort}} peuvent y accéder.
Pour cette raison, le message `Unauthorized` s'affiche dans votre navigateur de bureau.

1. A l'aide de votre application iOS, envoyez une demande au même noeud final.

	Objective-C :

	```Objective-C
	NSString *requestPath = [NSString stringWithFormat:@"%@/protected",
								[[IMFClient sharedInstance] backendRoute]];

	IMFResourceRequest *request =  [IMFResourceRequest requestWithPath:requestPath
																method:@"GET"];

	[request sendWithCompletionHandler:^(IMFResponse *response, NSError *error) {
		if (error){
			NSLog(@"Error :: %@", [error description]);
		} else {
			NSLog(@"Response :: %@", [response responseText]);
			NSLog("%@", IMFAuthorizationManager.sharedInstance().userIdentity)
		}
	}];
	```

	Swift :

	```Swift
	let requestPath = IMFClient.sharedInstance().backendRoute + "/protected"

	let request = IMFResourceRequest(path: requestPath, method: "GET");
	request.sendWithCompletionHandler { (response, error) -> Void in
		if (nil != error){
			NSLog("Error :: %@", error.description)
		} else {
			NSLog("Response :: %@", response.responseText)
			NSLog("%@", IMFAuthorizationManager.sharedInstance().userIdentity)
		}
	};

	```

1. Lancez votre application. Un écran de connexion Google s'affiche : 

	![image](images/ios-google-login.png)

	Cet écran peut être légèrement différent si l'appli Facebook n'est pas installée sur votre périphérique, ou si vous n'y êtes pas connecté.

1. Cliquez sur **OK** pour autoriser {{site.data.keyword.amashort}} à utiliser votre ID utilisateur Google pour l'authentification.

1. 	Votre demande doit aboutir. La sortie suivante figure alors dans l'outil LogCat :

	![image](images/ios-google-login-success.png)
