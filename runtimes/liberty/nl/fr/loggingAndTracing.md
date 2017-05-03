---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Journalisation et traçage
{: #logging_tracing}

## Fichiers journaux
{: #log_files}

Les journaux Liberty standard, tels que le fichier `messages.log` ou le répertoire `ffdc`, sont disponibles dans IBM Bluemix, dans le répertoire `logs` de chaque instance d'application. Vous pouvez accéder à ces journaux à partir de la console IBM Bluemix ou à via le client de ligne de commande pour Cloud Foundry.
Par exemple :

* Pour accéder aux journaux récents d'une application, exécutez la commande suivante :

  ```
  $ cf logs --recent <appname>
  ```
  {: codeblock}

* Pour voir le fichier `messages.log` d'une application lancée sur un noeud DEA, exécutez la commande suivante :

  ```
  $ cf files <appname> logs/messages.log
  ```
  {: codeblock}

* Pour voir le fichier `messages.log` d'une application lancée sur une cellule Diego, exécutez la commande suivante :

  ```
  $ cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

Vous
pouvez définir le niveau de journalisation et d'autres options de trace dans
le fichier de configuration de Liberty. Pour plus d'informations, voir
[Profil
Liberty : trace et journalisation](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html). Vous pouvez également ajuster le traçage sur une instance d'application en cours d'exécution à l'aide de la console IBM Bluemix.

## Utilisation des fonctions de trace et de vidage
{: #using_trace_and_dump}

Vous pouvez ajuster la configuration de traçage Liberty pour une application en cours d'exécution en procédant directement à partir de la console IBM Bluemix. La console offre aussi la possibilité de demander un vidage des unités d'exécution (threads) ou du tas (heap). Pour ajuster la configuration de traçage ou demander un vidage, sélectionnez une application Liberty dans la console Bluemix et choisissez le menu `Exécution` dans la navigation. Dans la vue `Exécution`, sélectionnez une instance et cliquez sur le bouton *TRACE* ou *VIDAGE*. Si vous ajustez le niveau de trace, consultez [Profil Liberty : trace et journalisation](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html) pour les détails concernant la syntaxe de la spécification de trace.

### Diego : déclenchement de vidages via SSH

Dans le cas d'une application fonctionnant dans une cellule Diego, il est aussi
possible de déclencher un vidage des unités d'exécution ou du tas via le client de ligne
de commande pour Cloud Foundry en utilisant la fonctionnalité SSH. Par exemple :

```
$ cf ssh <appname> -c "pkill -3 java"
```
{: codeblock}

Consultez la documentation ci-dessous pour les détails concernant le téléchargement des fichiers de vidage générés.

## Téléchargement des fichiers de vidage
{: #download_dumps}

Par défaut, les différents fichiers de vidage sont placés dans le répertoire `dumps` du conteneur de l'application.

### Application DEA

Dans le cas d'une application lancée sur un noeud DEA, utilisez la fonctionnalité "cf files" pour voir et télécharger les fichiers de vidage.

* Pour voir les vidages générés, exécutez la commande suivante :

  ```
  $ cf files <appname> dumps
  ```
  {: codeblock}

* Pour télécharger un fichier de vidage, exécutez les commandes suivantes :

    1. Obtenir l'identificateur global unique (GUID) de l'application

      ```
      $ cf app <appname> --guid
      ```
      {: codeblock}

    2. Télécharger le fichier de vidage

      ```
      $ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
      ```
      {: codeblock}

### Application Diego

Dans le cas d'une application lancée dans une cellule Diego, utilisez la fonctionnalité "cf ssh" pour voir et télécharger les fichiers de vidage.

* Pour voir les vidages générés, exécutez la commande suivante :

  ```
  $ cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* Pour télécharger un fichier de vidage, exécutez la commande suivante :

  ```
  $ cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

Il est aussi possible d'utiliser `scp` et d'autres outils similaires pour voir et télécharger les fichiers de vidage. Pour plus d'informations, consultez [Accessing Apps with SSH![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html).

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
