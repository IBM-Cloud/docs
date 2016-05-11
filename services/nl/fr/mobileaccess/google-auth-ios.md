---

Copyright : 2015, 2016

---

# Activation de l'authentification Google dans les applis iOS
{: #google-auth-ios}

**Astuce :** Si vous développez votre application iOS dans Swift, vous pouvez envisager d'utiliser le SDK Swift client de {{site.data.keyword.amashort}}. Les instructions de cette page s'appliquent au SDK client Objective-C de {{site.data.keyword.amashort}}. Pour les instructions d'utilisation du SDK Swift, voir [Activation de l'authentification Google dans les applications iOS (SDK Swift)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)

## Avant de commencer
{: #google-auth-ios-before}
* Vous devez disposer d'une ressource protégée par {{site.data.keyword.amashort}} et d'un projet iOS instrumenté avec le SDK client de {{site.data.keyword.amashort}}.  Pour plus d'informations, voir [Initiation à {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) et [Configuration du SDK Objective-C d'iOS](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html).  
* Protégez manuellement votre application de back end avec le SDK serveur de {{site.data.keyword.amashort}}. Pour plus d'informations, voir [Protection des ressources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


## Configuration d'un projet Google pour la plateforme iOS
{: #google-auth-ios-project}
Pour commencer à utiliser Google en tant que fournisseur d'identité, vous devez créer un projet dans Google Developer Console pour obtenir un ID client Google.  Cet ID client est un identificateur unique qui permet à Google de savoir quelle application tente de se connecter.   Si vous avez déjà un projet Google, vous pouvez passer les étapes qui décrivent la création du projet et commencer par l'ajout des droits d'accès.



1. Créez un projet dans [Google Developer Console](https://console.developers.google.com).
Si vous avez déjà un projet, vous pouvez passer les étapes qui décrivent la création du projet et commencer par l'ajout des droits d'accès.
   1.    Ouvrez le menu de nouveau projet. 
         
         ![image](images/FindProject.jpg)

   2.    Cliquez sur **Créer un projet**.
   
         ![image](images/CreateAProject.jpg)


1. Dans la liste **Social APIs**, sélectionnez **Google+ API**.

     ![image](images/chooseGooglePlus.jpg)

1. Cliquez sur **Enable** dans l'écran suivant.

1. Sélectionnez l'onglet **Consent Screen** et indiquez le nom de produit affiché aux utilisateurs. les autres valeurs sont facultatives. Cliquez sur **Sauvegarder**.

    ![image](images/consentScreen.png)
    
1. Dans la liste **Credentials**, sélectionnez OAuth client ID.

     ![image](images/chooseCredentials.png)
     


1. Puis, vous serez invité à choisir un type d'application. Sélectionnez **iOS**.

1. Donnez un nom parlant à votre client iOS. Spécifiez l'ID de bundle de votre application iOS. Pour le trouver, recherchez la valeur de **Bundle Identifier (ID de bundle)** dans le fichier `info.plist` ou dans l'onglet **General** du projet Xcode.

1. Notez l'ID de votre nouveau client iOS. Vous aurez besoin de cette valeur lors de la configuration de l'application dans {{site.data.keyword.Bluemix}}.


## Configuration de {{site.data.keyword.amashort}} pour l'authentification Google
{: #google-auth-ios-config}

Maintenant que vous disposez d'un ID client iOS, vous pouvez activer l'authentification Google dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.

1. Ouvrez votre appli dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.

1. Cliquez sur **Options pour application mobile** et notez la valeur de **Route** (`applicationRoute`)
et **Identificateur global unique de l'application** (`applicationGUID`). Vous aurez besoin de ces valeurs lors de l'initialisation du SDK.

1. Cliquez sur la vignette {{site.data.keyword.amashort}}. Le tableau de bord {{site.data.keyword.amashort}} se charge.

1. Cliquez sur la vignette **Google** .

1. Dans **ID application pour iOS**, indiquez votre ID client iOS pour Android et cliquez sur **Sauvegarder**.

	Remarque : en plus de l'ID client Google, la valeur inverse est également requise pour votre configuration client (voir ci-dessous). Pour accéder aux deux
valeurs, téléchargez le fichier d'exemple plist en cliquant sur l'icône en forme de crayon :
		![téléchargement du fichier info.plist](images/download_plist.png)

## Configuration du SDK client de {{site.data.keyword.amashort}} pour iOS
{: #google-auth-ios-sdk}

### Installation du SDK client de {{site.data.keyword.amashort}} à l'aide de CocoaPods
{: #google-auth-ios-sdk-cocoapods}

1. Accédez à votre projet iOS.

1. Modifiez le fichier `Podfile` en lui ajoutant la ligne suivante :

	```
	pod 'IMFGoogleAuthentication'
	```

1. Enregistrez le `Podfile` et lancez `pod install` depuis la ligne de commande. CocoaPods installe les dépendances. La progression et les composants ajoutés s'affichent.

  **Important** : Vous devez à présent ouvrir votre projet en utilisant le fichier `xcworkspace` généré par CocoaPods. Son nom est généralement `{your-project-name}.xcworkspace`.  

1. Exécutez `open {nom_projet}.xcworkspace` depuis la ligne de commande pour ouvrir votre espace de travail de projet iOS.

### Configuration d'un projet iOS pour l'authentification Google
{: #google-auth-ios-googleauth}
Configurez l'intégration Google en mettant à jour le fichier `info.plist`. Le fichier `info.plist` est généralement situé dans
le dossier `Supporting files` de votre projet Xcode. Vous pouvez éditer ce fichier à l'aide de l'éditeur de liste de propriétés ou d'un éditeur de
texte.

* Configurez l'intégration Google en ajoutant les schémas d'URL suivants à votre fichier
`info.plist`.
	![Fichier info.plist](images/ios-google-infoplist-settings.png)

	Le premier schéma d'URL est une version inversée de l'ID client dans Google Developer Console.  Par exemple, si votre ID client est
`123123-abcabc.apps.googleusercontent.com`, votre schéma d'URL sera : `com.googleusercontent.apps.123123-abcabc`. 

	Le second schéma d'URL est l'ID de bundle de votre application.

* Utilisez un éditeur de texte. Cliquez avec le bouton droit sur le fichier `info.plist` et sélectionnez **Ouvrir en tant que >
Code source**. Ajoutez le code XML suivant au fichier :

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
	Mettez à jour les deux schémas d'URL.

	**Important** : Ne modifiez pas les propriétés existantes dans le fichier `info.plist`. Si certaines propriétés se
chevauchent, vous devrez les fusionner manuellement. Pour plus d'informations, voir [Try Sign-In
for iOS](https://developers.google.com/identity/sign-in/ios/start).

## Initialisation du logiciel SDK client de {{site.data.keyword.amashort}}
{: #google-auth-ios-initialize}

Pour utiliser le SDK client de {{site.data.keyword.amashort}}, initialisez-le en lui transmettant les paramètres applicationGUID et applicationRoute.

En général, vous pouvez placer le code d'initialisation dans la méthode `application:didFinishLaunchingWithOptions` du délégué de l'application, bien que cet emplacement ne soit pas obligatoire.

1. Identifiez les valeurs de applicationGUID et applicationRoute. Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur votre
application. Cliquez sur **Options pour application mobile**. Les valeurs de *Route de l'application* et d'*Identificateur global unique de l'application* sont affichées.

1. Importez les structures requises dans la classe où vous comptez utiliser le SDK client {{site.data.keyword.amashort}}. Ajoutez les en-têtes
suivants :

	Objective-C :

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```

	Swift :

	Le SDK client de {{site.data.keyword.amashort}} est implémenté avec Objective-C. Il peut être nécessaire d'ajouter un en-tête de pontage à votre projet Swift pour utiliser le logiciel SDK.

	1. Cliquez avec le bouton droit sur votre projet dans Xcode, puis sélectionnez **New File... (Nouveau fichier...)**.
	2. Dans la catégorie **iOS Source (Source iOS)**, sélectionnez **Header file (Fichier d'en-tête)**.
	3. Nommez-le `BridgingHeader.h`.
	4. Ajoutez les importations suivantes votre en-tête de pontage :

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```
	5. Cliquez sur votre projet dans Xcode et sélectionnez l'onglet **Build Settings (Paramètres de génération)**.
	6. Recherchez `Objective-C Bridging Header`.
	7. Attribuez-lui comme valeur l'emplacement de votre fichier `BridgingHeader.h`. Par exemple :
`$(SRCROOT)/MyApp/BridgingHeader.h`.
	8. Vérifiez que l'en-tête de pontage est prélevé par Xcode lors de la génération de votre projet.

3. Utilisez le code suivant pour initialiser le SDK client.  Remplacez *applicationRoute* et *applicationGUID* par les valeurs de
**Route** et **Identificateur global unique de l'application** de la section **Options pour application mobile**.

	Objective-C :

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	Swift :

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```



1. Enregistrez le gestionnaire d'authentification en ajoutant le code suivant à la méthode `application:didFinishLaunchingWithOptions`
dans votre délégué d'application. Ajoutez ce code immédiatement après l'initialisation d'IMFClient :

	Objective-C :

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```

	Swift :

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```

1. Ajoutez le code suivant au délégué de votre appli.

	Objective-C :

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

	Swift :

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
Vous devez utiliser le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} et disposer au préalable d'une ressource protégée par {{site.data.keyword.amashort}} sur le noeud final `/protected`. Pour configurer un noeud final `/protected`, voir la rubrique [Protection des ressources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Essayez d'envoyer une demande à un noeud final protégé de votre back end mobile dans votre navigateur de bureau en ouvrant
`{applicationRoute}/protected`, par exemple : `http://my-mobile-backend.mybluemix.net/protected`

1. Le noeud final `/protected` d'un système de back end mobile créé avec le conteneur boilerplate MobileFirst Services est protégé par {{site.data.keyword.amashort}}, par conséquent, seules les applications mobiles instrumentées avec le logiciel SDK client de {{site.data.keyword.amashort}} peuvent y accéder. Pour cette raison, le message `Unauthorized` s'affiche dans votre navigateur de bureau.

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
			NSLog(@"%@", [[IMFAuthorizationManager sharedInstance] userIdentity]);
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
	
	
	Vous pouvez également ajouter une fonctionnalité de déconnexion en ajoutant le code suivant :
	
	Objective C:
	
	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] logout : callBack]
	```

	Swift :

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().logout(callBack)
	```


	Si vous appelez ce code alors que l'utilisateur était connecté via Google et qu'il tente à nouveau de se connecter, il est invité à autoriser
Mobile Client Access à utiliser Google aux fins d'authentification. A ce stade, l'utilisateur peut cliquer sur un nom d'utilisateur à l'angle supérieur droit de
l'écran pour sélectionner et se connecter sous un autre nom d'utilisateur.

	La transmission de `callBack` à la fonction de déconnexion est facultative. Vous pouvez également transmettre la valeur
`nil`.
