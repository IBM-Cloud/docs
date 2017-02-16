---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-11"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 





# Traitement des incidents liés aux contextes d'exécution
{: #runtimes}



Vous pouvez rencontrer des problèmes lorsque vous utilisez les contextes d'exécution IBM® Bluemix.. Toutefois, dans de nombreux cas, ces problèmes peuvent être résolus en quelques opérations simples.
{:shortdesc}


## Pack de construction obsolète utilisé lorsqu'une application est envoyée par commande push
{: #ts_loading_bp}


Il est possible que vous ne puissiez pas utiliser les derniers composants
du pack de construction lorsque vous envoyez une application par commande push. Vous pouvez utiliser des packs de construction disposant de mécanismes intégrés
pour empêcher le chargement de composants obsolètes ou supprimer le contenu du répertoire cache de votre application avant
de l'envoyer par commande push ou de la reconstituer. 

 

Lorsque vous envoyez une application par commande push ou que vous la reconstituez une fois le pack de construction mis à jour, les composants les plus récents du pack de construction ne sont pas automatiquement chargés. Par conséquent, votre application utilise les composants obsolètes du pack de construction à partir du cache. Les mises à jour qui ont été appliquées au pack de construction depuis le dernier envoi de l'application par commande push ne sont pas implémentées. 
{: tsSymptoms}



Certains packs de construction ne sont pas configurés pour télécharger automatiquement sur internet tous les composants mis à jour afin de vous assurer de toujours utiliser la version la plus récente.
{: tsCauses} 

 

Vous pouvez utiliser des packs de construction disposant de mécanismes intégrés pour éviter de charger des composants obsolètes. Exemples de packs de construction : 
{: tsResolve}

  * [Pack de construction Java Cloud Foundry ![icône de lien externe](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/java-buildpack){: new_window}. Ce pack de construction comporte un mécanisme intégré qui permet de s'assurer d'utiliser la version la plus récente. Pour plus d'informations sur le fonctionnement de ce mécanisme, voir [extending-caches.md ![icône de lien externe](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}. 
  * [Pack de construction Node.js Cloud Foundry ![icône de lien externe](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}. Ce pack de construction a une fonctionnalité similaire qui utilise des variables d'environnement. Pour permettre au pack de construction Node.js de télécharger des modules de noeud sur internet à chaque fois, entrez la commande suivante dans l'interface de ligne de commande cf : 	
  ```
  set NODE_MODULES_CACHE=false
  ```
Si le pack de construction que vous utilisez ne dispose pas d'un mécanisme permettant de charger automatiquement les composants les plus récents,  vous pouvez supprimer manuellement le contenu du répertoire cache et envoyer à nouveau votre application par commande push en procédant comme suit :
  1. Réservez une branche d'un pack de construction null, par exemple https://github.com/ryandotsmith/null-buildpack. Pour plus d'informations sur la réservation d'une branche, voir [Git Basics - Getting a Git Repository ![icône de lien externe](../icons/launch-glyph.svg)](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}.  
  2. Ajoutez la ligne suivante au fichier `null-buildpack/bin/compile` et validez les modifications. Pour plus d'informations sur la validation des modifications, voir [Git Basics - Recording Changes to the Repository ![icône de lien externe](../icons/launch-glyph.svg)](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}.
  ```
  rm -rfv $2/*
  ```
  3. Envoyez votre application par commande push avec le pack de construction null modifié pour supprimer
le cache à l'aide de la commande suivante. Une fois cette étape réalisée, l'intégralité du contenu du répertoire cache de votre application est supprimée.
  ```
  cf push nom_app -p chemin_app -b <pack_construction_null_modifié>
  ```
  4. Envoyez votre application par commande push avec le pack de construction le plus récent que vous souhaitez utiliser à l'aide de la commande suivante : 
  ```
  cf push nom_app -p chemin_app -b <pack_construction_le_plus_récent>
  ```
  
	


## Messages NOTICE du pack de construction PHP
{: #ts_phplog}

Des messages contenant le terme NOTICE peuvent apparaître dans les journaux. Vous pouvez arrêter la journalisation de ces
messages en changeant le niveau de journalisation.	
	
 

Lorsque vous envoyez par commande push une application dans Bluemix à l'aide d'un pack de construction PHP, des messages contenant le terme
`NOTICE` peuvent s'afficher :
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: fpm is running, pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: ready to handle connections
```



Dans le pack de construction PHP, le paramètre error_log est utilisé pour définir le niveau de journalisation. Par défaut, la valeur du paramètre `error_log` est **stderr notice**. L'exemple
ci-dessous illustre la configuration du niveau de journalisation par défaut dans le fichier `nginx-defaults.conf` du pack de
construction PHP fourni par Cloud Foundry. Pour plus d'informations, voir [cloudfoundry/php-buildpack ![icône de lien externe](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}.
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```

 	
	
Les messages `NOTICE` sont informatifs et ne signalent pas nécessairement un problème. Vous pouvez arrêter la journalisation de ces messages en remplaçant le niveau de journalisation stderr notice par stderr error dans le fichier nginx-defaults.conf de votre pack de construction. Exemple : 	
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
Pour plus d'informations sur la modification de la configuration de journalisation par défaut, voir [error_log ![icône de lien externe](../icons/launch-glyph.svg)](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}.
	

## Impossible d'importer une bibliothèque Python tierce dans {{site.data.keyword.Bluemix_notm}}
{: #ts_importpylib}

Il se peut que vous ne puissiez pas importer une bibliothèque Python tierce dans {{site.data.keyword.Bluemix_notm}}. Vous pouvez résoudre le problème en ajoutant des fichiers de configuration dans le répertoire racine de votre application Python.


Lorsque vous essayez d'importer une bibliothèque Python tierce, par exemple la bibliothèque `web.py`, la commande `cf push` échoue.
{: tsSymptoms}


 

Ce problème survient lorsque les informations de configuration pour l'application Python manquent.
{: tsCauses}


 

Pour résoudre le problème, ajoutez un fichier `requirements.txt` et un fichier `Procfile` dans le répertoire racine de votre application Python. Les informations suivantes supposent que vous importiez la bibliothèque web.py :
{: tsResolve}

  1. Ajoutez un fichier `requirements.txt` dans le répertoire racine de votre application Python.
     Le fichier
`requirements.txt` spécifie les packages de bibliothèque requis pour votre application Python ainsi que la version des packages. L'exemple
ci-après illustre le contenu du fichier `requirements.txt`, où `web.py==0.37` indique que la version de la bibliothèque
`web.py` qui sera téléchargée est la version 0.37 et `wsgiref==0.1.2` indique que la version de l'interface Web de
Secure Gateway requise par la bibliothèque web.py est la version 0.1.2.
	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	Pour plus d'informations sur la configuration du fichier `requirements.txt`, voir [Requirements files](https://pip.readthedocs.org/en/1.1/requirements.html). 
	 
  2. Ajoutez un fichier `Procfile` dans le répertoire racine de votre application Python.
	Le fichier `Procfile`
contient la commande de démarrage de votre application Python. Dans la commande ci-dessous, *nom_de_votre_app* est le nom de votre application
Python et *PORT* est le numéro de port que votre application Python doit utiliser pour recevoir les demandes des utilisateurs de
l'application. *$PORT* est facultatif. Si vous ne spécifiez pas PORT dans la commande de démarrage, le numéro de port qui figure dans la
variable d'environnement `VCAP_APP_PORT` dans l'application est utilisé à la place. 
	```
	web: python <nom_de_votre_app>.py $PORT
	```
A présent, vous pouvez importer la bibliothèque Python tierce dans {{site.data.keyword.Bluemix_notm}}.	



## Le bouton Actions de la page Détails de l'instance est désactivé
{: #ts_actionsbutton}



Le bouton Actions de la page Détails de l'instance est désactivé.
{: tsSymptoms} 

 

Ce problème se produit pour l'une des raisons suivantes :
{: tsCauses}

  * L'application n'est pas une application Web Java™. L'utilitaire de gestion des ressources prend en charge uniquement les applications Web
déployées avec les packs de construction Liberty.
  * L'application n'est pas déployée avec le pack de construction Liberty imbriqué.
  * L'application a été déployée avec une ancienne version du pack de construction Liberty.



Si l'application a été déployée avec une ancienne version du pack de construction Liberty, redéployez l'application dans {{site.data.keyword.Bluemix_notm}}. Sinon, vous pouvez transmettre les fichiers journaux d'application client suivants à l'équipe de support :
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
  

  
  
## Les données d'identification sont requises lors de l'ouverture d'une fenêtre de trace ou de vidage
{: #ts_username}


 

Un nom d'utilisateur et un mot de passe sont requis lors de l'ouverture de la fenêtre de trace et de vidage.
{: tsSymptoms}

 

Ce problème se produit à cause du dépassement de délai d'attente de la session de connexion.
{: tsCauses}

 

Entrez à nouveau le nom d’utilisateur et le mot de passe.
{: tsResolve}




## Des erreurs surviennent lors de l'exécution d'opérations de trace ou de vidage
{: #ts_target}

 

Un message d'erreur s'affiche lorsque des opérations de trace ou de vidage sont en cours. Ce message indique qu'une instance cible d'une application n'est pas à l'état en cours :	
{: tsSymptoms}

```
Instance 0 : La définition de la spécification de trace a abouti
Instance 2 : La définition de la spécification de trace a abouti
Instance 1 : L'instance cible 1 pour l'application abcd n'est pas à l'état en cours.
Instance 3 : La définition de la spécification de trace a abouti
Instance 4 : La définition de la spécification de trace a abouti
```



Ce problème se produit pour l'une des raisons suivantes :
{: tsCauses} 

  * Les fonctionnalités de trace ou de vidage s'appliquent uniquement aux instances d'application en cours d'exécution. Les opérations de trace ou de vidage ne peuvent pas être utilisées sur des instances d'application arrêtées, en cours de démarrage ou en panne.
  * Le statut de l'instance d'application change lorsque la boîte de dialogue de trace ou de vidage est ouverte. 
  


La solution consiste à fermer la fenêtre, puis à la rouvrir.
{: tsResolve} 



## Les instances possèdent une configuration traceSpecification différente
{: #ts_different_config}

 

Il peut exister différentes configurations traceSpecification pour différentes instances d'une seule application.
{: tsSymptoms}

 

Ce problème se produit pour l'une des raisons suivantes :
{: tsCauses}

  * Il se peut que vous ayez changé la configuration pour une ou plusieurs instances précédemment. Si vous changez la configuration traceSpecification pour une instance, cette configuration ne s'applique pas aux autres instances de la même application. Par exemple, votre application utilise log4j et il existe deux instances pour cette application. Vous
pouvez remplacer le niveau de journalisation info de l'instance 0 par debug ; toutefois, le niveau de journalisation de l'instance 1 reste info. 
  * L'application s'étend et possède de nouvelles instances. L'utilitaire de gestion des ressources n'applique pas la configuration
traceSpecification de l'instance existante à la
nouvelle instance ajoutée. La nouvelle instance utilise la configuration par défaut. Par exemple, votre application utilise log4j et possède une instance. Vous
pouvez remplacer le niveau de journalisation info de cette instance par debug. Après cette modification, si vous étendez votre application à deux
instances, le niveau de journalisation de la nouvelle instance est info, et non debug.
  


Ce comportement est normal.
{: tsResolve} 





## Quota de disque dépassé
{: #ts_diskquota}

Vous pouvez constater, dans votre journal d'application, que le quota de disque est dépassé.

 

Le message d'erreur `Disk quota exceeded` figure dans le journal de votre application.
{: tsSymptoms}



Ce problème survient pour l'une des raisons suivantes : 
{: tsCauses} 

  * Les fichiers de vidage sont générés avec les instances d'application en cours d'exécution ; le quota de disque alloué est dépassé. Par défaut, le quota de disque pour une instance d'application est de 1 Go. Vous
pouvez vérifier l'utilisation de votre disque en cliquant sur **Tableau de
bord > Application > Contexte d'exécution de l'application**. L'exemple suivant montre
les informations de contexte d'exécution, notamment l'utilisation du disque, pour deux instances d'une application :
    ```
    Instance	State	CPU	Memory Usage	Disk Usage

	0		Running	1.0%	344.8MB/512MB	236.8MB/1GB
	2		Running	2.3%	361.2MB/512MB	235.7MB/1GB
    ```
  * Le quota de disque est limité par le quota de l'organisation.
  
  


Vous pouvez résoudre ce problème en suivant l'une des méthodes ci-dessous :
{: tsResolve} 

  * Supprimez les fichiers de vidage après les avoir téléchargés.
  * Redéployez l'application avec un quota de disque plus important en insérant l'entrée suivante dans le manifeste de déploiement :
    ```
	disk_quota: 2048
	```
	
	
<!-- begin STAGING ONLY --> 

	
## Les objets de consignateur Log4js ne sont pas affichés dans la fenêtre en incrustation Node.js Trace
{: #ts_logger}

Les objets de consignateur Log4js ne sont pas affichés dans la fenêtre en incrustation Node.js Trace lorsque les modules log4js et ibmbluemix sont utilisés dans votre application. 	

 
Les objets de consignateur Log4js ne sont pas affichés dans la fenêtre en incrustation Node.js Trace lorsque les modules log4js, winston et ibmbluemix sont utilisés dans votre application.
{: tsSymptoms}


Etant donné que le module ibmbluemix fournit une API unifiée pour les opérations de consignation qui utilisent les modules log4js et winston, seuls les objets de consignateur ibmbluemix sont affichés dans la fenêtre en incrustation Node.js Trace. Ainsi, les paramètres de niveau de consignation des objets de consignateur ibmbluemix, log4js et winston ne s'écrasent pas mutuellement.
{: tsCauses}


Ce comportement est normal.
{: tsResolve}

<!-- end STAGING ONLY -->




<!-- begin STAGING ONLY -->


## L'option Apply trace setting to all instances of the application est désactivée
{: #ts_bunyan}

L'option **Apply trace setting to all instances of the application** est désélectionnée et désactivée dans la fenêtre en incrustation Node.js Trace lorsque les niveaux de consignateur Bunyan sont modifiés.



Lorsque vous modifiez les niveaux des objets de consignateur Bunyan, l'option **Apply trace setting to all instances of the application** est désélectionnée et désactivée dans la fenêtre en inscrustation Node.js Trace.
{: tsSymptoms} 

 

Lorsque les niveaux de consignation Bunyan sont modifiés, le paramètre de trace ne peut pas être appliqué à toutes les instances d'une application. Cela est dû au fait que la bibliothèque Bunyan n'exige pas que les noms ou les identificateurs des objets de consignateur Bunyan soient uniques. Plusieurs objets de consignateur Bunyan utilisés pour spécifier des niveaux dans les messages de journal de votre application peuvent avoir le même nom ou le même identificateur. Par conséquent, si le paramètre de trace est activé pour une application, les niveaux de consignation indiqués dans les messages de journal de l'application peut être inexacts.
{: tsCauses}




Ce comportement est normal.
{: tsResolve} 

<!-- end STAGING ONLY -->

