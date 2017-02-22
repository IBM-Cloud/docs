---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Mise en route - Exemple Hello Bluemix pour iOS
{: #gettingstarted-android}
Dernière mise à jour : 1er juin 2016
{: .last-updated}  

Si vous voulez débuter avec une nouvelle application iOS, vous pouvez utiliser l'application Hello Bluemix. Elle explique comment se connecter à votre système de back end {{site.data.keyword.Bluemix}} depuis une application
mobile sans authentification. Une fois prêt, vous pouvez vous procurer les bibliothèques spécifiques que vous voulez utiliser dans votre application.

1. Créez votre application de back end mobile dans {{site.data.keyword.Bluemix_notm}}.
    1. Dans la section Conteneurs boilerplate du catalogue {{site.data.keyword.Bluemix_notm}}, cliquez sur MobileFirst Services Starter.
    2. Entrez un nom et un hôte pour votre application et cliquez sur **Créer**.
    3. Cliquez sur **Terminer**.
2. Exécutez l'application exemple Hello Bluemix :
	1. Obtenez le projet depuis GitHub. Si vous le souhaitez, vous pouvez utiliser la commande git clone pour obtenir le projet. Depuis votre ordinateur, ouvrez le terminal, puis entrez la commande suivante :
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix.git
    ```
	2. Exécutez la commande `pod install` depuis le répertoire `bms-samples-swift-hellobluemix`, où le projet a été cloné. Si Cocoapods n'est pas installé, obtenez le depuis [https://cocoapods.org](https://cocoapods.org).
	3. Ouvrez l'espace de travail Xcode avec la commande `open HelloBluemix.xcworkspace`.
	4. Dans votre fichier `AppDelegate.swift`, mettez à jour les valeurs appRoute et appGuid en utilisant les valeurs obtenues depuis le backend Bluemix que vous avez créé précédemment.

3. Exécutez l'exemple dans votre environnement de développement. Dans Xcode, cliquez sur **Product&gt;Run**. Un simulateur iOS démarre.

	**Important :** votre valeur appRoute doit utiliser un protocole `https` et non`http`, ou vous risquez d'avoir un échec de connexion, dû aux paramètres de sécurité du transport d'appplications. Vous pouvez en savoir plus sur ces paramètres en consultant l'article de blogue [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/) blog post.
	
4. Dans le simulateur, cliquez sur **Ping {{site.data.keyword.Bluemix_notm}}**. Le modèle d'application obtient l'en-tête d'autorisation depuis le service Mobile Client Access. Si la commande ping aboutit, le texte dans le simulateur est mis à jour.

  Quand vous vous connectez à {{site.data.keyword.Bluemix_notm}} depuis l'application mobile dans Xcode, le message suivant s'affiche : `Yay! You are connected`
  {: screen}

  <!--
  ![Hello World application successfully connected to {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figure 1. Hello World application successfully connected to Bluemix")
-->

  Si la connexion échoue, le message suivant s'affiche : `Bummer. Something went wrong`
  {: screen}

 <!--
  ![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")
  -->

	Vous pouvez résoudre le problème de connexion en procédant comme suit :
	* Assurez-vous d'avoir collé correctement les valeurs de route et d'identificateur global unique.
	* Consultez le journal de débogage pour plus d'informations.


## Etapes suivantes :
{: #next}
Pour des informations sur l'obtention du logiciel SDK et son intégration à votre application mobile, voir les informations sur la configuration des services Bluemix.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# rellinks

## samples
   * [Exemple Hello Bluemix (iOS)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix)

## sdk
   * [Logiciel SDK de base](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [API Core](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
