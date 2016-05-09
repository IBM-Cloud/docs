---

 

copyright:

  2015，2016

 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Interface de ligne de commande en mode développement
{: #devmodecli}

*Dernière mise à jour : 11 avril 2016*

Via l'interface de ligne de commande en mode développement (CLI dev_mode), vous pouvez mettre à jour vos applications alors qu'elles s'exécutent dans le
cloud. Celle-ci est construite comme un plug-in d'interface de ligne de commande cf et prend en
charge les
applications Liberty et IBM Node.js.
{: shortdesc}
 

Vous pouvez effectuer les tâches suivantes à l'aide de l'interface CLI dev_mode :
- Basculement de votre application entre le mode développement et le mode normal.
- Mise à jour des fichiers d'application de manière incrémentielle sans nouvelle commande push.
- Démarrage, arrêt ou redémarrage de votre application dans le conteneur existant.

## Installation du plug-in dev_mode
**Conditions préalables :** avant de commencer, installez l'interface de ligne de commande Cloud Foundry. Pour plus de détails, voir [Start coding with Cloud Foundry command line interface](https://github.com/cloudfoundry/cli). 


Utilisez l'une des méthodes suivantes pour installer l'outil de ligne de commande dev_mode :
- Installation locale
  1. Téléchargez le plug-in dev_mode correspondant à votre plateforme depuis le [référentiel de plug-in
de l'interface de ligne de commande IBM Bluemix](http://plugins.{DomainName}).
  2. Installez le plug-in dev_mode à l'aide de la commande cf install-plugin :
  
        ```
        cf install-plugin dev_mode-linux_amd64
        ```

- Installez le plug-in depuis le référentiel CLI de Bluemix
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

## Affichage des commandes dev_mode
**Pour afficher toutes les commandes de l'interface CLI dev_mode, utilisez la commande suivante :**

```
cf plugins
```

## Index des commandes de l'interface CLI dev_mode
{: #dev_mode_cmds_index}

Utilisez l'index de la table suivante pour consulter les commandes CLI dev_mode fréquemment utilisées :

<table summary="Index des commandes dev_mode">
 <thead>
 <th colspan="4">Commandes dev_mode</th>
 </thead>
 <tbody> 
 <tr> 
 <td>[help](#help)</td> 
 <td>[mode](#mode)</td> 
 <td>[statut](#status)</td>
 <td>[update-file](#update_file)</td>
 </tr> 
 <tr> 
 <td>[delete-file](#delete_file)</td>
 <td>[start-inplace](#start_inplace)</td>
 <td>[stop-inplace](#stop_inplace)</td>
 <td>[restart-inplace](#restart_inplace)</td>
 </tr>
  </tbody> 
 </table> 
*Tableau 1. Commandes dev_mode*



## help
{: #help}

Affichez l'aide relative à une commande.

```
cf help <nom_commande>
```


## mode
{: #mode}

Changez le mode d'application.

```
cf mode <nom_app> <dev|normal>
```
<strong>Options de commande</strong> :

   <dl>
   <dt>dev</dt>
   <dd>Mode développement.</dd>
   <dt>normal</dt>
   <dd>Mode production.</dd>
   </dl>


## statut
{: #status}

Affichez le mode d'application et le statut d'exécution.
```
cf status <nom_app>
```



## update-file
{: #update_file}

Mettez à jour les fichiers d'application dans le cloud.

```
cf update-file <chemin_distant> <chemin_local> [options_commande]
```


<strong>Options de commande</strong> :

   <dl>
   <dt>expand</dt>
   <dd>Indiquez si les fichiers téléchargés doivent être extraits du fichier zip.</dd>
   <dt>restart</dt>
   <dd>Redémarrez l'exécution de l'application une fois les fichiers mis à jour.</dd>
   </dl>


  
## delete-file
{: #delete_file}

Supprimez les fichiers d'application dans le cloud.

```
cf delete-file <chemin_distant> [options_commande]
```


<strong>Options de commande</strong> :
 <dl>
   <dt>restart</dt>
   <dd>Redémarrez l'exécution de l'application une fois les fichiers mis à jour.</dd>
  </dl>


## start-inplace
{: #start_inplace}
Démarrez l'application dans le conteneur existant.

```
cf start-inplace <nom_app>
```



## stop-inplace
{: #stop_inplace}
Arrêtez l'application dans le conteneur existant.

```
cf stop-inplace <nom_app>
```



## restart-inplace
{: #restart_inplace}

Redémarrez l'application dans le conteneur existant.

```
cf restart-inplace <nom_app>
```



# Liens connexes
{: #rellinks}

## Liens connexes
{: #general}

<!-- Include a link to your full product documentation, pricing sheet, IBM Bluemix prerequisites -->


* [Interface de ligne de commande et outils de développement](../../index.html#cli){:new_window}


