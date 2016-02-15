{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}

#{{site.data.keyword.Bluemix_notm}} Live Sync {: #live-sync}

*Dernière mise à jour : 8 décembre 2015*  

Si vous construisez une application Node.js, vous pouvez utiliser {{site.data.keyword.Bluemix}} Live Sync pour mettre rapidement à jour
l'instance d'application dans {{site.data.keyword.Bluemix_notm}} et procéder au développement sans redéploiement, comme vous le feriez sur le bureau.   
{: shortdesc} 

Lorsque vous apportez une modification, vous pouvez immédiatement voir cette modification dans votre application
{{site.data.keyword.Bluemix_notm}} en cours d'exécution. {{site.data.keyword.Bluemix_notm}} Live Sync fonctionne depuis la ligne de
commande et dans l'environnement de développement intégré Web. Vous pouvez déboguer des applications écrites en Node.js avec
{{site.data.keyword.Bluemix_notm}} Live Sync.  

{{site.data.keyword.Bluemix_notm}} Live Sync se compose de trois fonctions. 

**Desktop Sync**  
    Vous pouvez synchroniser n'importe quelle arborescence de répertoires de bureau avec un espace de travail de projet reposant sur le cloud de la
même façon qu'avec Dropbox. L'environnement de développement intégré Web édite directement le même espace de travail reposant sur le cloud ; par conséquent, les deux restent
synchronisés. Desktop
Sync fonctionne pour tout type d'application. Pour pouvoir utiliser Desktop Sync, vous devez télécharger et installer l'interface de ligne de commande BL.  
	
**Live Edit**	
    Vous pouvez modifier une application Node.js qui s'exécute dans {{site.data.keyword.Bluemix_notm}} et tester immédiatement les modifications dans votre navigateur. Les modifications que vous apportez dans un répertoire de bureau synchronisé ou dans l'environnement de développement intégré Web sont immédiatement propagées dans le système de fichiers de l'application.  
	
**Debug**  
    Lorsqu'une application Node.js est en mode édition directe, vous pouvez ouvrir un shell et la déboguer. Vous pouvez éditer le code dynamiquement,
insérer des points d'arrêt, parcourir le code, redémarrer le contexte d'exécution, et effectuer d'autres opérations à l'aide du débogueur Node Inspector.  

Vous pouvez utiliser Desktop Sync pour que votre espace de travail de bureau reste synchronisé avec l'espace de travail de projet reposant sur le
cloud, que vous éditez directement dans l'environnement de développement intégré Web. Vous pouvez utiliser Live Edit pour propager les modifications apportées dans votre espace de travail de projet reposant sur le cloud de votre
application en cours d'exécution. Vous pouvez utiliser l'une de ces fonctions, ou les deux. De plus, si vous utilisez Desktop Sync ou Live Edit pour placer
votre application en mode édition directe, vous pouvez déboguer l'application en cours d'exécution.

Le processus Bluemix Live Sync est illustré dans le diagramme ci-dessous.	

*Figure 1. Le processus Bluemix Live Sync*
![Image du processus Bluemix Live Sync](images/bluemix-live-sync.png)
 
Si vous développez une application Java qui s'exécute dans Liberty, vous pouvez procéder au débogage à distance avec
[Eclipse Tools for Bluemix](../manageapps/eclipsetools/eclipsetools.html#eclipsetools).

##Desktop Sync {: #desktop-sync} 

Vous pouvez utiliser la fonction Desktop Sync de Bluemix Live Sync pour mettre rapidement à jour l'instance d'application dans {{site.data.keyword.Bluemix_notm}} et procéder au
développement, comme vous le feriez sur le bureau. 

Prenez connaissance des remarques suivantes relatives à Desktop Sync : 
* Desktop Sync s'exécute sur les systèmes d'exploitation suivants : 
  * Windows 7 ou 8
  * Mac OS X version 10.9 ou ultérieure
      **Remarque :** Windows requiert .NET Framework version 4.5. Si .NET n'est pas installé, vous êtes invité à l'installer lorsque
vous installez l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} Live Sync.  
* Il n'est pas nécessaire de cloner votre référentiel Git. 
* Quel que soit le type d'application que vous développez, vous pouvez synchroniser votre projet de bureau avec l'espace de travail de cloud. 
* Si votre application est écrite en Node.js, vous pouvez propager les applications à des applications en cours d'exécution.

