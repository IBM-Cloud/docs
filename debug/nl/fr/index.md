---

copyright:
  years: 2015, 2016

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}


# Débogage
{: #debugging}

*Dernière mise à jour : 3 mars 2016*

Si vous rencontrez des problèmes avec {{site.data.keyword.Bluemix}}, vous pouvez afficher les fichiers journaux et déboguer les erreurs. 
{:shortdesc}

Les journaux fournissent des informations telles que l'exécution réussie d'un travail ou son échec. Ils fournissent également des informations
appropriées qui peuvent être utilisées pour le débogage et la détermination de la cause d'un problème.

Les journaux ont un format fixe. Vous pouvez filtrer les journaux prolixes ou utiliser des hôtes de
journalisation externes pour
stocker et traiter les journaux. Pour plus d'informations sur les formats des journaux, leur affichage et leur filtrage, ainsi que sur la configuration de
la journalisation externe, voir [Journalisation pour les applications qui s'exécutent dans Cloud
Foundry](../monitor_log/monitoringandlogging.html#logging_for_bluemix_apps){: new_window}.


## Débogage des erreurs de constitution
{: #debugging-staging-errors}
Vous pouvez rencontrer des problèmes lorsque vous constituez vos applications dans {{site.data.keyword.Bluemix_notm}}. Si la constitution de votre
application échoue, vous pouvez consulter les journaux afin d'identifier la cause de l'erreur et de résoudre le problème.

Pour comprendre la raison pour laquelle votre application ne fonctionne pas dans {{site.data.keyword.Bluemix_notm}}, vous devez savoir comment
une
application est déployée et exécutée dans {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations, voir [Déploiement d'une application](../manageapps/depapps.html#appdeploy){: new_window}.

La procédure suivante présente l'utilisation de la commande `cf logs` pour déboguer des erreurs constitution. Avant de continuer, vérifiez que vous avez installé l'interface de ligne de commande cf. Pour plus d'informations sur l'installation de l'interface de ligne de commande cf, voir [Installation de l'interface de ligne de commande cf](../starters/install_cli.html){: new_window}.

  1. Connectez-vous à {{site.data.keyword.Bluemix_notm}} en entrant la commande suivante sur l'interface de ligne de commande cf :
     ```
	 cf api https://api.ng.bluemix.net
	 ```
	 
  2. Connectez-vous à {{site.data.keyword.Bluemix_notm}} en entrant `cf login`.
  
  3. Procédez à l'extraction des fichiers journaux récents en entrant la commande `cf logs nom_app --recent`. Si vous souhaitez filtrer un fichier journal prolixe, utilisez l'option `grep`. Par exemple, vous pouvez entrer le code suivant pour afficher les journaux [STG] seulement :
    ```
	cf logs nom_app --recent | grep '\[STG\]'
	```
  4. Regardez la première erreur qui apparaît dans le journal.
  
Si vous utilisez le plug-in IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} pour déployer des applications, l'onglet **Console** de l'outil Eclipse affiche des journaux
semblables à la sortie de cf logs. Vous pouvez également ouvrir une fenêtre Eclipse distincte pour contrôler `les journaux` au cours du déploiement de l'application.

En complément de la commande `cf logs`, vous pouvez également utiliser le service {{site.data.keyword.Bluemix_notm}} Monitoring and Analytics pour collecter des détails de journaux. Ce service contrôle également la performance, la santé et la disponibilité de vos applications. Il fournit également des analyses de journaux pour les applications de contexte d'exécution Node.js et Liberty.  

### Débogage des erreurs de constitution pour une application Node.js

Vous trouverez ci-après un exemple de journal qui s'affiche suite à l'entrée de la commande `cf logs nom_app --recent`. On
présuppose que des erreurs de constitution se sont produites pour une application Node.js :
```
2014-08-11T14:19:36.17+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({name"=>"SampleExpressApp"}
2014-08-11T14:20:44.17+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({"state"=>"STOPPED"})
2014-08-11T14:20:44.19+0100 [App/0]   ERR
2014-08-11T14:20:44.43+0100 [DEA]     OUT Stopping app instance (index 0) with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:44.44+0100 [DEA]     OUT Stopped app instance (index 0) with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:48.97+0100 [DEA]     OUT Got staging request for app with id 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:50.94+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({"state"=>"STARTED"})
2014-08-11T14:20:51.66+0100 [STG]     OUT -----> Download app package (4.1M)
2014-08-11T14:20:51.90+0100 [STG]     OUT -----> Download app buildpack cache (1.1M)
2014-08-11T14:20:52.78+0100 [STG]     OUT -----> Buildpack Version: v1.1-20140717-1447
2014-08-11T14:20:52.78+0100 [STG]     ERR parse error: Expected another key-value pair at line 18, column 3
2014-08-11T14:20:52.79+0100 [STG]     OUT 0 info it worked if it ends with ok
```
{: screen}


La première erreur du journal indique la raison pour laquelle la constitution a échoué. Dans cet exemple, la première erreur correspond à une
sortie du composant DEA au cours de la phase de constitution.
```
2014-08-11T14:20:52.78+0100 [STG]   ERR parse error: expected another key-value pair at line 18, column 3
```
{: screen}


Pour une application Node.js, le composant DEA utilise les informations du fichier `package.json` pour télécharger les modules. A partir de cette erreur, vous pouvez voir que l'erreur s'est produite pour le module. Il peut être nécessaire de vérifier la ligne 18 du fichier `package.json`. 

```
15   "jade": "~1.3.0",
16   "mongodb": "*",
17   "monk":"*",
18   }
```
{: screen}


Une virgule figure à la fin de la ligne 17, une paire clé-valeur est donc attendue en ligne 18. Pour corriger le problème, supprimez la virgule :

```
15   "jade": "~1.3.0",
16   "mongodb": "*",
17   "monk":"*"
18   }
```
{: screen}


## Débogage d'erreurs d'exécution
{: #debugging-runtime-errors}
Si vous rencontrez des problèmes lors de l'exécution de votre application, les journaux peuvent vous aider à déterminer la cause de l'erreur et à y remédier. 

La journalisation de sortie standard et d'erreur standard peut être activée. Pour plus d'informations sur la manière de configurer les fichiers journaux pour des applications déployées à l'aide du pack de construction intégré {{site.data.keyword.Bluemix_notm}}, consultez la liste ci-après :

  * Pour les applications Liberty for Java™, voir [Liberty Profile: Logging and Trace](http://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html){: new_window}.
  * Pour les applications Node.js, voir [How
to log in node.js](http://docs.nodejitsu.com/articles/intermediate/how-to-log){: new_window}. 
  * Pour les applications PHP, voir [error_log](http://php.net/manual/en/function.error-log.php){: new_window}.
  * Pour les applications Python, voir [Logging
HOWTO](https://docs.python.org/2/howto/logging.html){: new_window}.
  * Pour les applications Ruby on Rails, voir
[The Logger](http://guides.rubyonrails.org/debugging_rails_applications.html#the-logger){: new_window}.
  * Pour les applications Ruby Sinatra, voir
[Logging](http://www.sinatrarb.com/intro.html#Logging){: new_window}.
  
Lorsque vous entrez la commande `cf logs nom_app --recent` dans l'interface de ligne de commande cf, seuls les journaux les plus
récents s'affichent. Pour accéder aux erreurs précédentes, vous devez extraire tous les journaux. Pour ce faire, utilisez l'une des méthodes suivantes :
<dl> 
<dt><strong>Service {{site.data.keyword.Bluemix_notm}} Monitoring and Analytics</strong></dt> 
<dd>Les fonctionnalités intégrées de recherche et d'analyse de fichier journal du service Monitoring and Analytics permettent d'identifier rapidement les erreurs. Pour plus d'informations, voir <a href="../services/monana/index.html#gettingstartedtemplate" target="_blank">Contrôle et analyse</a>.</dd> 
<dt><strong>Outils tiers </strong></dt> 
<dd>Vous pouvez collecter et exporter les journaux de votre application sur un hôte de journaux externe. Pour plus d'informations, voir
<a href="../monitor_log/monitoringandlogging.html#thirdparty_logging" target="_blank">Configuration d'hôtes de journaux externes</a>.</dd> 
<dt><strong>Scripts pour collecter et exporter les journaux  </strong></dt> 
<dd>Pour utiliser un script permettant de collecter et d'exporter automatiquement les journaux vers un fichier externe, vous devez vous connecter au serveur {{site.data.keyword.Bluemix_notm}} depuis votre ordinateur et disposer de suffisamment d'espace pour y télécharger les journaux. Pour plus d'informations, voir <a href="../support/index.html#collecting-diagnostic-information" target="_blank">Collecte d'informations de diagnostic</a>. </dd>
</dl>

Auparavant, les fichiers `stdout.log` et `stderr.log` étaient accessibles par défaut via la vue d'application dans
le tableau de bord {{site.data.keyword.Bluemix_notm}}, sous **Fichiers** > **journaux**. Toutefois, cette journalisation d'application n'est plus disponible dans la version en cours de Cloud Foundry, où {{site.data.keyword.Bluemix_notm}} est hébergé. Pour que la journalisation de sortie standard et d'erreur standard reste accessible via le tableau de bord {{site.data.keyword.Bluemix_notm}} sous
**Fichiers** > **journaux**, vous pouvez rediriger la journalisation vers d'autres fichiers du système de
fichiers {{site.data.keyword.Bluemix_notm}}, selon le contexte d'exécution que vous utilisez. 

  * Pour les applications Liberty for Java, la sortie dirigée vers stdout et stderr se trouve déjà dans le fichier `messages.log` situé dans le
répertoire logs. Recherchez les entrées portant respectivement le préfixe SystemOut et SystemErr.
  * Pour les applications Node.js, vous pouvez redéfinir la fonction console.log pour écrire des données explicitement dans un fichier dans le
répertoire logs.
  * Pour les applications PHP, vous pouvez utiliser la fonction error_log pour écrire des données dans un fichier dans le répertoire logs.
  * Pour les applications Python, vous pouvez demander au consignateur d'écrire des données dans un fichier dans le répertoire logs : logging.basicConfig(filename='../../logs/example.log',level=logging.DEBUG)
  * Pour les applications Ruby, vous pouvez demander au consignateur d'écrire des données dans un fichier dans le répertoire logs.
 

# rellinks
{: #rellinks}

## general
{: #general}

  * [Droplet Execution Agent (DEA)](http://docs.cloudfoundry.org/concepts/architecture/execution-agent.html){: new_window}
  * [Initiation au service IBM Monitoring and Analytics for Bluemix](../services/monana/index.html#gettingstartedtemplate){: new_window}
  * [Fonctionnement de Bluemix](../public/index.html#howwork){: new_window}
  * [Installation de l'outil de commande cf](../starters/install_cli.html){: new_window}
  * [Affichage des journaux](../monitor_log/monitoringandlogging.html#viewing_logs){: new_window}
  
  
 














