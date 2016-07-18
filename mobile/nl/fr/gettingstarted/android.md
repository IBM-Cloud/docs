---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Mise en route - Exemple Hello Bluemix pour Android
{: #gettingstarted-android}
*Dernière mise à jour : 27 mai 2016*
{: .last-updated}  

Si vous voulez débuter avec une nouvelle application Android, vous pouvez utiliser l'application HelloWorld. Elle explique comment se connecter à votre système de back end {{site.data.keyword.Bluemix}} depuis une application
mobile sans authentification. Le logiciel SDK est déjà installé pour l'application. Une fois prêt, vous pouvez vous procurer les bibliothèques spécifiques que vous voulez utiliser dans
votre application.

1. Créez votre application de back end mobile dans {{site.data.keyword.Bluemix_notm}}.
    1. Dans la section Conteneurs boilerplate du catalogue {{site.data.keyword.Bluemix_notm}}, cliquez sur MobileFirst Services Starter.
    2. Entrez un nom et un hôte pour votre application et cliquez sur **Créer**.
    3. Cliquez sur **Terminer**.
2. Obtenez le projet depuis GitHub. Si vous le souhaitez, vous pouvez utiliser la commande git clone pour obtenir le projet. Depuis votre ordinateur, ouvrez le
terminal, puis entrez la commande suivante :
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld.git
    ```

3. Initialisez le projet en remplaçant &lt;APPLICATION_ROUTE&gt; et &lt;APPLICATION_ID&gt; par la route et l'identificateur global unique de votre application dans le bloc `try` de la fonction `BMSClient.getInstance().initialize()` :
```
// Initialisez le logiciel SDK avec l'ID et la route de l'application IBM Bluemix BMSClient.getInstance().initialize(this, "<APPLICATION_ROUTE>",
"<APPLICATION_ID>");
```
4. Exécutez l'exemple dans votre environnement de développement.
Dans la barre d'outils d'Android Studio, cliquez sur le bouton de lecture et sélectionnez un simulateur.
5. Dans le simulateur, cliquez sur **Ping {{site.data.keyword.Bluemix_notm}}**. L'application exemple envoie une demande Get vers le contexte d'exécution `Node.js` sur {{site.data.keyword.Bluemix_notm}}. Si la demande
aboutit, la connexion est vérifiée et le texte dans le simulateur est mis à jour.

  **Remarque :** le code d'exécution `Node.js` est fourni dans le conteneur boilerplate MobileFirst Services Starter. Si l'application de back end n'a pas été créée avec le conteneur boilerplate MobileFirst Services Starter, elle ne peut pas se connecter.

  Si vous parvenez à vous connecter à {{site.data.keyword.Bluemix_notm}} depuis votre application mobile, le message suivant s'affiche :

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
