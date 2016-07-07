---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Mise en route - Exemple Hello Bluemix pour iOS
{: #gettingstarted-android}
*Dernière mise à jour : 1er juin 2016*
{: .last-updated}  

Si vous voulez débuter avec une nouvelle application iOS, vous pouvez utiliser l'application HelloWorld. Elle explique comment se connecter à votre système de back end {{site.data.keyword.Bluemix}} depuis une application
mobile sans authentification. Le logiciel SDK est déjà installé pour l'application. Une fois prêt, vous pouvez vous procurer les bibliothèques spécifiques que vous voulez utiliser dans
votre application.

1. Créez votre application de back end mobile dans {{site.data.keyword.Bluemix_notm}}.
    1. Dans la section Conteneurs boilerplate du catalogue {{site.data.keyword.Bluemix_notm}}, cliquez sur MobileFirst Services Starter.
    2. Entrez un nom et un hôte pour votre application et cliquez sur **Créer**.
    3. Cliquez sur **Terminer**.
2. Obtenez le projet depuis GitHub. Si vous le souhaitez, vous pouvez utiliser la commande git clone pour obtenir le projet. Depuis votre ordinateur, ouvrez le
terminal, puis entrez la commande suivante :
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld.git
    ```

3. Initialisez le projet. Pour initialiser le logiciel SDK, copiez le code suivant dans la méthode `didFinishLaunchingWithOptions` du délégué de l'application :

	###Objective-C
	{: initializeobjc}

	**Important** : alors que le SDK Objective-C reste complètement pris en charge et est toujours considéré comme le SDK principal pour {{site.data.keyword.Bluemix}} Mobile Services,  il est prévu qu'il soit interrompu plus tard dans l'année et remplacé par le nouveau SDK Swift.

	Le SDK Objective-C rapporte les données de surveillance à la console de surveillance du service {{site.data.keyword.amashort}}. Si vous dépendez des fonctions de surveillance du service {{site.data.keyword.amashort}}, continuez à utiliser le SDK Objective-C.

	```
	// Initialisez le logiciel SDK avec l'ID et la route de l'application IBM Bluemix
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
	```

	###Swift
	{: initializeswift}
	```
	// Initialisez le logiciel SDK avec l'ID et la route de l'application IBM Bluemix
IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
return true
	```

4. Exécutez l'exemple dans votre environnement de développement. Dans Xcode, cliquez sur **Product&gt;Run**. Un simulateur iOS démarre.
5. Dans le simulateur, cliquez sur **Ping {{site.data.keyword.Bluemix_notm}}**. Le modèle d'application obtient l'en-tête
d'autorisation depuis le service Mobile Client Access. Si la commande ping aboutit, le texte
dans le simulateur est mis à jour.

  Si vous parvenez à vous connecter à {{site.data.keyword.Bluemix_notm}} depuis l'application mobile dans Xcode, le message suivant s'affiche :

  `Yay! You are connected`
  {: screen}

  ![Application Hello World
connectée{{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figure 1. Application Hello World connectée à  Bluemix")

  Si la connexion échoue, le message suivant s'affiche : `Bummer. Something went wrong`
  {: screen}

  ![Application Hello World non connectée à
Bluemix](images/bummer_android.jpg "Figure 2. Application Hello World non connectée à Bluemix")

	Vous pouvez résoudre le problème de connexion en procédant comme suit :
	* Assurez-vous d'avoir collé correctement les valeurs de route et d'identificateur global unique.
		####Objective-C
		{: #objcvals}
		```
		[imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
  backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
		```

		####Swift
		{: #swiftvals}
		```
		IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")
		```

	* Consultez le journal de débogage pour plus d'informations.


## Etapes suivantes :
{: #next}
Pour des informations sur l'obtention du logiciel SDK et son intégration à votre application mobile, voir les informations sur la configuration des
services Bluemix.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# rellinks

## samples
   * [Exemple Hello Bluemix](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld)

## sdk
   * [Logiciel SDK de base](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [API Core](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
