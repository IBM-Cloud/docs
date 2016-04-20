---

 

copyright:

  years: 2015, 2016

 

---
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Interface de ligne de commande en mode développement 
{: #devmodecli}

*Dernière mise à jour : 25 février 2016*

Le mode développement (dev_mode) est une fonction Bluemix que vous pouvez utiliser pour gérer vos applications en cours d'exécution dans le
cloud. Il inclut l'interface de ligne de commande dev_mode. Celle-ci est construite comme un plug-in d'interface de ligne de commande cf et prend en
charge les
applications Liberty et IBM Node.js.

L'interface de ligne de commande dev_mode fournit les fonctions suivantes :
- Basculement de votre application entre le mode développement et le mode normal.
- Mise à jour des fichiers d'application de manière incrémentielle sans nouvelle commande push.
- Démarrage, arrêt ou redémarrage de votre application dans le conteneur existant.

## Initiation
**Conditions préalables :** avant de commencer, installez l'interface de ligne de commande Cloud Foundry. Pour plus de détails, voir [Start coding with Cloud Foundry command line interface](https://github.com/cloudfoundry/cli). 


Utilisez l'une des méthodes suivantes pour installer l'outil de ligne de commande dev_mode :
- Installation locale 
  1. Téléchargez le plug-in dev_mode correspondant à votre plateforme depuis le [référentiel de plug-in
de l'interface de ligne de commande IBM Bluemix](http://plugins.ng.bluemix.net).
  2. Installez le plug-in dev_mode à l'aide de la commande cf install-plugin :
  
        ```
        cf install-plugin dev_mode-linux_amd64
        ```

- Installation à partir du référentiel d'interface de ligne de commande Bluemix 
  1. Ajoutez le référentiel bluemix-repo aux référentiels d'interface de ligne de commande Cloud Foundry avec la commande suivante :
  
        ```
        cf add-plugin-repo bluemix-repo http://plugins.ng.bluemix.net
        ```

  2. Entrez cf repo-plugins. Le plug-in dev_mode apparaît dans le référentiel bluemix-repo.
		
		```
        cf repo-plugins
        ```
  
  3. Installez le plug-in dev_mode dans les plug-in d'interface de ligne de commande Cloud Foundry avec la commande suivante :
  
        ```
        cf install-plugin dev_mode -r bluemix-repo
        ```

## Syntaxe
**Pour afficher toutes les commandes de l'interface de ligne de commande dev_mode, utilisez la commande suivante :**

```
cf plugins
```

### Commandes dev_mode

### mode

```
cf mode <nom_app> <dev|normal>
```

Changez le mode d'application.

### statut

```
cf status <nom_app>
```

Affichez le mode d'application et le statut d'exécution.

### update-file

```
cf update-file <chemin_distant> <chemin_local> [options_commande]
```

Mettez à jour les fichiers d'application dans le cloud.

Options de commande :

**expand**

Indiquez si les fichiers téléchargés doivent être extraits du fichier zip.

**restart**

Redémarrez l'exécution de l'application une fois les fichiers mis à jour.
  
### delete-file

```
cf delete-file <chemin_distant> [options_commande]
```

Supprimez les fichiers d'application dans le cloud.

Options de commande :

**restart**

Redémarrez l'exécution de l'application une fois les fichiers supprimés.

### start-inplace

```
cf start-inplace <nom_app>
```

Démarrez l'application dans le conteneur existant.

### stop-inplace

```
cf stop-inplace <nom_app>
```

Arrêtez l'application dans le conteneur existant.

### restart-inplace

```
cf restart-inplace <nom_app>
```

Redémarrez l'application dans le conteneur existant.



### help

```
cf help <nom_commande>
```
Affichez l'aide relative à une commande.
