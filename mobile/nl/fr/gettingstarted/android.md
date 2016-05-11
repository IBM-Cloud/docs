<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Initiation à l'exemple HelloWorld
{: #gettingstarted-android}
*Dernière mise à jour : 28 janvier 2016*  

Si vous voulez débuter avec une nouvelle application Android, vous pouvez utiliser l'application HelloWorld. Elle explique comment se connecter à votre système de back end {{site.data.keyword.Bluemix}} depuis une application
mobile sans authentification. Le logiciel SDK est déjà installé pour l'application. Une fois prêt, vous pouvez vous procurer les bibliothèques spécifiques que vous voulez utiliser dans
votre application.

1. Créez votre application de back end mobile dans {{site.data.keyword.Bluemix_notm}}.
    1. Dans la section Conteneurs boilerplate du catalogue {{site.data.keyword.Bluemix_notm}}, cliquez sur MobileFirst
Services
Starter.
    2. Entrez un nom et un hôte pour votre application et cliquez sur **Créer**.
    3. Cliquez sur **Terminer**.
2. Obtenez le projet depuis GitHub. Si vous le souhaitez, vous pouvez utiliser la commande git clone pour obtenir le projet. Depuis votre ordinateur, ouvrez le
terminal, puis entrez la commande suivante :
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld.git
```
Avant de commencer, téléchargez le fichier `Gradle.zip` et installez Gradle en procédant à l'extraction du fichier compressé que vous avez téléchargé dans le
répertoire de votre choix. Android Studio peut demander un répertoire de base Gradle (GRADLE HOME) lorsque vous importez l'exemple pour la première fois. Pour ce chemin d'accès, définissez le répertoire bin qui se trouve dans le fichier `Gradle.zip` extrait. Le fichier
`build.gradle` génère automatiquement votre projet en extrayant les dépendances requises.
3. Initialisez le projet.
Pour initialiser le logiciel SDK, remplacez &lt;APPLICATION_ROUTE&gt; et &lt;APPLICATION_ID&gt; par la route et l'identificateur global unique de votre
application dans le bloc try de la fonction `BMSClient.getInstance().initialize()` :
```
// Initialisez le logiciel SDK avec l'ID et la route de l'application IBM Bluemix BMSClient.getInstance().initialize(this, "<APPLICATION_ROUTE>",
"<APPLICATION_ID>");
```{: codeblock}

4. Exécutez l'exemple dans votre environnement de développement.
Dans la barre d'outils d'Android Studio, cliquez sur le bouton de lecture et sélectionnez un simulateur.
Dans le simulateur, cliquez sur **Ping {{site.data.keyword.Bluemix_notm}}**. Le modèle d'application envoie une demande Get à
une ressource protégée dans le contexte d'exécution Node.js dans {{site.data.keyword.Bluemix_notm}}. Si la demande
aboutit, la connexion est vérifiée et le texte dans le simulateur est mis à jour.
<br/>**Remarque :** le code d'exécution Node.js est fourni dans le conteneur boilerplate MobileFirst
Services Starter. Si l'application de back end n'a pas été créée avec le conteneur boilerplate MobileFirst
Services Starter, elle ne peut pas se connecter.<br/>
Lorsque vous parvenez à vous connecter à {{site.data.keyword.Bluemix_notm}} depuis l'application mobile dans Android Studio, le message "Yay! You
are connected" s'affiche :<br/>
![Application Hello World connectée à {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figure 1. Application Hello World connectée à Bluemix")

5. Résolvez les éventuels problèmes.<br/>Si la connexion échoue, le message "Bummer. Something went wrong" s'affiche :</br>
![Application Hello World non connectée à
Bluemix](images/bummer_android.jpg "Figure 2. Application Hello World non connectée à Bluemix")
<br/>
Vérifiez les points suivants :
 * Assurez-vous d'avoir collé correctement les valeurs de route et d'identificateur global unique.
 * Vous pouvez aussi consulter le journal de débogage pour plus d'informations.

## Etapes suivantes :
{: #next}
Pour des informations sur l'obtention du logiciel SDK et son intégration à votre application mobile, voir les informations sur la configuration des
services Bluemix.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# rellinks

## samples
   * [Exemple HelloWorld ](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld)

## sdk
   * [Logiciel SDK de base](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [API Core](https://classicdocs.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
