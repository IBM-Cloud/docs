---



copyright:
  years: 2015，2017
lastupdated: "2017-3-10"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}

#{{site.data.keyword.Bluemix_notm}} Live Sync
{: #live-sync}

 
Si vous construisez une application Node.js, vous pouvez utiliser {{site.data.keyword.Bluemix}} Live Sync pour mettre rapidement à jour l'instance d'application dans {{site.data.keyword.Bluemix_notm}} et procéder au développement sans avoir à effectuer un redéploiement manuel.    
{: shortdesc}

Lorsque vous apportez une modification, vous pouvez immédiatement voir cette modification dans votre application {{site.data.keyword.Bluemix_notm}} en cours d'exécution. {{site.data.keyword.Bluemix_notm}} Live Sync fonctionne 
<!--from both the command line and -->
dans l'interface IDE Web Eclipse Orion. Vous pouvez déboguer des applications écrites en Node.js avec {{site.data.keyword.Bluemix_notm}} Live Sync.  

{{site.data.keyword.Bluemix_notm}} Live Sync se compose de deux fonctions. 
<!-- three -->

<!--
**Desktop Sync**  

You can synchronize any desktop directory tree with a cloud-based project workspace similar to the way Dropbox works. The Web IDE directly edits the same cloud-based workspace, so both stay in sync. Desktop Sync works for any kind of application. To use Desktop Sync, you need to download and install the BL command line interface.  
-->

**Live Edit**

Vous pouvez modifier une application Node.js qui s'exécute dans {{site.data.keyword.Bluemix_notm}} et tester immédiatement les modifications dans votre navigateur. Les modifications que vous apportez dans l'interface IDE Web sont immédiatement propagées dans le système de fichiers de l'application.  

**Debug**  

Lorsqu'une application Node.js est en mode édition directe, vous pouvez ouvrir un shell et la déboguer. Vous pouvez éditer le code dynamiquement, insérer des points d'arrêt, parcourir le code, redémarrer le contexte d'exécution, et effectuer d'autres opérations à l'aide du débogueur Node Inspector.  

<!-- You can use Desktop Sync to keep your desktop workspace in sync with the cloud-based project workspace that you edit directly with the Web IDE. -->

Vous pouvez utiliser Live Edit pour propager les modifications apportées dans votre espace de travail de projet reposant sur le cloud de votre application en cours d'exécution. 
<!-- You can use one or both of these features. And if you use Desktop Sync or -->
Si vous utilisez Live Edit pour placer votre application en mode édition directe, vous pouvez déboguer l'application en cours d'exécution.


Le processus Bluemix Live Sync est illustré dans le diagramme ci-dessous.    

Figure 1. Le processus Bluemix Live Sync
    

![Image du processus Bluemix Live Sync](images/bluemix-live-sync.png)

Si vous développez une application Java qui s'exécute dans Liberty, vous pouvez procéder au débogage à distance avec [Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools).


##Live Edit {: #live-edit}

Si vous construisez une application Node.js, lorsque vous apportez des modifications à votre projet dans l'environnement de développement intégré Web, la fonction Live Edit de {{site.data.keyword.Bluemix_notm}} Live Sync peut mettre à jour rapidement l'instance d'application qui s'exécute dans {{site.data.keyword.Bluemix_notm}}. Live Edit vous permet de procéder au développement comme sur le bureau, sans redéploiement.

La fonction Live Edit est prise en charge uniquement pour les applications Node.js.

Dans l'interface IDE Web Eclipse Orion, dans la barre d'exécution, cliquez sur **Live Edit**.

![Image de la barre d'exécution avec Live Edit](images/bluemix-live-sync-light.png)

Live Edit permet de prévisualiser rapidement les modifications apportées aux applications Node.js qui s'exécutent dans {{site.data.keyword.Bluemix_notm}}. Lorsque vous mettez à jour votre code alors que la fonction Live Edit est activée, vous pouvez actualiser la fenêtre de navigateur de votre application Web pour afficher ces modifications quelques secondes après les avoir effectuées.

<!--
For a tutorial on using the Live Edit feature of {{site.data.keyword.Bluemix_notm}} Live Sync, see the tutorial [Test and debug a Node.js app with Bluemix Live Sync![External link icon](../icons/launch-glyph.svg "External link icon")](https://hub.jazz.net/tutorials/livesync){:new_window}.
-->

Lorsque vous modifiez les fichiers dans votre environnement de développement intégré Web, ceux-ci sont redéployés automatiquement dans votre application qui s'exécute dans {{site.data.keyword.Bluemix_notm}}. Si vous devez redémarrer l'application de noeud, vous pouvez utiliser le bouton **Redémarrer** dans la barre d'exécution.

**REMARQUE :** pour une expérience plus cohérente lors de l'utilisation de la fonction Live Edit de {{site.data.keyword.Bluemix_notm}} Live Sync, 256 Mo de mémoire supplémentaire sont requis et seront ajoutés.

##{{site.data.keyword.Bluemix_notm}} Live Debug {: #live-debug}

Vous pouvez accéder à la fonction Debug de {{site.data.keyword.Bluemix_notm}} Live Sync lorsque {{site.data.keyword.Bluemix_notm}} Live Sync est activé pour votre application Node.js.

La fonction debug permet d'éditer le code, d'insérer des points d'arrêt, de parcourir le code, de redémarrer le contexte d'exécution et d'effectuer d'autres opérations de manière dynamique, pendant que votre application est exécutée par {{site.data.keyword.Bluemix_notm}}. Vous pouvez développer votre application de façon incrémentielle avec agilité en effectuant votre choix dans une longue liste de services {{site.data.keyword.Bluemix_notm}}.

{{site.data.keyword.Bluemix_notm}} Live Debug inclut les fonctions suivantes :

* Le contrôle du contexte d'exécution d'application
* Le débogage à l'aide de [node-inspector![](../icons/launch-glyph.svg "")](https://github.com/node-inspector/node-inspector){:new_window}
* L'accès au shell

###Contrôle du contexte d'exécution d'application {: #app-runtime}

Avec le contrôle du contexte d'exécution d'application, vous pouvez utiliser la fonction Debug afin d'inspecter l'état de l'application au démarrage. Cette capacité est utile lorsque vous traitez les incidents liés à une application qui tombe en panne au démarrage.

Lorsque vous développez votre application, vous pouvez choisir une action parmi les suivantes :

* Procéder à un redémarrage rapide de l'application
* Suspendre l'application avant l'exécution du code de l'application

###Debug {: #debug}

La fonction Debug inclut les capacités suivantes :

**Restriction :** Google Chrome est requis.

* Définir des points d'arrêt dans le code de l'application pour interrompre l'exécution à une ligne spécifique.
* Editer les conditions de point d'arrêt pour interrompre l'exécution uniquement lorsque certains critères sont remplis.
* Inspecter l'état des zones et des variables locales.
* Afficher immédiatement la sortie de débogage des appels de `console.log()`. Cette action est plus rapide que la surveillance des journaux cf.
* Utiliser l'éditeur de code source intégré pour apporter des modifications immédiates mais temporaires au code d'application en cours d'exécution.

###Shell {: #shell}

Cet outil permet d'accéder au conteneur dans lequel votre application est en cours d'exécution via un shell. Avec ce terminal, vous pouvez exécuter des commandes shell de diagnostic à distance afin d'administrer votre application.

Surveillez l'utilisation de la mémoire et de l'unité centrale dans l'instance qui utilise des commandes Linux standard, comme **top**, **ps** et **kill**.

###Configuration d'une application pour activer {{site.data.keyword.Bluemix_notm}} Live Debug {: #configure_app_debug}

L'application doit utiliser le pack de construction IBM SDK for Node.js. Les packs de construction personnalisés ne sont pas pris en charge.

1. Autorisez le pack de construction à détecter la commande de démarrage de l'application. La commande start doit être détectée automatiquement par le pack de construction et ne doit pas être définie dans le fichier `manifest.yml`.  

    a. Vérifiez que le fichier `package.json` contient un script de démarrage, qui inclut une commande start pour l'application.  
    b. Si le fichier `manifest.yml` de l'application contient une commande, définissez la valeur null.  

2. Définissez la variable d'environnement.  

    a. Dans le fichier `manifest.yml`, ajoutez la variable suivante :
	```
	env:
      ENABLE_BLUEMIX_DEV_MODE: "true"
	```

3. Augmentez la mémoire.  

    a. Dans le fichier `manifest.yml` de l'application, ajoutez 128M ou plus à la valeur spécifiée pour l'attribut de mémoire :

Une fois {{site.data.keyword.Bluemix_notm}} Live Debug installé, vous pouvez utiliser les outils de débogage.

Déployez l'application, puis ouvrez `https://app-host.mybluemix.net/bluemix-debug/manage` pour accéder à l'interface utilisateur de débogage {{site.data.keyword.Bluemix_notm}}. Lorsque vous êtes invité à vous authentifier, entrez votre ID utilisateur et votre jeton d'accès personnel ou votre mot de passe IBMid.    

<!--
   **Note**: Your user ID for DevOps Services can be either an IBMid or a federated ID (corporate ID). If you use federated authentication, to log in to your Bluemix Live Sync command-line client, you must use a personal access token instead of a password. If you don't use federated authentication, your IBMid and password work with all clients. For more information about creating a personal access token, see [What's federated authentication and how does it affect me?![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/devops-services/2016/06/23/whats-federated-authentication-and-how-does-it-affect-me/){:new_window}
   -->

###Restauration des configurations d'application et désactivation de Bluemix Live Debug {: #restore_live_debug}

1. Supprimez la variable d'environnement ENABLE_BLUEMIX_DEV_MODE du fichier `manifest.yml` de l'application.

2. Restaurez la commande de démarrage et la valeur de mémoire d'origine de l'application.

3. Déployez l'application.


## Liens connexes
{: #general}

* [Eclipse tools for Bluemix![](../icons/launch-glyph.svg "")](https://www.ng.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html){:new_window}
