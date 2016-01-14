# Initiation à l'exemple HelloWorld
{: #gettingstarted-cordova}

Si vous voulez débuter avec une nouvelle application Cordova, vous pouvez utiliser l'application HelloWorld.
Elle explique comment se connecter à votre système de back end Bluemix depuis une application mobile sans authentification.
Le logiciel SDK est déjà installé pour l'application. Une fois prêt, vous pouvez vous procurer les bibliothèques spécifiques que vous voulez utiliser dans
votre application.

1. Créez votre application de back end mobile dans Bluemix.
<ol>
	<li>Dans la section Conteneurs boilerplate du catalogue Bluemix, cliquez sur MobileFirst Services Starter.</li>
    	<li>Entrez un nom et un hôte pour votre application et cliquez sur **Créer**.</li>
    	<li>Cliquez sur **Terminer**. </li>
</ol>
2. Obtenez le projet depuis GitHub. Si vous le souhaitez, vous pouvez utiliser la commande git clone pour obtenir le projet. Depuis votre ordinateur, ouvrez le
terminal, puis entrez la commande suivante :
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-Cordova-helloworld.git
```
Avant de commencer, téléchargez le fichier Gradle.zip et installez Gradle en procédant à l'extraction du fichier compressé que vous avez téléchargé dans le
répertoire de votre choix. Android Studio peut demander un répertoire de base Gradle (GRADLE HOME) lorsque vous importez l'exemple pour la première fois.
Pour ce chemin d'accès, définissez le répertoire bin qui se trouve dans le fichier Gradle.zip extrait. Le fichier build.gradle génère automatiquement votre
projet en extrayant les dépendances requises.


3. Initialisez le projet.
Pour initialiser le logiciel SDK, remplacez &lt;APPLICATION_ROUTE&gt; et &lt;APPLICATION_ID&gt; par la route et l'identificateur global unique de votre
application dans le bloc try de la fonction BMSClient.getInstance().initialize() :
```
// Initialisez le logiciel SDK avec l'ID et la route de l'application IBM Bluemix BMSClient.getInstance().initialize(this, "<APPLICATION_ROUTE>",
"<APPLICATION_ID>");
```
4. Exécutez l'exemple dans votre environnement de développement.
Dans la barre d'outils d'Android Studio, cliquez sur le bouton de lecture et sélectionnez un simulateur.
Dans le simulateur, cliquez sur **Ping Bluemix**. Le modèle d'application envoie une demande Get à une ressource protégée dans le
contexte d'exécution Node.js dans Bluemix. Si la demande
aboutit, la connexion est vérifiée et le texte dans le simulateur est mis à jour.
Remarque : le code d'exécution Node.js est fourni dans le conteneur boilerplate MobileFirst Services Starter. Si l'application de back end n'a pas été
créée avec le conteneur boilerplate MobileFirst Services Starter, elle ne peut pas se connecter.



![Application Hello World
connectée à Bluemix](images/yayconnected.jpg "Figure 1. Application Hello World connectée à Bluemix")

Lorsque vous parvenez à vous connecter à Bluemix depuis l'application mobile dans Android Studio, le message "Yay! You are connected" s'affiche.
5. Corrigez les problèmes éventuels.

![Application Hello World non connectée à
Bluemix](images/bummer_android.jpg "Figure 2. Application Hello World non connectée à Bluemix")

Si la connexion échoue, le message "Bummer Something went wrong" s'affiche. Des informations supplémentaires sur l'erreur sont incluses. Vérifiez les points suivants :
 * Assurez-vous d'avoir collé correctement les valeurs de route et d'identificateur global unique.
 * Vous pouvez aussi consulter le journal de débogage pour plus d'informations.

## Etapes suivantes :
{: #next}
Pour des informations sur l'obtention du logiciel SDK et son intégration à votre application mobile, voir Configuration du logiciel SDK du client Android. 
