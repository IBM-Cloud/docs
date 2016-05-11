<!-- Attribute definitions -->
{:codeblock: .codeblock}
{:screen: .screen}

# Initiation à l'exemple HelloWorld
{: #gettingstarted-ios}
*Dernière mise à jour : 28 janvier 2016*
Si vous voulez débuter avec une nouvelle application iOS, vous pouvez utiliser l'application HelloWorld. Elle explique comment se connecter à votre système de back end {{site.data.keyword.Bluemix}} depuis une application
mobile sans authentification. Le logiciel SDK est déjà installé pour l'application. Une fois prêt, vous pouvez vous procurer les bibliothèques spécifiques que vous voulez utiliser dans
votre application.

1. Créez votre application de back end mobile dans {{site.data.keyword.Bluemix_notm}}.
<ol>
	<li>Dans la section Conteneurs boilerplate du catalogue {{site.data.keyword.Bluemix_notm}}, cliquez sur **MobileFirst Services
Starter**.</li>
    <li>Entrez un nom et un hôte pour votre application et cliquez sur **Créer**.</li>
    <li>Cliquez sur **Terminer**. </li>
</ol>
2. Obtenez le projet depuis GitHub.
Depuis votre ordinateur, ouvrez le terminal, puis entrez la commande suivante :
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld
```

3. Initialisez le projet.
Pour initialiser le logiciel SDK, copiez le code suivant dans la méthode `didFinishLaunchingWithOptions` du délégué de l'application :
   * Objective-C :
```
// Initialisez le logiciel SDK avec l'ID et la route de l'application IBM Bluemix
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
```{: codeblock}
   * Swift :
```
// Initialisez le logiciel SDK avec l'ID et la route de l'application IBM Bluemix
IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
return true
```{: codeblock}

4. Exécutez l'exemple dans votre environnement de développement.
Dans Xcode, cliquez sur **Product&gt;Run**. Un simulateur iOS démarre.
Dans le simulateur, cliquez sur **Ping {{site.data.keyword.Bluemix_notm}}**. Le modèle d'application obtient l'en-tête
d'autorisation depuis le service Mobile Client Access. Si la commande ping aboutit, le texte
dans le simulateur est mis à jour.
<br/>Lorsque vous parvenez à vous connecter à {{site.data.keyword.Bluemix_notm}} depuis l'application mobile dans Xcode, le message "Yay! You
are connected" s'affiche :<br/>
![Application Hello
World connectée à {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figure 1. Application Hello World connectée à {{site.data.keyword.Bluemix_notm}}") <br/>
Si la connexion aboutit, le Xcode de connexion pour le débogage contient le message suivant :
```You have connected to {{site.data.keyword.Bluemix_notm}} successfully```
5. Corrigez les problèmes éventuels.
Si la connexion échoue, le message "Bummer Something went wrong" s'affiche. Des informations supplémentaires sur l'erreur sont incluses.<br/>
![Application Hello World non connectée à {{site.data.keyword.Bluemix_notm}}](images/bummer_android.jpg "Figure 2. Application Hello World non connectée à Bluemix")
<br/>Assurez-vous d'avoir collé correctement les valeurs de route et d'identificateur global unique :
   * Objective-C :
  ```
  [imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
  backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
  ``` {: codeblock}
   * Swift :
  ```
  IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")
  ```{: codeblock}


Vous pouvez aussi consulter le journal de débogage pour plus d'informations.

## Etapes suivantes :
{: #next}
Pour des informations sur l'obtention du logiciel SDK et son intégration à votre application mobile, voir les informations sur la configuration des
services {{site.data.keyword.Bluemix}}.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# rellinks

## samples
   * [Exemple HelloWorld ](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld)

## sdk
   * [Logiciel SDK de base](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-ios-core)

## api
   *
[API Core](https://classicdocs.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)
