# Interface CLI Bluemix dev_mode 
Le mode développement est une fonction Bluemix que vous pouvez utiliser avec vos applications alors qu'elles sont en cours d'exécution dans le cloud. Cette fonction inclut l'interface de ligne de commande dev_mode. L'interface CLI dev_mode CLI est construite comme un plug-in CLI cf et prend en charge les applications Liberty et IBM Node.js.

L'interface CLI dev_mode fournit les fonctions suivantes :
- Basculement de votre application entre le mode dev et le mode normal.
- Mise à jour des fichiers d'application de manière incrémentielle sans nouvelle commande push.
- Démarrage, arrêt ou redémarrage de votre application dans le conteneur existant. 

## Initiation
**Conditions préalables :** Avant de commencer, installez l'interface CLI Cloud Foundry. Pour plus de détails, voir  [Start coding with Cloud Foundry command line interface](https://github.com/cloudfoundry/cli). 


Utilisez l'une des méthodes suivantes pour installer l'outil de ligne de commande dev_mode :
- Installation en local. 
  1. Téléchargez le plug-in dev_mode correspondant à votre plateforme depuis [IBM Bluemix CLI Plugin Repository](http://plugins.ng.bluemix.net).
  2. Installez le plug-in dev_mode à l'aide de la commande cf install-plugin :
  
        ```
        cf install-plugin dev_mode-linux_amd64
        ```

- Installation à partir du référentiel d'interface CLI Bluemix CLI.
  1. Ajoutez le référentiel bluemix-repo aux référentiels d'interface CLI Cloud Foundry à l'aide de la commande suivante :
  
        ```
        cf add-plugin-repo bluemix-repo http://plugins.ng.bluemix.net
        ```

  2. Entrez cf repo-plugins. Le plug-in dev_mode apparaît dans le référentiel bluemix-repo.
		
		```
        cf repo-plugins
        ```
  
  3. Installez le plug-in dev_mode dans les plug-in d'interface CLI Cloud Foundry à l'aide de la commande suivante :
  
        ```
        cf install-plugin dev_mode -r bluemix-repo
        ```

## Utilisation
**Pour afficher toutes les commandes CLI dev_mode, utilisez la commande suivante :**

```
cf plugins
```

### Commandes dev_mode

### mode

```
cf mode <appName> <dev|normal>
```

Changez le mode d'application.

### statut

```
cf status <appName>
```

Affichez le mode d'application et le statut d'exécution.

### update-file

```
cf update-file <remotePath> <localPath> [command_options]
```

Mettez à jour les fichiers d'application dans le cloud.

Options de commande :

**expand**

Indiquez si les fichiers téléchargés doivent être extraits du fichier zip.

**restart**

Redémarrez l'exécution de l'application une fois les fichiers mis à jour. 
  
### delete-file

```
cf delete-file <remotePath> [command_options]
```

Supprimez les fichiers d'application dans le cloud.

Options de commande :

**restart**

Redémarrez l'exécution de l'application une fois les fichiers supprimés. 

### start-inplace

```
cf start-inplace <appName>
```

Démarrez l'application dans le conteneur existant. 

### stop-inplace

```
cf stop-inplace <appName>
```

Arrêtez l'application dans le conteneur existant. 

### restart-inplace

```
cf restart-inplace <appName>
```

Redémarrez l'application dans le conteneur existant. 



### help

```
cf help <commandName>
```
Affichez l'aide relative à une commande. 
