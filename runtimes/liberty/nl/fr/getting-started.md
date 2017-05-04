---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Initiation à Liberty sur Bluemix

* {: download} Félicitations, vous avez déployé une application exemple Hello World sur {{site.data.keyword.Bluemix}} !  Pour commencer, suivez ce guide pas à pas. Ou <a class="xref" href="http://bluemix.net" target="_blank" title="(Télécharger l'exemple de code)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Télécharger le code de l'application" />téléchargez l'exemple de code</a> et découvrez-le par vous-même.

En suivant ce guide, vous allez mettre en place un environnement de développement, déployer une application à la fois localement et sur {{site.data.keyword.Bluemix}}, puis intégrer un service de base de données {{site.data.keyword.Bluemix}} dans votre application.

## Prérequis 
{: #prereqs}

Vous aurez besoin des comptes et outils suivants :
* [Compte {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI (client de ligne de commande pour Cloud Foundry) ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Eclipse IDE for Java EE Developers ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}
* [Git ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://git-scm.com/downloads){: new_window}
* [Maven ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://maven.apache.org/download.cgi){: new_window}

Pour développer dans Eclipse avec {{site.data.keyword.eclipsetoolsfull}}, vous aurez aussi besoin de [télécharger les outils. ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix){: new_window}

## 1. Clonez l'application exemple
{: #clone}

Commencez par cloner le référentiel GitHub contenant l'application exemple.
  ```bash
git clone https://github.com/IBM-Bluemix/get-started-java
  ```
  {: pre}


## 2. Lancez l'application localement en utilisant la ligne de commande
{: #run_locally}

Utilisez Maven pour construire votre code source et exécuter l'application résultante.

1. Sur la ligne de commande, placez-vous dans le répertoire où se trouve l'application exemple.

  ```
cd get-started-java
  ```
  {: pre}

1. Utilisez Maven pour installer les dépendances et construire le fichier .war.

  ```
mvn clean install
  ```
  {: pre}

1. Exécutez l'application localement sur Liberty. 
  ```
mvn install liberty:run-server
  ```
  {: pre}

Lorsque vous voyez le message *Le serveur defaultServer est prêt pour une planète plus intelligente*, visualisez votre application à l'adresse : http://localhost:9080/GetStartedJava.

Pour arrêter votre application, utilisez la combinaison de touches *Ctrl-C* dans la fenêtre de ligne de commande d'où vous l'avez lancée.


## 3. Préparez l'application pour le déploiement
{: #prepare}

Pour déployer sur {{site.data.keyword.Bluemix_notm}}, il peut être utile de créer un fichier manifest.yml. Ce fichier inclut des informations essentielles sur votre application, telles que son nom, la quantité de mémoire à allouer à chaque instance et la route. Pour vous éviter d'avoir à le créer, nous avons prévu un exemple de fichier manifest.yml dans le répertoire `get-started-java`.

Ouvrez le fichier manifest.yml et, dans le champ `name`, remplacez le nom `GetStartedJava` par celui de votre application, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
   - name: GetStartedJava
     random-route: true
     path: target/GetStartedJava.war
     memory: 512M
     instances: 1
  ```
  {: codeblock}

Dans ce fichier manifest.yml, l'effet de **random-route: true** est de générer une route aléatoire pour votre application afin d'éviter qu'elle n'entre en conflit avec d'autres. Au besoin, vous pouvez remplacer **random-route: true** par **host: myChosenHostName** et fournir un nom d'hôte de votre choix. [En savoir plus...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. Déployez sur {{site.data.keyword.Bluemix_notm}}
{: #deploy}

Déployez votre application dans l'une des régions Bluemix suivantes. Pour une latence aussi faible que possible, choisissez la région la plus proche de vos utilisateurs. 

|Région          |Point d'extrémité d'API                             |
|:---------------|:-------------------------------|
| Sud des Etats-Unis       |https://api.ng.bluemix.net     |
| Royaume-Uni | https://api.eu-gb.bluemix.net  |
| Sydney         | https://api.au-syd.bluemix.net |

1. Spécifiez le point d'extrémité d'API en remplaçant `<API-endpoint>` par le point d'extrémité de votre région.
  ```
cf api <API-endpoint>
  ```
  {: pre}

1. Connectez-vous à votre compte {{site.data.keyword.Bluemix_notm}}.
  ```
cf login
  ```
  {: pre}

1. Depuis le répertoire `get-started-java`, poussez votre application vers {{site.data.keyword.Bluemix_notm}}.
  ```
cf push
  ```
  {: pre}

Le déploiement de votre application peut prendre quelques minutes. Une fois le déploiement achevé, vous verrez un message indiquant que votre application est lancée. Vous pouvez visualiser l'application en accédant à l'URL qui figure dans la sortie de la commande push. Vous pouvez aussi voir à la fois son statut de déploiement et son URL en exécutant la commande suivante :

  ```
cf apps
  ```
  {: pre}

Si des erreurs se produisent dans le processus de déploiement, vous pouvez les diagnostiquer en utilisant la commande `cf logs <Your-App-Name> --recent`.
{: tip}  

## 5. Développement avec Eclipse
{: #eclipse}

{{site.data.keyword.eclipsetoolsfull}} fournit des plug-ins que vous pouvez installer dans un environnement Eclipse existant afin de faciliter son intégration avec {{site.data.keyword.Bluemix_notm}}.

1. Assurez-vous d'avoir [IBM Eclipse Tools for Bluemix](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix).

2. Importez l'exemple `get-started-java` dans Eclipse en sélectionnant **Fichier > Importer > Maven > Projets Maven existants**.

3. Créez une définition de serveur Liberty. Les étapes suivantes permettent de télécharger un nouveau serveur Liberty.
  - Dans la vue **Fenêtre > Afficher la vue > Serveurs**, faites un clic droit et sélectionnez **Nouveau > Serveur**.
  - Sélectionnez **IBM > WebSphere Application Server Liberty**.
  - Sélectionnez **Installer depuis une archive ou un référentiel**.
  - Lorsque vous y êtes invité, entrez le chemin menant au nouveau dossier (/Users/username/liberty) dans lequel vous voulez installer Liberty.
  - Sélectionnez **Télécharger et installer un nouvel environnement d'exécution à partir d'ibm.com**.
  - Sélectionnez **WAS Liberty avec profil Web Java EE 7**.
  - Continuez à dérouler l'assistant jusqu'à la fin en conservant les options par défaut.

4. Lancez votre application localement sur Liberty :
  - Changez le navigateur web de l'environnement pour le navigateur par défaut du système en sélectionnant **Fenêtre > Navigateur web > Navigateur Web système par défaut**.
  - Faites un clic droit sur l'exemple `GetStartedJava` et choisissez **Exécuter en tant que > Exécuter sur le serveur**.
  - Localisez et sélectionnez le serveur Liberty localhost et cliquez sur **Terminer**.

  En quelques secondes, votre application doit être lancée sur http://localhost:9080/GetStartedJava.

5. Modifiez le code : 
  - Ouvrez `src/main/webapp/index.html` et remplacez le titre `<h1>Bienvenue.</h1>` par `<h1>Bienvenue Jane.</h1>`.
  - Enregistrez vos changements. Ils sont pris en compte automatiquement par Liberty.
  - Actualisez votre navigateur (http://localhost:9080/GetStartedJava) pour voir vos changements.

6. Poussez vos changements vers {{site.data.keyword.Bluemix_notm}} :
  - Sur la ligne de commande, à partir du répertoire `get-started-java`, reconstruisez le fichier .war.
    ```
mvn clean install
    ```
    {: pre}
  - Poussez votre application vers {{site.data.keyword.Bluemix_notm}}.
    ```
cf push
    ```
    {: pre}

Et voilà ! Vous venez de lancer votre code à la fois localement et sur le cloud !

## 6. Ajoutez une base de données
{: #add_database}

Nous allons à présent ajouter une base de données NoSQL à l'application et configurer cette dernière pour qu'elle puisse être exécutée localement et sur {{site.data.keyword.Bluemix_notm}}.

1. Dans votre navigateur, connectez-vous à {{site.data.keyword.Bluemix_notm}} et allez au Tableau de bord. Sélectionnez votre application en cliquant sur son nom dans la colonne **Nom**.
2. Cliquez sur **Connexions**, puis sur **Connecter un nouveau**.
3. Dans la section **Données & analyse**, sélectionnez **Cloudant NoSQL DB**, puis créez le service.
4. Sélectionnez **Reconstituer** lorsque vous y êtes invité. {{site.data.keyword.Bluemix_notm}} redémarre votre application et lui fournit les données d'identification pour l'accès à la base de données en utilisant la variable d'environnement `VCAP_SERVICES`. L'application n'a accès à cette variable d'environnement que lorsqu'elle fonctionne sur {{site.data.keyword.Bluemix_notm}}.

Les variables d'environnement vous permettent de séparer les paramètres de déploiement de votre code source. Par exemple, plutôt que de coder en dur le mot de passe d'accès à la base de données, vous pouvez le stocker dans une variable d'environnement et inclure une référence à celle-ci dans votre code source. [En savoir plus...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 7. Utilisez la base de données
{: #use_database}
Nous allons à présent mettre à jour votre code local pour le faire pointer sur cette base de données. Créons à cet effet un fichier de propriétés pour y stocker les identifiants d'accès aux services. Ce fichier ne sera utilisé QUE lorsque l'application est exécutée localement. Lors de son fonctionnement sur {{site.data.keyword.Bluemix_notm}}, elle obtiendra ces identifiants en lisant la variable d'environnement `VCAP_SERVICES`. 

1. Dans Eclipse, ouvrez le fichier src/main/resources/cloudant.properties :
  ```
  cloudant_url=
  ```
  {: pre}

2. Dans votre navigateur, allez sur {{site.data.keyword.Bluemix_notm}} et sélectionnez **Applis > _votre appli_ > Connexions > Cloudant > Afficher les données d'identification**.

3. Copiez seulement la partie `url` des données d'identification et collez-la dans le champ `url` du fichier `cloudant.properties`, puis sauvegardez les changements. 
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:pre}

4. Redémarrez le serveur Liberty dans Eclipse à partir de la vue `Serveurs`.

  Dans votre navigateur, actualisez la vue de http://localhost:9080/GetStartedJava/. Chaque nom que vous entrez dans l'application sera ajouté à la base de données.

  Votre application locale et son instance {{site.data.keyword.Bluemix_notm}} partagent la même base de données. Les noms que vous ajoutez depuis l'une ou l'autre version de l'application doivent apparaître dans les deux lorsque vous actualisez les navigateurs.


Si vous n'avez pas besoin de votre application live sur {{site.data.keyword.Bluemix_notm}}, arrêtez-la. Vous éviterez des frais imprévus.
{: tip}  
