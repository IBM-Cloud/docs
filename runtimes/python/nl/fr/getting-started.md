---

copyright:
  years: 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Initiation à Python sur Bluemix
{: #getting_started}

* {: download} Félicitations, vous avez déployé une application exemple Hello World sur {{site.data.keyword.Bluemix}} !  Pour commencer, suivez ce guide pas à pas. Ou <a class="xref" href="http://bluemix.net" target="_blank" title="(Télécharger l'exemple de code)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Télécharger le code de l'application" />téléchargez l'exemple de code</a> et découvrez-le par vous-même.

En suivant ce guide, vous allez mettre en place un environnement de développement, déployer une application à la fois localement et sur {{site.data.keyword.Bluemix}}, puis intégrer un service de base de données {{site.data.keyword.Bluemix}} dans votre application.

## Prérequis 
{: #prereqs}

Vous aurez besoin des éléments suivants :
* [Compte {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI (client de ligne de commande pour Cloud Foundry) ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://git-scm.com/downloads){: new_window}
* [Python ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.python.org/downloads/){: new_window}

## 1. Clonez l'application exemple
{: #clone}

Vous êtes maintenant prêt à travailler avec l'application. Clonez le référentiel et placez-vous dans le répertoire où se trouve l'application exemple.
  ```
git clone https://github.com/IBM-Bluemix/get-started-python
  ```
  {: pre}
  ```
cd get-started-python
  ```
  {: pre}

  Examinez attentivement les fichiers dans le répertoire *get-started-python* afin de vous familiariser avec leur contenu.

## 2. Lancez l'application localement
{: #run_locally}

Consultez le document [The Hitchhiker’s Guide to Python! ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://docs.python-guide.org/en/latest/) pour une aide sur la configuration de Python sur votre système.
{: tip}

Installez les dépendances listées dans le fichier [requirements.txt![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://pip.readthedocs.io/en/stable/user_guide/#requirements-files) afin de pouvoir exécuter l'application localement. 

Au besoin, vous pouvez utiliser un [environnement virtuel ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://packaging.python.org/installing/#creating-and-using-virtual-environments) pour éviter toute contradiction entre ces dépendances et celles d'autres projets Python ou de votre système d'exploitation.
{: tip}

  ```
pip install -r requirements.txt
  ```
  {: pre}

Avec Python3, vous pouvez également émettre la commande

  ```
python3 -m pip install -r requirements.txt
  ```
  {: pre}

Exécutez l'application.
  ```
python hello.py
  ```
  {: pre}

 Affichez votre application sur : http://localhost:8000


## 3. Préparez l'application pour le déploiement
{: #prepare}

Pour déployer sur {{site.data.keyword.Bluemix_notm}}, il peut être utile de créer un fichier manifest.yml. Ce fichier inclut des informations essentielles sur votre application, telles que son nom, la quantité de mémoire à allouer à chaque instance et la route. Pour vous éviter d'avoir à le créer, nous avons prévu un exemple de fichier manifest.yml dans le répertoire `get-started-python`.

Ouvrez le fichier manifest.yml et, dans le champ `name`, remplacez le nom `GetStartedPython` par celui de votre application, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
  - name: GetStartedPython
    random-route: true
    memory: 128M
  ```
  {: codeblock}

Dans ce fichier manifest.yml, l'effet de **random-route: true** est de générer une route aléatoire pour votre application afin d'éviter qu'elle n'entre en conflit avec d'autres. Au besoin, vous pouvez remplacer **random-route: true** par **host: myChosenHostName** et fournir un nom d'hôte de votre choix. [En savoir plus...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. Déployez l'application
{: #deploy}

Vous pouvez utiliser l'interface de ligne de commande Cloud Foundry pour déployer des applications.

Choisissez votre point d'extrémité d'API
   ```
cf api <API-endpoint>
   ```
   {: pre}

Dans cette commande, remplacez *API-endpoint* par un point d'extrémité d'API parmi les suivants.

|URL                             |Région          |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | Sud des Etats-Unis       |
| https://api.eu-gb.bluemix.net  | Royaume-Uni |
| https://api.au-syd.bluemix.net | Sydney         |

Connectez-vous à votre compte {{site.data.keyword.Bluemix_notm}}

  ```
cf login
  ```
  {: pre}

Depuis le répertoire *get-started-python*, poussez votre application vers {{site.data.keyword.Bluemix_notm}}
  ```
cf push
  ```
  {: pre}

Cette opération peut prendre une minute. S'il y a une erreur dans le processus de déploiement, vous pouvez utiliser la commande `cf logs <Nom_Application> --recent` pour identifier et résoudre le problème.

Une fois le déploiement achevé, vous devez voir un message indiquant que votre application est lancée. Vous pouvez visualiser l'application en accédant à l'URL qui figure dans la sortie de la commande push. Vous pouvez aussi émettre la commande
  ```
cf apps
  ```
  {: pre}
pour voir l'état de votre application et obtenir son URL.

## 5. Ajoutez une base de données
{: #add_database}

Nous allons à présent ajouter une base de données NoSQL à l'application et configurer cette dernière pour qu'elle puisse être exécutée localement et sur {{site.data.keyword.Bluemix_notm}}.

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}} dans votre navigateur. Accédez au `Tableau de bord`. Sélectionnez votre application en cliquant sur son nom dans la colonne `Nom`.
2. Cliquez sur `Connexions`, puis sur `Connecter un nouveau`.
2. Dans la section `Données & analyse`, sélectionnez `Cloudant NoSQL DB` et `Créer` pour créer le service.
3. Sélectionnez `Reconstituer` lorsque vous y êtes invité. {{site.data.keyword.Bluemix_notm}} redémarre votre application et lui fournit les données d'identification pour l'accès à la base de données en utilisant la variable d'environnement `VCAP_SERVICES`. L'application n'a accès à cette variable d'environnement que lorsqu'elle fonctionne sur {{site.data.keyword.Bluemix_notm}}.

Les variables d'environnement vous permettent de séparer les paramètres de déploiement de votre code source. Par exemple, plutôt que de coder en dur le mot de passe d'accès à la base de données, vous pouvez le stocker dans une variable d'environnement et inclure une référence à celle-ci dans votre code source. [En savoir plus...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 6. Utilisez la base de données
{: #use_database}
Nous allons à présent mettre à jour votre code local pour le faire pointer sur cette base de données. Créons à cet effet un fichier json pour y stocker les identifiants d'accès aux services que l'application utilisera. Ce fichier ne sera utilisé QUE lorsque l'application est exécutée localement. Lors de son fonctionnement sur {{site.data.keyword.Bluemix_notm}}, elle obtiendra ces identifiants en lisant la variable d'environnement VCAP_SERVICES.

1. Créez un fichier nommé `vcap-local.json` dans le répertoire `get-started-python` et ajoutez-y le contenu suivant :
  ```
  {
    "services": {
      "cloudantNoSQLDB": [
        {
          "credentials": {
            "username":"CLOUDANT_DATABASE_USERNAME",
            "password":"CLOUDANT_DATABASE_PASSWORD",
            "host":"CLOUDANT_DATABASE_HOST"
          },
          "label": "cloudantNoSQLDB"
        }
      ]
    }
  }
  ```
  {: pre}

2. De retour dans l'interface utilisateur de {{site.data.keyword.Bluemix_notm}}, sélectionnez votre application -> Connexions -> Cloudant -> Afficher les données d'identification

3. Copiez les valeurs des champs `username`, `password` et `host` des données d'identification dans les mêmes champs du fichier `vcap-local.json`, en remplaçant **CLOUDANT_DATABASE_USERNAME**, **CLOUDANT_DATABASE_PASSWORD** et **CLOUDANT_DATABASE_URL**.

4. Lancez votre application localement.
  ```
python hello.py
  ```
  {: pre}

  Affichez votre application sur : http://localhost:8000. Chaque nom que vous entrez dans l'application sera ajouté à la base de données.

  Votre application locale et son instance {{site.data.keyword.Bluemix_notm}} partagent la même base de données. Vous pouvez visualiser votre application {{site.data.keyword.Bluemix_notm}} en accédant à l'URL obtenue précédemment dans la sortie de la commande push. Les noms que vous ajoutez depuis l'une ou l'autre version de l'application doivent apparaître dans les deux lorsque vous actualisez les navigateurs.

Si vous n'avez pas besoin de votre application live, arrêtez-la. Vous éviterez des frais imprévus.
{: tip}
