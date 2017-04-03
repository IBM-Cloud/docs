---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Traitement des incidents
{: #ts}

Certains problèmes connus rencontrés avec le plug-in {{site.data.keyword.dev_cli_notm}} sont documentés, et des solutions sont proposées.
{:shortdesc}

<!-- Add a headings and paragraphs about troubleshooting for your service, or a list of known issues and workarounds. -->

## Problèmes connus
{: #knownissues}

Les sections suivantes décrivent les problèmes connus et la façon dont ils peuvent être résolus.


### Erreur de nom d'hôte pris lors de la création d'un projet avec un modèle non mobile
{: #hostname}

L'erreur suivante peut s'afficher si vous utilisez le plug-in {{site.data.keyword.dev_cli_short}} pour créer un projet depuis les modèles Application Web, BFF ou Microservice :

```
The hostname <myHostname> is taken.
```
{: codeblock}


#### Cause
{: #hostname-cause}
   
Cette erreur est due à un jeton de connexion expiré.


#### Résolution
{: #hostname-resolution}

Connectez-vous à nouveau.

```
bx login
```
{: codeblock}


### Défaillances générales au niveau du plug-in {{site.data.keyword.dev_cli_short}}
{: #general}

L'erreur suivante peut s'afficher si vous utilisez les commandes create, delete, list ou code de {{site.data.keyword.dev_cli_short}} : 

```
Failed to <command> project.
```
{: codeblock}


#### Cause
{: #hostname-cause}
   
Cette erreur est due à un jeton de connexion expiré.


#### Résolution
{: #hostname-resolution}

Connectez-vous à nouveau.

```
bx login
```
{: codeblock}


### Erreur du courtier de service lors de l'ajout d'une fonctionnalité {{site.data.keyword.objectstorageshort}}
{: #os}

L'erreur suivante peut s'afficher si vous utilisez le plug-in {{site.data.keyword.dev_cli_short}} pour créer deux projets avec la fonctionnalité {{site.data.keyword.objectstorageshort}} :

```
FAILED
Service broker error: {"description"=>"You can not create this Object Storage instance. Each organization using the Object Storage service is limited to one instance of the Free plan."}
```
{: codeblock}


#### Cause
{: #os-cause}
   
Cette erreur est due au fait que le service {{site.data.keyword.objectstorageshort}} n'autorise qu'une instance du plan {{site.data.keyword.objectstorageshort}} gratuit.


#### Résolution
{: #os-resolution}

Choisissez un autre plan pour éviter cette erreur.


### Echec lors de l'obtention du code lors de la création d'un projet
{: #code}

L'erreur suivante peut s'afficher si vous utilisez le plug-in {{site.data.keyword.dev_cli_short}} pour créer un projet :
	
```
FAILED                            
Project created, but could not get code
https://console.ng.bluemix.net/developer/projects/b22165f3-cbc6-4f73-876f-e33cbec199d4/code
```
{: codeblock}
	

#### Cause
{: #code-cause}

Cette erreur est due à un dépassement de délai interne.
	

#### Résolution
{: #code-resolution}

Vous pouvez obtenir le code de l'une des façons suivantes :

* Exécutez la commande ci-après en utilisant l'interface de ligne de commande :

	```
	bx dev code <votre-nom-projet>
	```
	{: codeblock}
	
	`<votre-nom-projet>` doit être remplacé par le nom du projet que vous avez utilisé durant la création du projet.

* Utilisez la console {{site.data.keyword.dev_console}}.

	1. Sélectionnez votre [projet ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://console.{DomainName}/developer/projects) dans la console {{site.data.keyword.dev_console}} et cliquez sur la commande relative à l'obtention du code.

	2. Cliquez sur la commande de génération de code.

	3. Une fois le code généré, cliquez sur la commande de téléchargement du code.


### Erreur lors de l'exécution de `bx dev run` pour les projets Node.js
{: #node}

L'erreur suivante peut s'afficher si vous exécutez `bx dev run` avec des projets Web or BFF du plug-in {{site.data.keyword.dev_cli_short}} for Node.js :

```
module.js:597
  return process.dlopen(module, path._makeLong(filename));
                 ^

Error: /app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/appmetrics.node: invalid ELF header
    at Error (native)
    at Object.Module._extensions..node (module.js:597:18)
    at Module.load (module.js:487:32)
    at tryModuleLoad (module.js:446:12)

    at Function.Module._load (module.js:438:3)
    at Module.require (module.js:497:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/index.js:25:13)
    at Module._compile (module.js:570:32)
    at Object.Module._extensions..js (module.js:579:10)
```
{: codeblock}


#### Cause
{: #node-cause}
   
Cette erreur est due au fait que le module `appmetrics` est installé dans une architecture différente. Les modules npm natifs installés sur une architecture ne fonctionneront pas sur une autre architecture. Les images Docker incluses sont basées sur le noyau Linux.


#### Résolution
{: #node-resolution}

Supprimez le dossier `node_modules` et exécutez à nouveau `bx dev run`.


<!--
## Troubleshooting techniques
{: #tstechniques}
-->

<!-- Add a heading and content for how to get help and support. Use this template for beta and GA services:  -->


## Aide et support
{: #gettinghelp}

Si vous avez des problèmes ou des questions quand vous utilisez la console {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} ou le plug-in {{site.data.keyword.dev_cli_notm}}, vous pouvez obtenir de l'aide en recherchant des informations précises ou en posant des questions via un forum. Vous pouvez aussi ouvrir un ticket de demande de service.

Quand vous utilisez les forums pour poser une question, prenez soin d'étiqueter cette dernière de façon à ce qu'elle soit vue par les équipes de développement {{site.data.keyword.Bluemix_notm}}.

<!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->

Si vous avez des questions techniques sur le développement ou le déploiement d'une application avec la console {{site.data.keyword.dev_console}} ou le plug-in {{site.data.keyword.dev_cli_notm}} :

* Postez votre question sur [stackoverflow![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://stackoverflow.com/search?q=bluemix-dev-services+ibm-bluemix) et marquez votre question avec les étiquettes `bluemix-dev-services` et `ibm-bluemix`.
* Postez votre question sur [Slack ![Icône de lien externe](../icons/launch-glyph.svg "External link icon")](http://ibm-cloud-tech.slack.com/) sur le canal `bluemix-dev-services`. [Inscrivez-vous ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://ibm.biz/IBMCloudNativeSlack) maintenant.


<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
<!--
* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/bluemix-dev-services/?smartspace=bluemix) forum. Include the  "bluemix-dev-services" and "bluemix" tags.
* -->

Pour plus d'informations sur l'utilisation des forums, voir la rubrique décrivant [Comment obtenir de l'aide ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/support/index.html#getting-help).

Pour plus d'informations sur l'ouverture d'un ticket de demande de service {{site.data.keyword.IBM}}, sur les niveaux de support disponibles ou les niveaux de gravité des tickets, voir la rubrique décrivant [comment contacter le support![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/support/index.html#contacting-support).

<!--Add a heading and content for how to get help. (Support not available for experimental.) Use this template for experimental services:  -->

