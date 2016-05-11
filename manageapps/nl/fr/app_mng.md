---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Gestion des applications Liberty et Node.js
{: #app_management}

*Dernière mise à jour : 17 mars 2016*

App Management est un ensemble d'utilitaires de développement et de débogage qui peuvent être activés pour les applications Liberty et Node.js
dans {{site.data.keyword.Bluemix}}.
{:shortdesc}

##Utilitaires App Management
{: #Utilities}

Les utilitaires ci-après prennent en charge Liberty et Node.js.

  1. *proxy* : gestion des applications minimale qui sert de proxy entre votre application et {{site.data.keyword.Bluemix_notm}}.

    Lorsque cet utilitaire est activé, le pack de construction démarre un agent proxy qui se trouve entre le contexte d'exécution de
votre
application et le conteneur. L'utilitaire *proxy* traite toutes les demandes que l'application reçoit. En fonction du type de demande, il
effectue une action App Management ou transmet la demande à votre application. *proxy* permet d'activer la plupart des autres utilitaires App
Management. Lorsque *proxy* est activé, le conteneur d'applications reste actif même si l'application tombe en panne. L'agent proxy permet également la mise à jour incrémentielle des fichiers, qui active le mode d'édition directe "Live Edit" pour les applications Node.js.
	
  2. *devconsole* : active l'utilitaire de console de développement accessible à l'adresse URL suivante :
    ```
    http://<nom_de_votre_app>.mybluemix.net/bluemix-debug/manage
    ```
	
    Avec la console de développement, les utilisateurs peuvent redémarrer, arrêter ou interrompre leurs applications. Ils peuvent également activer les utilitaires shell et inspector ou y accéder.

    L'utilitaire devconsole démarre aussi *proxy*.
	
  3. *hc* : agent Health Center qui permet à votre application d'être surveillée par le client Health Center.

    Health Center prend en charge l'analyse des performances de vos applications Liberty et Node.js à l'aide d'IBM Monitoring and Diagnostic Tools. Pour
plus d'informations, voir [How to analyze the performance of Liberty Java or Node.js apps in {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){:new_window}.</p></li>
	
  4. *shell* : active un shell reposant sur le Web qui est accessible depuis l'utilitaire devconsole ou à l'adresse URL
suivante :
    ```
    http://<nom_de_votre_app>.mybluemix.net/bluemix-debug/shell
    ```
	
    Une fenêtre de terminal permettant d'accéder au shell s'ouvre dans votre application une fois que vous avez accédé à
l'utilitaire
shell. Vous pouvez
effectuer toutes les opérations prises en charge habituellement dans un shell classique, par exemple éditer des fichiers, vérifier l'utilisation de la
mémoire ou exécuter des commandes de diagnostic.
	
    L'utilitaire *shell* démarre aussi *proxy*.

Les utilitaires ci-après prennent en charge Liberty seulement.

  1. *debug* : active le mode débogage pour l'application Liberty et permet aux clients tels qu'IBM Eclipse Tools for
{{site.data.keyword.Bluemix_notm}} d'établir une session de débogage à distance avec l'application.
  
   Pour plus d'informations, voir [Débogage à distance](../manageapps/eclipsetools/eclipsetools.html#remotedebug).
   
   L'utilitaire *debug* démarre aussi *proxy*.
   
  2. *jmx* : permet au connecteur JMX REST d'autoriser un client JMX distant à gérer l'application avec les données d'identification
{{site.data.keyword.Bluemix_notm}}.
  
  Pour plus d'informations sur la configuration d'un connecteur JMX, voir [Configuring secure JMX connection to the Liberty profile.](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}.
  
  L'utilitaire *jmx* ne démarre pas proxy.

Les utilitaires ci-après prennent en charge Node.js seulement.

  1. *inspector* : active l'interface de débogage node inspector qui est accessible depuis l'utilitaire
*devconsole*
ou à l'adresse *https://monApp.mybluemix.net/bluemix-debug/inspector*.
  
  Le processus inspector s'exécute dans votre conteneur d'applications. Servez-vous de cet utilitaire pour créer des profils d'utilisation de l'unité
centrale, ajouter des points d'arrêt et déboguer le code alors que votre application s'exécute dans {{site.data.keyword.Bluemix_notm}}. Pour plus
d'informations sur le module node inspector, voir [node-inspector dans le référentiel
GitHub](https://github.com/node-inspector/node-inspector){:new_window}.
  
  L'utilitaire *inspector* démarre aussi *proxy*.
  
  2. *strongpm* : permet l'utilisation de [StrongLoop Arc](https://strongloop.com/node-js/arc){:new_window} pour
analyser votre application Node.js avec des utilitaires tels que [les métriques, le
profilage et la fonction de trace de StrongLoop](https://strongloop.com/node-js/devops-tools/){:new_window}.
    
  L'utilitaire *strongpm* démarre aussi *proxy*.
  
  Procédez comme suit pour configurer votre application Node.js avec [StrongLoop
Arc](https://strongloop.com/node-js/arc){:new_window}.

    1. Configurez la variable d'environnement *strongpm* BlUEMIX_APP_MGMT_ENABLE et reconstituez votre application.
    
	```
    cf set-env <nom_app> BLUEMIX_APP_MGMT_ENABLE strongpm
    cf restage <nom_app>
    ```
	
    2. Depuis la ligne de commande Cloud Foundry, ajoutez une route à votre application, dans laquelle la chaîne "-pm" est ajoutée au nom
d'application, par exemple <nom_app>-pm.mybluemix.net.
    
	```
    cf map-route <nom_app> ng.bluemix.net -n <nom_app>-pm
    ```
	
    3. Installez le [module npm StrongLoop](https://www.npmjs.com/package/strongloop){:new_window} sur votre poste de travail
local.
    
	```
    npm install -g strongloop
    ```
	
    4. Créez un compte sur le [site Web de StrongLoop](https://strongloop.com/register/){:new_window}.
    5. Lancez Arc sur votre poste de travail local et connectez-vous avec le compte que vous avez créé.
    
	```
    slc arc
    ```
	
    6. Accédez à la vue Process Manager dans Arc. Entrez la route que vous venez de créer avec le port 80 dans Process Manager. Cliquez sur le bouton Activate. Voir la [documentation complète relative à l'utilisation
d'Arc](https://docs.strongloop.com/display){:new_window} pour plus de détails.
	
  3. *trace* : définit dynamiquement des niveaux de trace si votre application utilise les modules de journalisation *log4js*,
*ibmbluemix*
ou *bunyan*.
  
  **Remarque :** les versions de dépendance prises en charge sont :

    * log4js : (0.6.0 à 0.6.24)
    * bunyan : (1.0.0, 1.0.1, 1.1.0 à 1.1.3, 1.2.0 à 1.2.3, 1.3.0 à 1.3.5)
    * ibmbluemix : (1.0.0-20140707-1250) à (1.0.0-20150409-1328)
  
  Accédez à la page Détails de l'instance dans la console Web de {{site.data.keyword.Bluemix_notm}} et sélectionnez
**Actions** pour afficher l'interface utilisateur.

  L'utilitaire *trace* ne démarre pas *proxy*.

##Configuration d'App Management
{: #configure}

Pour activer les utilitaires App Management, définissez la variable d'environnement *BLUEMIX_APP_MGMT_ENABLE*
et reconstituez votre application. Vous pouvez activer plusieurs utilitaires en les séparant par le signe plus (“+”).

Par exemple, pour activer les utilitaires devconsole et *shell*, exécutez la commande suivante :

```
cf set-env monApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

N'oubliez pas de reconstituer votre application après avoir défini la variable d'environnement :

```
cf restage monApp
```

Si vous ne souhaitez pas que les utilitaires App Management soient installés avec votre application, associez la
variable d'environnement *BLUEMIX_APP_MGMT_INSTALL* à la valeur 'false' et reconstituez votre application.

Exemple :

```
cf set-env monApp BLUEMIX_APP_MGMT_INSTALL false
cf restage monApp
```

##Restrictions
{: #restrictions}

* App Management prend en charge les applications à instance unique seulement.
* Les modifications que vous apportez à votre application avec App Management sont transitoires et sont perdues lorsque vous quittez ce mode. Ce mode a été conçu pour être utilisé temporairement au cours du développement et ne doit pas être utilisé dans un environnement de production en raison
de ses performances.
* La plupart des utilitaires App Management ne fonctionne pas si vous définissez votre commande de démarrage dans le fichier manifest.yml (command)
ou dans l'interface de ligne de commande CF (-c). Ces méthodes constituent des remplacements de pack de construction et sont des anti-modèles pour le
démarrage des applications Node.js. Pour de meilleurs résultats, définissez la commande de démarrage dans le fichier package.json ou Procfile.

##Mode développement pour Eclipse Tools
{: #devmode}

Le mode développement est une fonction d'[Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](../manageapps/eclipsetools/eclipsetools.html#eclipsetools) qui permet aux développeurs d'utiliser leurs applications lorsqu'elles s'exécutent dans le cloud.

Lorsqu'ils utilisent leurs applications dans {{site.data.keyword.Bluemix_notm}}, les développeurs peuvent
avoir l'impression de ne pas pouvoir effectuer les activités de développement habituelles qu'ils peuvent effectuer dans un
environnement local. Le mode développement d'Eclipse Tools résout ce problème en leur permettant de travailler dans le cloud, tout en se trouvant dans un espace de travail
sécurisé temporaire.

Le mode développement est pris en charge pour les applications Liberty et Node.js. Lorsqu'il est activé pour votre application Liberty ou Node.js,
vous pouvez mettre à jour des fichiers de façon incrémentielle sans avoir à envoyer votre application par commande push. Vous pouvez également établir une session de débogage pour votre application. Le
mode développement pour les applications Liberty équivaut à
activer les utilitaires d'App Management debug et jmx. Pour les applications Node.js, il équivaut à activer les utilitaires *devconsole*,
*inspector* et *shell*.