Pour plus de détails sur les commandes, voir la [documentation sur l'interface de ligne de commande Bluemix
Live Sync](../cli/reference/bl/index.html). 

<ol>
<li>Téléchargez et installez la ligne de commande bl de {{site.data.keyword.Bluemix_notm}} Live Sync.   
<p>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/blive_setup.msi" target="_blank" title="(Ouverture dans un nouvel onglet ou une nouvelle fenêtre)"><img class="image" src="images/bl_gs_icons_windows_b.svg" alt="Bouton de téléchargement de la ligne de commande bl Windows" /> </a> <a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/BluemixLive.pkg" target="_blank" title="(Ouverture dans un nouvel onglet ou une nouvelle fenêtre)"><img class="image" src="images/bl_gs_icons_mac-osx_b.svg" alt="Bouton de téléchargement de la ligne de commande bl Mac" /> </a>
</p>  

<strong>Important :</strong> l'outil de ligne de commande bl est disponible uniquement pour Windows 7 et 8 et Mac OS X version 10.9 ou ultérieure. </li>
<li>Sur une ligne de commande, connectez-vous avec la commande ci-après. Vous serez invité à entrer votre ID IBM et votre mot de passe.  
<pre class="codeblock">bl login</pre>
</li>

<li>Affichez la liste des projets disponibles pour la synchronisation {{site.data.keyword.Bluemix_notm}} Live Sync en entrant la commande suivante
: 
<pre class="codeblock">bl projects</pre>
<p>Recherchez le nom de projet dans
la liste qui correspond à votre application. Le nom de projet est au format <i>votre alias</i> | <i>nom de-votre-application</i>. </p>
</li>
<li>Synchronisez votre environnement local avec votre projet dans {{site.data.keyword.Bluemix_notm}} à l'aide de la
commande ci-après. Si vous êtes le propriétaire du projet, il suffit de spécifier nom-de-votre-application pour nom_projet. 
<pre class="codeblock">bl sync
nom_projet -d répertoire_local --verbose</pre>
<p>Cette commande continue de s'exécuter (et la synchronisation continue) jusqu'à ce que vous entriez la lettre "q". L'option --verbose affiche les
informations de journalisation et de statut. Si l'un de vos arguments contient un espace, placez-le entre apostrophes. </p></li>
<li>Dans une autre fenêtre de ligne de commande, dans votre répertoire local, déployez l'application dans {{site.data.keyword.Bluemix_notm}} en
mode édition directe avec la commande suivante :
<pre class="codeblock">bl start</pre>
</li>
</ol>

Lorsque vous modifiez les fichiers dans votre répertoire local, les modifications sont propagées automatiquement dans l'application exécutée dans {{site.data.keyword.Bluemix_notm}} et dans l'espace de travail de cloud de projet. Si vous devez
redémarrer l'application de noeud, vous pouvez utiliser la commande suivante :
```
bl start --restart 
```

##Live Edit {: #live-edit} 

Si vous construisez une application Node.js, lorsque vous apportez des modifications à votre projet dans l'environnement de développement intégré Web,
la fonction Live Edit de {{site.data.keyword.Bluemix_notm}} Live Sync peut mettre à jour rapidement l'instance d'application qui s'exécute dans {{site.data.keyword.Bluemix_notm}}. Live Edit vous permet de procéder au développement comme sur le bureau, sans redéploiement. 

La fonction Live Edit est prise en charge uniquement pour les applications Node.js. 

Dans l'environnement de développement intégré Web, dans la barre d'exécution, cliquez sur **Live Edit**. 

