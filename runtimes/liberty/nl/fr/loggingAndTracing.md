---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Journalisation et traçage
{: #logging_tracing}

## Fichiers journaux
{: #log_files}

Les journaux Liberty standard, tels que le fichier messages.log ou le répertoire ffdc, sont disponibles dans IBM Bluemix, dans le répertoire logs de chaque instance d'application. Vous pouvez accéder à ces journaux à partir de la console IBM Bluemix ou à l'aide des commandes cf logs et cf files.
Par exemple, pour afficher le fichier messages.log, exécutez la commande suivante :
```
    $ cf files <yourappname> logs/messages.log
```
{: codeblock}

Vous
pouvez définir le niveau de journalisation et d'autres options de trace dans
le fichier de configuration de Liberty. Pour plus d'informations, voir
[Profil
Liberty : trace et journalisation](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html?cp=SSAW57_8.5.5%2F3-17-0-0). Vous pouvez également ajuster le traçage sur une instance d'application en cours d'exécution à l'aide de la console IBM Bluemix.

## Utilisation des fonctions de trace et de vidage
{: #using_trace_and_dump}

L'interface utilisateur d'IBM Bluemix dispose de fonctions de trace et de vidage.
* Utilisez la fonction Trace pour examiner et mettre à jour la spécification
traceSpecification de journalisation Liberty sur les instances d'application en cours d'exécution.
* Utilisez la fonction Vidage pour créer les clichés d'unité d'exécution et de pile sur les instances d'application en exécution.

Pour
ce faire, sélectionnez une application Liberty dans l'interface utilisateur. Dans la catégorie Exécution du panneau de navigation, vous pouvez ouvrir les détails de l'instance. Sélectionnez une ou plusieurs instances. Dans le menu Actions, vous pouvez choisir TRACE ou DUMP.

## Téléchargement des fichiers de vidage
{: #download_dumps}

<strong>Prérequis :</strong>
* [Installez l'interface de ligne de commande CF](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html)
* [Installez le plug-in Diego-Enabler](https://github.com/cloudfoundry-incubator/Diego-Enabler) si votre application s'exécute dans Diego

<strong>Si votre application s'exécute dans DEA, procédez comme suit :</strong>
  
1. Obtenez app_guid
```
$ cf app <app_name> --guid
```

2. Téléchargez le fichier de vidage
```
$ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
```

<strong>Si votre application s'exécute dans Diego, procédez comme suit :</strong>
  
1. Obtenez app_guid
```
$ cf app <app_name> --guid
```

2. Obtenez app_ssh_endpoint(host and port) et app_ssh_host_key_fingerprint
```
$ cf curl /v2/info
```

3. Obtenez ssh-code pour la commande scp
```
$ cf ssh-code
```

4. Lancez la commande scp sur le fichier de vidage distant vers l'environnement local et utilisez ssh-code lorsque vous êtes invité à indiquer un mot de passe
```
$ scp -P <app_ssh_endpoint_port> -o User=cf:<app_guid>/<instance_id> <app_ssh_endpoint_host>:/home/vcap/dumps/<dump_file_name> <local_dump_file_name>
```

Pour plus de détails, voir [Accessing Apps with SSH](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html).


# rellinks
{: #rellinks}
## general
{: #general}
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)

