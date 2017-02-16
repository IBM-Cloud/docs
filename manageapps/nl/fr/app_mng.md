---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Gestion des applications Liberty et Node.js
{: #app_management}


App Management est un ensemble d'utilitaires de développement et de débogage qui peuvent être activés pour les applications Liberty et Node.js
dans {{site.data.keyword.Bluemix}}.
{:shortdesc}

## Utilitaires App Management
{: #Utilities}

### Les utilitaires ci-après prennent en charge Liberty et Node.js
{: #liberty_and_node_utilities}

#### proxy
{: #proxy}

Le *proxy* offre une gestion des applications minimale entre
votre application et {{site.data.keyword.Bluemix_notm}}.

Lorsque cet utilitaire est activé, le pack de construction démarre un agent proxy qui se trouve entre le contexte d'exécution de
votre
application et le conteneur. L'utilitaire *proxy* traite toutes les demandes que l'application reçoit. En fonction du type de demande, il
effectue une action App Management ou transmet la demande à votre application. Le
*proxy* permet d'activer la plupart des autres utilitaires App
Management. Lorsque *proxy* est activé, le conteneur d'applications reste actif même si l'application tombe en panne. L'agent proxy permet également la mise à jour incrémentielle des fichiers, qui active le mode d'édition directe "Live Edit" pour les applications Node.js.

#### noproxy
{: #noproxy}

L'utilitaire *noproxy* désactive l'utilitaire
*proxy* lorsqu'il a été automatiquement démarré par l'un des
autres utilitaires. Le proxy n'est pas nécessaire avec Diego car ce dernier
permet d'exécuter directement *ssh* sur votre application et de
configurer l'acheminement de port.

L'utilitaire *noproxy* est applicable uniquement pour les
applications qui s'exécutent dans une cellule Diego.



#### devconsole
{: #devconsole}

L'utilitaire de la console de développement (*devconsole*)
permet aux utilisateurs de redémarrer, arrêter ou suspendre leurs applications. Ils peuvent également activer les utilitaires shell et inspector ou y accéder.  Il est accessible à l'adresse URL suivante :
```
  https://<nom_votre_app>.mybluemix.net/bluemix-debug/manage
```

Pour Node version 6.3.0 ou ultérieure, la console de développement
fournit un bouton de redémarrage pour votre application et un accès à
l'utilitaire shell.  Pour plus d'informations, voir la
section relative à *inspector*.

L'utilitaire *devconsole* démarre également *proxy*.

#### hc
{: #hc}

L'agent Health Center (*hc*) permet à votre application
d'être surveillée par le client Health Center.

Health Center prend en charge l'analyse des performances de vos applications Liberty et Node.js à l'aide d'IBM Monitoring and Diagnostic Tools. Pour plus d'informations, voir [How to analyze the performance of Liberty Java or Node.js apps in {{site.data.keyword.Bluemix_notm}} ![icône de lien externe](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){: new_window}.</p></li>

L'utilitaire *hc* démarre également *proxy*.

L'utilitaire *hc* peut être utilisé conjointement avec *noproxy*. Pour
utiliser Health Center avec *noproxy*, établissez d'abord
l'acheminement de port à l'aide de la commande `cf ssh`. Exemple :

```
$ cf ssh -N -T -L 1883:127.0.0.1:1883 <nomApp>
```

Ensuite, pour vous connecter avec le client Health Center, utilisez la [connexion MQTT ![icône de lien externe](../icons/launch-glyph.svg)](http://www.ibm.com/support/knowledgecenter/SS3KLZ/com.ibm.java.diagnostics.healthcenter.doc/topics/connectingtojvm.html){: new_window} et indiquez l'hôte `127.0.0.1` et le port `1883`.

#### shell
{: #shell}

L'utilitaire *shell* active un shell basé sur le Web.  Il est
accessible depuis l'utilitaire *devconsole* ou à partir de
l'adresse URL suivante :

```
  https://<nom_votre_app>.mybluemix.net/bluemix-debug/shell
```

Une fenêtre de terminal permettant d'accéder au shell s'ouvre dans votre application une fois que vous avez accédé à
l'utilitaire *shell*. Vous pouvez
effectuer toutes les opérations prises en charge habituellement dans un shell classique, par exemple éditer des fichiers, vérifier l'utilisation de la
mémoire ou exécuter des commandes de diagnostic.

L'utilitaire *shell* démarre aussi *proxy*.

Diego fournit un shell interactif via la commande `cf
ssh`, de sorte que l'utilitaire *shell* n'est utile
que pour les applications qui s'exécutent sur un agent DEA.

### Les utilitaires ci-après prennent en charge Liberty seulement
{: #liberty_utilities}

#### debug
{: #debug}

L'utilitaire *debug* active le mode débogage pour l'application Liberty et permet aux clients tels qu'IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} d'établir une session de [débogage à distance](/docs/manageapps/eclipsetools/eclipsetools.html#remotedebug) avec l'application.

L'utilitaire *debug* démarre aussi *proxy*.

L'utilitaire *debug* peut être utilisé conjointement avec *noproxy*. Pour utiliser le débogueur avec *noproxy*, établissez d'abord l'acheminement de port à l'aide de la commande `cf ssh`. Exemple :

```
$ cf ssh -N -T -L 7777:127.0.0.1:7777 <nomApp>
```

Ensuite, pour vous connecter à Eclipse, utilisez "Remote Java Configuration" et indiquez l'hôte `127.0.0.1` et le port `7777`.

#### jmx
{: #jmx}

L'utilitaire *jmx* permet au connecteur JMX REST d'autoriser un client JMX distant à gérer l'application avec les données d'identification {{site.data.keyword.Bluemix_notm}}.

Pour plus d'informations sur la configuration d'un connecteur JMX, voir [Configuring secure JMX connection to the Liberty profile ![icône de lien externe](../icons/launch-glyph.svg)](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}.

L'utilitaire *jmx* ne démarre pas proxy.

#### localjmx
{: #localjmx}

L'utilitaire *localjmx* active la fonction Liberty [localConnector-1.0 ![icône de lien externe](../icons/launch-glyph.svg)](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feature_localConnector-1.0.html){:new_window}. Combinée avec l'acheminement de port local, elle offre un autre moyen d'autoriser un client JMX distant à gérer l'application.

L'utilitaire *localjmx* est applicable uniquement pour les applications qui s'exécutent dans une cellule Diego. Pour utiliser *localjmx*, établissez d'abord l'acheminement de port à l'aide de la commande `cf ssh`. Exemple :

```
$ cf ssh -N -T -L 5000:127.0.0.1:5000 <nomApp>
```

Ensuite, pour vous connecter avec JConsole, choisissez "Remote Process",
indiquez `127.0.0.1:5000` et utilisez une connexion non
sécurisée.


### Les utilitaires ci-après prennent en charge Node.js seulement
{: #node_utilities}

#### inspector
{: #inspector}

Pour les versions de Node.js antérieures à la version 6.3.0,
*inspector* active l'interface du débogueur node inspector. Le processus *inspector* s'exécute dans votre conteneur d'applications. Servez-vous de cet utilitaire pour créer des profils d'utilisation de l'unité
centrale, ajouter des points d'arrêt et déboguer le code alors que votre application s'exécute dans {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations sur le module node inspector, voir [node-inspector on GitHub ![icône de lien externe](../icons/launch-glyph.svg)](https://github.com/node-inspector/node-inspector){:new_window}.

Pour Node.js versions 6.3.0 et ultérieures, *inspector* utilise [V8 Inspector Integration for Node.js ![icône de lien externe](../icons/launch-glyph.svg)](https://nodejs.org/dist/latest-v6.x/docs/api/debugger.html#debugger_v8_inspector_integration_for_node_js){:new_window}.

L'utilitaire inspector démarre *proxy* par défaut, mais le mode de débogage à distance dépend de la version de Node.js et de l'utilisation de *proxy* ou de *noproxy*.  Le tableau suivant indique comment accéder au débogage à distance dans les différents scénarios.

| | proxy | noproxy |
|---|---|---|
| < &nbsp; 6.3.0 | utilitaire devconsole *at*<br/> https://myApp.mybluemix.net/bluemix-debug/inspector | http://127.0.0.1:8790
| >= 6.3.0 | URL de chrome-devtools | URL de chrome-devtools

Pour *noproxy* et une version de Node.js antérieure à la
version 6.3.0, activez l'accès à l'URL via l'acheminement de port local. Exemple :

```
$ cf ssh -N -T -L <portLocal>:127.0.0.1:8790 <nomApp>
```

Accédez ensuite à http://127.0.0.1:8790 dans votre navigateur Web Chrome.  Modifiez le port en définissant la variable d'environnement
BLUEMIX_APP_MGMT_INSPECTOR :

```
$ cf set-env <nomApp> BLUEMIX_APP_MGMT_INSPECTOR='{port: 9790}'
```

Pour Node.js version 6.3.0 ou ultérieure, un message de journal indique
une URL qui peut être employée pour associer les outils Chrome
DevTools à votre application. Les messages du journal
sont similaires à l'exemple suivant :

```
  2016-11-30T16:40:56.03-0500 [APP/0]      OUT Starting app with 'node --inspect=9229  app.js '
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR Debugger listening on port 9229.
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR To start debugging, open the following URL in Chrome:
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR     chrome-devtools://devtools/remote/serve_file...
```

Activez l'accès à l'URL via l'acheminement de port local. Exemple :

```
$ cf ssh -N -T -L 9229:127.0.0.1:9229 <nomApp>
```

Vous aurez besoin d'une version à jour du navigateur Web Chrome pour
accéder à cette URL. Dans ce scénario, le proxy n'achemine pas le trafic à
l'inspecteur.

#### trace
{: #trace}

L'utilitaire *trace* vous permet de définir dynamiquement
des niveaux de trace si votre application utilise les modules de
journalisation *log4js*, *ibmbluemix* ou *bunyan*.

**Remarque :** Les versions de dépendance prises en charge sont :
* log4js : (0.6.0 à 0.6.24)
* bunyan : (1.0.0, 1.0.1, 1.1.0 à 1.1.3, 1.2.0 à 1.2.3, 1.3.0 à 1.3.5)
* ibmbluemix : (1.0.0-20140707-1250) à (1.0.0-20150409-1328)

Accédez à la page Détails de l'instance dans la console Web de {{site.data.keyword.Bluemix_notm}} et sélectionnez
**Actions** pour afficher l'interface utilisateur.

L'utilitaire *trace* n'est pas disponible si l'application a été démarrée avec l'option "-b buildpack".

L'utilitaire *trace* ne démarre pas *proxy*.

##  Configuration d'App Management
{: #configure}

Pour activer les utilitaires App Management, définissez la variable d'environnement *BLUEMIX_APP_MGMT_ENABLE*
et reconstituez votre application. Vous pouvez activer plusieurs utilitaires en les séparant par le signe plus "+".

Par exemple, pour activer les utilitaires *devconsole* et
*shell*, exécutez la commande suivante :

```
$ cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

Reconstituez votre application après avoir défini la variable d'environnement :

```
$ cf restage myApp
```

Si vous ne souhaitez pas que les utilitaires App Management soient installés avec votre application, associez la
variable d'environnement *BLUEMIX_APP_MGMT_INSTALL* à la valeur 'false' et reconstituez votre application.

Exemple :

```
$ cf set-env myApp BLUEMIX_APP_MGMT_INSTALL false
$ cf restage myApp
```

## Restrictions
{: #restrictions}

* App Management prend uniquement en charge les applications à
instance unique lorsque l'application s'exécute sur un noeud DEA.
* Les modifications que vous apportez à votre application avec App Management sont transitoires et sont perdues lorsque vous quittez ce mode. Ce mode a été conçu pour être utilisé temporairement au cours du développement et ne doit pas être utilisé dans un environnement de production en raison
de ses performances.
* La plupart des utilitaires App Management ne fonctionnent pas si vous
définissez votre commande de démarrage dans le fichier
`manifest.yml` (command) ou dans l'interface de ligne de
commande CF (-c). Ces méthodes constituent des remplacements de pack de construction et sont des anti-modèles pour le
démarrage des applications Node.js. Pour de meilleurs résultats, définissez la
commande de démarrage dans le fichier `package.json` ou dans `Procfile`.

## Mode développement pour Eclipse Tools
{: #devmode}

Le mode développement est une fonction d'[Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools) qui permet aux développeurs d'utiliser leurs applications lorsqu'elles s'exécutent dans le cloud.

Lorsqu'ils utilisent leurs applications dans {{site.data.keyword.Bluemix_notm}}, les développeurs peuvent
avoir l'impression de ne pas pouvoir effectuer les activités de développement habituelles qu'ils peuvent effectuer dans un
environnement local. Le mode développement d'Eclipse Tools résout ce problème en leur permettant de travailler dans le cloud, tout en se trouvant dans un espace de travail
sécurisé temporaire.

Le mode développement est pris en charge pour les applications Liberty et Node.js. Lorsqu'il est activé pour votre application Liberty ou Node.js,
vous pouvez mettre à jour des fichiers de façon incrémentielle sans avoir à envoyer votre application par commande push. Vous pouvez également établir une session de débogage pour votre application. Le
mode développement pour les applications Liberty équivaut à
activer les utilitaires d'App Management debug et jmx. Pour les applications Node.js, il équivaut à activer les utilitaires *devconsole*,
*inspector* et *shell*.
