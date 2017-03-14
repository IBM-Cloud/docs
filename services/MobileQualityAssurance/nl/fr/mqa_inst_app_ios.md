---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Instrumentation de MQA avec une application iOS (obsolète)
{: #instrumentios}

Si vous souhaitez utiliser {{site.data.keyword.mqafull}} avec votre application iOS, vous devez télécharger le logiciel SDK et l'instrumenter en effectuant quelques modifications à l'aide de l'environnement de développement Xcode.
{: shortdesc}

Pour pouvoir instrumenter une application avec {{site.data.keyword.mqa}}, vous devez disposer d'un compte {{site.data.keyword.Bluemix}} et avoir installé la version de l'environnement de développement adaptée aux plateformes de l'application que vous instrumentez.

Pour instrumenter {{site.data.keyword.mqa}} en vue de son exécution avec votre application Objective-C ou Swift, procédez comme suit :

1. Ajoutez les droits requis et téléchargez le logiciel SDK dans votre projet iOS.

	1. Créez ou ouvrez votre projet dans Xcode.

	2. Ajoutez les bibliothèque des dépendances suivantes en sélectionnant `+` dans la section *Linked Frameworks and Libraries* de l'onglet *General* du projet Xcode :

		* AssetsLibrary.framework
		* AudioToolbox.framework
		* AVFoundation.framework
		* CoreData.framework
		* CoreLocation.framework
		* CoreMedia.framework
		* CoreMotion.framework
		* CoreTelephony.framework
		* CoreText.framework
		* CoreVideo.framework
		* MediaPlayer.framework
		* QuartzCore.framework
		* Security.framework
		* SystemConfiguration.framework

	3. Faites glisser le dossier `Q4M.framework` du logiciel SDK {{site.data.keyword.mqa}} pour iOS dans le groupe **Frameworks** de l'arborescence du navigateur. Dans la fenêtre Choose options, sélectionnez *Copy items if needed*, **Create groups**, et cochez la case correspondant au nom de votre projet comme cible.

	4. Dans la section Linking de l'onglet *Build Settings*, définissez les indicateurs *Other Linker flags* pour le débogage et la publication (Debug et Release) sur **-ObjC**. Important : Veillez à sélectionner l'onglet *All* de telle sorte que les indicateurs Other Linker soient inclus dans la liste.

	5. *Pour Objective-C uniquement :* ajoutez l'instruction d'importation suivante dans les fichiers `AppDelegate.m` et `ViewController.m` :

		```
		#import <Q4M/MQALogger.h>
		```
		{: codeblock}

	6. *Pour Swift uniquement :* ajoutez un en-tête de pontage Objective-C pour le logiciel SDK {{site.data.keyword.mqa}} pour iOS en procédant comme suit :

		1. Cliquez à l'aide du bouton droit de la souris sur le noeud racine du projet et sélectionnez **New File**.

		2. Dans la fenêtre Choose Template, sous iOS, cliquez sur le modèle Header File dans la section Source.

		3. Nommez le fichier `MonProjet-Bridging-Header.h`, où *MonProjet* est le nom de votre projet Swift, et sélectionnez le nom de votre projet comme cible. Par exemple, nommez le fichier `MonProjet-Bridging-Header.h`.

		4. Cliquez sur **Create** pour sauvegarder le fichier à la racine de votre projet.

		5. Dans le nouveau fichier d'en-tête de pontage, ajoutez l'instruction d'importation suivante :

			```
			#import <Q4M/MQALogger.h>
			```
			{: codeblock}

		6. Sélectionnez votre projet dans le navigateurs de projets Xcode, puis cliquez sur **Build Settings** et recherchez `Objective-C Bridging Header`.

		7. Sous **Swift Compiler - General**, définissez la valeur de **Objective-C Bridging Header** sur le chemin de l'en-tête de pontage. Le chemin est relatif par rapport à la racine de votre projet. Par exemple, si le projet MQASampleApp se trouve dans `/user/example/MQASampleApp`, le chemin est `/user/example/MQASampleApp/MQASampleApp-Bridging-Header.h`. Si vous avez sauvegardé votre fichier à la racine du projet, vous pouvez utiliser une variable d'environnement pour définir le chemin en indiquant `${SRCROOT}/${PROJECT}-Bridging-Header.h`.

		8. Sauvegardez et générez l'application pour vérifier que le chemin est correct.

	7. Dans le fichier `info.plist`, vérifiez les paramètres suivants dans les informations du projet :

		* Bundle version - {{site.data.keyword.mqa}} utilise la valeur de cette zone pour savoir quand envoyer une notification de nouvelle génération aux testeurs. Lorsque vous transférez une nouvelle génération vers {{site.data.keyword.mqa}}, veillez à incrémenter ce nombre. La chaîne de la zone Bundle version ne peut contenir que des chiffres et le caractère point (.). Cette restriction étant une exigence Xcode, la plupart des applications respectent cette convention et ne requièrent pas de modification.
		* Bundle versions string - Cette zone contient une représentation sous forme de chaîne de votre numéro de version. La chaîne n'est pas soumise aux mêmes restrictions que la zone Bundle version.

2. Configurez une nouvelle session à lancer à chaque connexion.

    1. Repérez la méthode `didFinishLaunchingWithOptions` dans le fichier `AppDelegate` :

        * Objective-C : fichier `AppDelegate.m`
        * Swift : fichier `AppDelegate.swift`

	2. Démarrez la session {{site.data.keyword.mqa}}.

		* Objective-C

			1. Démarrez la nouvelle session dans une méthode au sein de votre méthode `applicationDelegate`, comme la méthode `didFinishLaunchingWithOptions`. Vous trouverez votre délégué en ouvrant le dossier du même nom que votre projet dans le navigateur de projet. Recherchez le fichier `projectDelegate.m`.

			2. Ajoutez le code suivant dans la méthode `didFinishLaunchingWithOptions` avant la ligne indiquant `return YES;` :

				```
				// Starts a quality assurance session using a
				    placeholder key and QA mode
				[MQALogger startNewSessionWithApplicationKey:@"Clé_Votre_Application"];
				```
				{: codeblock}

			3. Remplacez la variable *Clé_Votre_Application* par votre clé d'application de {{site.data.keyword.mqa}}.
               Astuce : Vous trouverez votre clé d'application dans le panneau Web {{site.data.keyword.mqa}} sous App Settings.

		* Swift

			1. Repérez la méthode `didFinishLaunchingWithOptions` dans le fichier `AppDelegate.swift`.

			2. Ajoutez le code suivant dans la méthode avant la ligne indiquant `return true`, où *Clé_Votre_Application* est une clé valide de votre application :

				```
				// Set the application key
				MQALogger.startNewSession(withApplicationKey: "Clé_Votre_Application")
				```
				{: codeblock}

	3. Indiquez si vous souhaitez utiliser le mode préproduction ou le mode production. Pour plus d'informations sur les différences entre le mode préproduction et le mode production, voir [Differences between preproduction and production modes ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/cPreprodvsProd.html){: new_window} dans l'IBM Knowledge Center.

		* Objective-C

			1. Repérez la méthode `didFinishLaunchingWithOptions`.

			2. Ajoutez une des lignes de code suivantes dans la méthode didFinishLaunchingWithOptions avant la ligne indiquant `return YES;` :

			Pour utiliser le mode préproduction, ajoutez cette ligne de code :

				```
				[[MQALogger settings] setMode:MQAModeQA];
				```
				{: codeblock}

			Pour utiliser le mode production, ajoutez cette ligne de code :

				```
				[[MQALogger settings] setMode:MQAModeMarket];
				```
				{: codeblock}

				**Exemple complet Objective-C**
				<pre><code>
					- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
						{
					   // Override point for customization after application launch.
					   if ([[UIDevice currentDevice] userInterfaceIdiom] == UIUserInterfaceIdiomPad) {
					      UISplitViewController *splitViewController = (UISplitViewController*)self.window.rootViewController;
					      UINavigationController *navigationController = [splitViewController.viewControllers lastObject];
					      splitViewController.delegate = (id)navigationController.topViewController;
						}
					     #ifdef Debug
					   [[MQALogger settings] setMode:MQAModeQA];
					   #else
					   [[MQALogger settings] setMode:MQAModeMarket];
					   #endif
					      // Starts a quality assurance session using a placeholder key
					      [MQALogger startNewSessionWithApplicationKey:@"Your-Application-Key"];
					      // Enables the quality assurance application crash reporting
					      NSSetUncaughtExceptionHandler(&MQAUncaughtExceptionHandler);
					      return YES; }
				</code></pre>
				{: codeblock}

        * Swift

			1. Dans le fichier AppDelegate.swift, recherchez la méthode `didFinishLaunchingWithOptions`.

			2. Ajoutez les lignes suivantes dans votre méthode `didFinishLaunchingWithOptions` avant la ligne indiquant `return true` :

				```
				//Set the SDK mode Market vs QA for Production
				   and Pre-Production
				#if Debug
				  MQALogger.settings().mode = MQAMode.QA
				#elseif Release
				  MQALogger.settings().mode = MQAMode.Market
				#endif
				```
				{: codeblock}

			Voici un exemple de code :

				```
				func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

				//Set the SDK mode Market vs QA for Production
				   and Pre-Production
				#if Debug
					MQALogger.settings().mode = MQAMode.QA
				#elseif Release
					MQALogger.settings().mode = MQAMode.Market
				#endif

				// Set the application key
				MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")

				// Override point for customization after
				   application launch.
				return true
				```
				{: codeblock}

				**Exemple complet Swift**
				<pre><code>				
				func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions:[NSObject: AnyObject]?) -> Bool {
					// Override point for customization after application launch.
					//Set the Shake Device option to true or false. If this is not explicitly set, the Shake Device is enabled by default.
					MQALogger.settings().reportOnShakeEnabled = true
					//Set the SDK mode Market vs QA for Production and Pre-Production
					#if Debug
					MQALogger.settings().mode = MQAMode.QA
					#elseif Release
					MQALogger.settings().mode = MQAMode.Market
					#endif

				//Start the MQA session with the specified app key
					   MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
				// Enables MQA crash reporting to catch uncaught exceptions
					   NSSetUncaughtExceptionHandler(exceptionHandlerPointer);

					   return true
					}
				</code></pre>
				{: codeblock}

3. Exécutez votre application afin de vérifier que {{site.data.keyword.mqa}} démarre au lancement de l'application.

4. Poursuivez en procédant comme indiqué dans [Initiation à {{site.data.keyword.mqa}}](index.html).

# Liens connexes
{: #rellinks notoc}

## Liens connexes
{: #general notoc}
* [Initiation à {{site.data.keyword.mqa}}](index.html){:new_window}