![Image de la barre d'exécution avec Live Edit](images/run-bar-live-edit.png) 

Live Edit permet de prévisualiser rapidement les modifications apportées aux applications Node.js qui s'exécutent dans {{site.data.keyword.Bluemix_notm}}. Lorsque vous mettez à jour
votre code alors que la fonction Live Edit est activée, vous pouvez actualiser la fenêtre de navigateur de votre application Web pour afficher ces
modifications quelques secondes après les avoir effectuées. 

Pour suivre un tutoriel sur l'utilisation de la fonction Live Edit de {{site.data.keyword.Bluemix_notm}} Live Sync, voir
[Test and debug a Node.js app with Bluemix Live Sync](https://hub.jazz.net/tutorials/livesync).

Lorsque vous modifiez les fichiers dans votre environnement de développement intégré Web, ceux-ci sont redéployés automatiquement dans votre application
qui s'exécute dans {{site.data.keyword.Bluemix_notm}}. Si vous devez redémarrer l'application de noeud, vous pouvez utiliser le bouton **Redémarrer** dans la barre d'exécution.

##{{site.data.keyword.Bluemix_notm}} Live
Debug {: #live-debug}

Vous pouvez accéder à la fonction Debug de {{site.data.keyword.Bluemix_notm}} Live Sync lorsque {{site.data.keyword.Bluemix_notm}}
Live Sync est
activé pour votre application Node.js. 

La fonction debug permet d'éditer le code, d'insérer des points d'arrêt, de parcourir le code, de redémarrer le contexte d'exécution et d'effectuer
d'autres opérations de manière dynamique, pendant que votre application est exécutée par {{site.data.keyword.Bluemix_notm}}. Vous pouvez développer votre application de façon incrémentielle avec agilité en effectuant votre choix dans une longue liste de services
{{site.data.keyword.Bluemix_notm}}. 

{{site.data.keyword.Bluemix_notm}} Live
Debug inclut les fonctions suivantes :

* Le contrôle du contexte d'exécution d'application
* Le débogage avec [node-inspector](https://github.com/node-inspector/node-inspector)
* L'accès au shell 

###Contrôle du contexte d'exécution d'application {: #app-runtime} 

Avec le contrôle du contexte d'exécution d'application, vous pouvez utiliser la fonction Debug afin d'inspecter l'état de l'application
au démarrage. Cette capacité est utile lorsque vous traitez les incidents liés à une application qui tombe en panne au démarrage.

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

Cet outil permet d'accéder au conteneur dans lequel votre application est en cours d'exécution via un shell. Avec ce terminal, vous pouvez
exécuter des commandes shell de diagnostic à distance afin d'administrer votre application. 

Surveillez l'utilisation de la mémoire et de l'unité centrale dans l'instance qui utilise des commandes Linux standard, comme
**top**, **ps** et **kill**. 

###Configuration d'une application pour activer {{site.data.keyword.Bluemix_notm}}
Live
Debug {: #configure_app_debug} 

L'application doit utiliser le pack de construction IBM SDK for Node.js. Les packs de construction personnalisés ne sont pas pris en charge. 

1. Autorisez le pack de construction à détecter la commande de démarrage de l'application. La commande start doit être détectée automatiquement par
le pack de construction et ne doit pas être définie dans le fichier `manifest.yml`.  
    
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
	
Une fois {{site.data.keyword.Bluemix_notm}} Live
Debug installé, vous pouvez utiliser les outils de débogage.

Déployez l'application, puis ouvrez `https://hôte-app.mybluemix.net/bluemix-debug/manage` pour accéder à l'interface
utilisateur de débogage {{site.data.keyword.Bluemix_notm}}. Lorsque vous y êtes invité, entrez votre ID IBM et votre mot de passe pour vous
authentifier. 

###Restauration des configurations d'application et désactivation de Bluemix Live Debug {: #restore_live_debug} 

1. Supprimez la variable d'environnement ENABLE_BLUEMIX_DEV_MODE du fichier `manifest.yml` de l'application.

2. Restaurez la commande de démarrage et la valeur de mémoire d'origine de l'application. 

3. Déployez l'application.


># Liens connexes {:class="linklist"}
>## Tutoriels et exemples {:id="samples"}
>* [Test and debug a Node.js app with Bluemix Live Sync](https://hub.jazz.net/tutorials/livesync)
>
># Liens connexes {:class="linklist"}
>## Liens connexes {:id="general"}
>* [Commandes bl](https://www.ng.bluemix.net/docs/cli/bl_cli.html)   
>
>{:elementKind="article" id="rellinks"}
