{:new_window: target="_blank"}

# Commencer à utiliser {{site.data.keyword.objectstorageshort}}  {: #using-object-storage} 

*Dernière mise à jour : 24 juin 2016*
{: .last-updated}


## Utilisation de l'interface utilisateur {{site.data.keyword.objectstorageshort}} {: #using-object-storage-ui}

### Eléments d'interface utilisateur et navigation
Quand {{site.data.keyword.objectstorageshort}} est provisionné, vous pouvez voir vos informations d'instance dans {{site.data.keyword.objectstorageshort}} pour le tableau de bord d'instance de service {{site.data.keyword.Bluemix_notm}}. Depuis le tableau de bord, sélectionnez votre instance {{site.data.keyword.objectstorageshort}} pour afficher le panneau avec des informations plus détaillées.  
#### Données d'utilisation
La page d'accueil de votre application contient des informations sur l'utilisation du stockage pour votre instance. A cet emplacement s'affichent aussi le nombre actuel de **conteneurs de stockage** et le nombre total d'**objets** dans tous vos conteneurs. Votre utilisation de la mémoire en mégaoctets est aussi indiquée. L'espace de **stockage consommé** se réfère au volume actuel d'espace qui est utilisé. 
#### Actions
Pour extraire les dernières données d'utilisation, cliquez sur le bouton **Actualiser**.   
####Navigateur d'objet 
Utilisez ce dernier pour gérer les objets et conteneurs de stockage d'objets. Vous pouvez créer des conteneurs, télécharger des fichiers, supprimer des conteneurs ou des fichiers, et effectuer d'autres actions.


## Utilisation de {{site.data.keyword.objectstorageshort}} depuis une application {{site.data.keyword.Bluemix_notm}} {: #using-object-storage-from-bluemix-app} 

### Comment lier votre service {{site.data.keyword.objectstorageshort}} à une application après création ? {: #bind-object-storage-to-application} 
1.	Sur le tableau de bord {{site.data.keyword.Bluemix_notm}}, sélectionnez l'application que vous voulez lier.
2.	Dans la vue d'ensemble de l'application, cliquez sur **Lier un service ou une API**.
3.	Sélectionnez votre instance {{site.data.keyword.objectstorageshort}} dans la liste des services et cliquez sur **Ajouter**.
4.	Cliquez sur **Reconstituer** quand vous y êtes invité. Votre application doit être reconstituée pour utiliser le nouveau service.

### Contexte lié

Si vous voulez utiliser {{site.data.keyword.objectstorageshort}} dans un contexte lié, les données d'identification du cloud sont fournies indirectement via le processus de liaison d'application. Après avoir lié une instance de service à votre application, une configuration similaire à celle de l'exemple suivant est ajoutée à votre variable d'environnement `VCAP_SERVICES`.

    {
    "Object-Storage": [
    {
      "name": "Object-Storage - YP",
      "label": "Object-Storage",
      "plan": "Free",
      "credentials": {
         "auth_url": "https://identity.open.softlayer.com",
         "project": "object_storage_d049255b",
         "projectId": "0f47b41b06d047f9aae3b33f1db061ed",
         "region": "dallas",
         "userId": "ad78b2a3f843466988afd077731c61fc",
         "username": "user_202db1f8a7aa3f3ac51ec68f10dbe7dc29070bc7",
         "password": "K/jyIi2jR=1?D.TP",
         "domainId": "2df6373c549e49f8973fb6d22ab18c1a",
         "domainName": "639347"
        }
       }
      ]
    }


## Utilisation de l'interface de ligne de commande Swift pour accéder à {{site.data.keyword.objectstorageshort}} {: #using-swift-cli}

Vous pouvez accéder au service {{site.data.keyword.objectstorageshort}} sur Internet et à partir d'applications et de serveurs virtuels
dans IBM {{site.data.keyword.Bluemix_notm}}. Des cas d'utilisation courants du service {{site.data.keyword.objectstorageshort}} sont présentés ci-dessous :

* Sauvegarde de données de volume depuis vos instances
* Utilisation d'un emplacement intermédiaire lors du transfert de volumes importants de données
* Transfert de données entre des environnements non directement connectés
* Rôle de référentiel central

Le service {{site.data.keyword.objectstorageshort}}, qui repose sur OpenStack Swift, est accessible via une application client compatible. Cette
section explique comment se servir du client Python Swift, qui est l'interface de ligne de commande pour l'API
{{site.data.keyword.objectstorageshort}} et ses extensions, pour utiliser des conteneurs et des fichiers.

### Installation du client Swift {: #install-swift-client}

Installez les logiciels prérequis suivants, si ce n'est pas déjà fait. Pour plus d'informations, voir la [documentation OpenStack](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}. 
* Python 2.7 ou ultérieur
* Package setuptools
* Package pip

Installez le client Python Swift en utilisant Python pip :

	sudo pip install python-swiftclient

### Configuration du client {: #setup-swift-client}

Le client Swift prend les informations d'authentification dans les variables d'environnement suivantes :
* ```OS_AUTH_URL``` est l'adresse URL du noeud final 
* ```OS_USER_ID``` est le nom d'utilisateur
* ```OS_PASSWORD``` est le mot de passe

Définissez les informations d'authentification comme suit. 

	export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
	export OS_PASSWORD=aaa55AAAaaaaa]?,
	export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
	export OS_AUTH_URL=https://identity.open.softlayer.com/v3
	export OS_REGION_NAME=dallas
	export OS_IDENTITY_API_VERSION=3
	export OS_AUTH_VERSION=3

Vous pouvez trouver les valeur de données d'identification pour votre service {{site.data.keyword.objectstorageshort}} sur la page **Données d'identification pour le service** de l'interface utilisateur {{site.data.keyword.objectstorageshort}} 

**Remarque :** assurez-vous d'ajouter ```/v3``` à ```auth_url``` depuis les données
d'identification dans l'interface utilisateur {{site.data.keyword.objectstorageshort}} lorsque vous configurez les variables d'environnement ```OS_AUTH_URL``` pour
le client Swift.



### Utilisation des conteneurs {: #work-with-containers}

Création d'une liste des conteneurs :

	swift list
	
Création d'un conteneur :

	swift post <nom_conteneur>
	
Création d'une liste du contenu d'un conteneur :

	swift list <nom_conteneur>

### Utilisation des objets {: #work-with-objects}

#### Ajout d'un fichier à un conteneur

	swift upload <nom_conteneur> <nom_fichier>

#### Ajout dans un conteneur d'un fichier supérieur à 5 Go

Si vous téléchargez un fichier qui fait plus de 5 Go, vous devez le diviser en parties plus petites. Vous pouvez demander au client Swift de gérer un
téléchargement de ce type en fournissant le paramètre ```-segment-size` :

	swift upload <nom_conteneur> <nom_fichier> --segment-size <taille_en_octets>
	
Chaque segment est téléchargé en parallèle dans un conteneur distinct nommé ```<nom_conteneur>_segments`. Une fois tous
les segments transférés, Swift crée un fichier manifeste de façon à ce que les segments puissent être téléchargés dans un fichier unique à partir
du conteneur d'origine ```<nom_conteneur>``` avec le nom de fichier d'origine ```<nom_fichier>```.

Par exemple, la commande suivante télécharge un fichier nommé ```grand_fichier ``` depuis un conteneur nommé ```conteneur_test``` avec
la taille de segment ```1073741824```.

	swift upload conteneur_test -S 1073741824 grand_fichier 

Vous pouvez exécuter la commande suivante pour télécharger le fichier :

	swift download conteneur_test grand_fichier

#### Téléchargement d'un fichier

	swift download <nom_conteneur> <nom_fichier>
	
#### Ajout d'un répertoire à un conteneur

Swift n'a pas de véritable structure de répertoires, mais utilise la désignation pour en représenter une. Pour ajouter un répertoire à un conteneur, exécutez la commande suivante :

	swift upload <nom_conteneur> <nom_répertoire>
	
Cette commande télécharge la structure de répertoire complète en tant que chemin relatif. Par exemple, si vous spécifiez ```/mnt/volume1```,
la structure de répertoire mnt/volume1 est jointe à tous les noms de fichier pour indiquer la structure de répertoire. 

	
#### Téléchargement d'un répertoire

Pour télécharger une structure de répertoire, utilisez le paramètre ```-prefix``` afin d'indiquer le répertoire ou la
structure de répertoire à télécharger.


	swift download <nom_conteneur> --prefix <répertoire>
	
#### Suppression d'un fichier

	swift delete <nom_conteneur> <nom_fichier>

### Utilisation de la gestion des versions d'objet {: #work-with-object-versioning}

Vous pouvez configurer des versions de chaque objet dans votre conteneur avec l'indicateur ```X-Versions-Location```. Pour ce
faire, créez un conteneur supplémentaire dans lequel placer les anciennes versions de vos objets comme suit.
 

Si vous utilisez le client Swift, vous pouvez entrer la commande suivante : 

	swift post conteneur_un -H "X-Versions-Location:conteneur_deux"

Si vous utilisez curl, vous pouvez entrer la commande suivante : 

	curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:conteneur_deux" https://<url-stockage-objet>/conteneur_un

Dans l'exemple, ```conteneur_deux``` a été configuré pour contenir les anciennes versions de vos objets qui sont stockés dans ```conteneur_un```. 
Par conséquent, ```conteneur_un``` contient la version la plus récente de vos objets et ```conteneur_deux``` contient
les anciennes versions de vos objets. Vérifiez que ```conteneur_deux``` existe pour assurer le fonctionnement de la gestion des
versions.


Une fois la gestion des versions configurée, lorsque vous téléchargez un objet dans ```conteneur_un```, s'il existe déjà une
version de l'objet, la version existante est déplacée dans ```conteneur_deux``` et la nouvelle version est créée dans ```conteneur_un```. Si
vous supprimez un objet de ```conteneur_un```, la version précédente de l'objet est déplacée de ```conteneur_deux``` vers ```conteneur_un```.

Les objets dans ```conteneur_deux``` sont nommés automatiquement selon le format suivant : ```<Longueur><Nom_objet>/<Horodatage>```

```Longueur``` est la longueur du nom de votre objet ; il s'agit d'un nombre hexadécimal de trois caractères remplis avec des zéros.
```Nom_objet``` est le nom de votre objet. ```Horodatage``` est l'horodatage du téléchargement initial de cette version particulière de l'objet.
Pour désactiver la gestion des versions, utilisez l'indicateur ```X-Remove-Versions-Location``` : 

	swift post conteneur_un -H "X-Remove-Versions-Location:"

ou 

	curl -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<url-stockage-objet>/conteneur_un

Voici un exemple complet de gestion des versions : 

1. Créez un conteneur : 

		$ swift post conteneur_un
		$

2. Configurez la gestion des versions pour conteneur_un :

		$ swift post conteneur_un -H "X-Versions-Location:conteneur_deux"
		$

3. Créez conteneur_deux:

		$ swift post conteneur_deux
		$

4. Téléchargez un objet pour la première fois dans conteneur_un :

		$ swift upload conteneur_un object
		object
		$

5. Répertoriez les objets dans conteneur_un :

		$ swift list conteneur_un
		object
		$

6. Répertoriez les objets dans conteneur_deux :

		$ swift list conteneur_deux
		$

7. Téléchargez une nouvelle version de l'objet dans conteneur_un :

		$ swift upload conteneur_un object
		object
		$

8. Répertoriez les objets dans conteneur_un :

		$ swift list conteneur_un 		object 		$

9. Répertoriez les objets dans conteneur_deux :

		$ swift list conteneur_deux
		006object/1457456909.27383
		$

10. Supprimez un objet dans conteneur_un :

		$ swift delete conteneur_un object
		object
		$

11. Répertoriez les objets des deux conteneurs : 

		$ swift list conteneur_un
		object
		$ swift list conteneur_deux
		$

### Planification de la suppression d'un objet {: #schedule-object-deletion}

Vous pouvez configurer vos objets pour qu'ils arrivent à expiration au bout d'un certain temps. En d'autres termes, vous pouvez planifier la
suppression de vos objets. Pour ce faire, utilisez l'en-tête ```X-Delete-At``` ou ```X-Delete-After```. L'en-tête ```X-Delete-At``` admet
un entier représentant la date et l'heure auxquelles supprimer l'objet. L'en-tête ```X-Delete_After``` admet un entier représentant le nombre
de secondes au bout duquel l'objet doit être supprimé.


Si vous utilisez le client Swift, émettez une commande post pour l'objet dans votre conteneur, comme dans les exemples ci-dessous. 

* Pour que l'objet soit supprimé le 01/04/2016 à 08:00:00, utilisez la commande suivante : 

		swift post -H "X-Delete-At:1459515600" container object

* Pour que l'objet soit supprimé dans une heure, utilisez la commande suivante : 

		swift post -H "X-Delete-After:3600" container object

  Ensuite, la commande ```swift stat container object``` permet d'afficher l'en-tête ```X-Delete-At``` avec
la date et l'heure d'expiration appropriées.


* Pour retirer la date et l'heure d'expiration de votre objet, utilisez la commande suivante : 

		swift post -H "X-Remove-Delete-After:" container object

Si vous utilisez curl, les commandes sont les suivantes :  

* Pour que l'objet soit supprimé le 01/04/2016 à 08:00:00, utilisez la commande suivante : 

		curl -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:1459515600" https://<url-stockage-objet>/container/object

* Pour que l'objet soit supprimé dans une heure, utilisez la commande suivante : 

		curl -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:3600" https://<url-stockage-objet>/container/object

* Pour vérifier si l'objet comporte l'en-tête, utilisez la commande suivante : 

		curl -I -H "X-Auth-Token: <token>" https://<url-stockage-objet>/container/object

* Pour retirer la date et l'heure d'expiration, utilisez la commande suivante : 

		curl -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:" https://<url-stockage-objet>/container/object

**Remarque :** il se peut que la suppression réelle d'un objet ne survienne pas exactement à l'heure indiquée. Cependant,
l'objet arrive effectivement à expiration à l'heure spécifiée, ce qui signifie qu'il devient inaccessible. La suppression réelle a lieu lorsque le démon
swift-object-expirer configuré dans votre cluster swift s'exécute. 





### Création d'une URL temporaire {: #create-temporary-url}

Une URL temporaire est une URL longue et difficile à deviner qui peut être utilisée pour une période spécifiée pour télécharger des objets sans nécessiter plus d'authentification. Générez une URL temporaire en procédant comme suit :

1. Identifiez votre compte d'authentification.
2. Définissez une clé secrète.
3. Créez l'URL temporaire.

#### Identification de votre compte d'authentification

La commande Swift ```stat` affiche les informations relatives à votre compte : 

	swift stat

Localisez la zone Compte et prenez note de la chaîne complète figurant après *Compte* : incluant ```AUTH_```.

#### Définition d'une clé secrète

Vous pouvez choisir la clé de votre choix, mais il est conseillé de choisir une chaîne longue, aléatoire et difficile à deviner.

	swift post -m "Temp-URL-Key:<key>"
	
Exécutez la commande Swift ```stat``` pour vérifier que l'élément ```Temp-URL-Key``` est défini
automatiquement. 

	swift stat


#### Création de l'URL temporaire

La commande Swift ```tempurl` admet les arguments de position suivants :

* [method] GET pour permettre la réception par téléchargement. PUT pour permettre l'envoi par téléchargement. 
* [seconds] Durée en secondes pendant laquelle l'adresse URL temporaire sera disponible. 
* [path] Chemin complet de l'objet, exprimé sous la forme ```/v1/<auth_compte>/<nom_conteneur>/<nom_objet>```. Pour
plus d'informations, voir [Adresse URL {{site.data.keyword.objectstorageshort}}](#access-points). 
* [key] Clé que vous avez configurée à l'étape 2. 

```
swift tempurl GET <seconds> <path> <key>
```

Cette commande retourne une URL que vous pouvez ajouter à votre nom de cluster pour obtenir une URL complète. Utilisez cette URL complète pour télécharger l'objet avec tout client HTTP compatible comme curl, wget ou Firefox.

## Utilisation de l'API Swift REST pour accéder à {{site.data.keyword.objectstorageshort}} {: #using-swift-restapi}

Vous pouvez vous servir de l'API Swift REST avec une interface client de ligne de commande, comme cURL, ou appeler l'API depuis votre application.  

### URL {{site.data.keyword.objectstorageshort}} {: #access-points}

Pour interagir avec l'API {{site.data.keyword.objectstorageshort}}, construisez l'URL {{site.data.keyword.objectstorageshort}} comme suit :

	https://<point d'accès>/<version d'API>/AUTH_<ID projet>/<espace de nom de conteneur>/<object namespace>



L'URL se compose des cinq parties suivantes : La ```<version de l'API>``` est la version 1 (v1). Vous pouvez trouver les
éléments ```<ID projet>```, ```<espace de nom de conteneur>``` et
```<espace de nom d'objet>``` de votre élément {{site.data.keyword.objectstorageshort}} depuis l'interface utilisateur {{site.data.keyword.objectstorageshort}}. Pour l'élément ```<point d'accès>```, voir le tableau suivant :  



| **Région**  |   **Point d'accès public**                     |
|-------------|-----------------------------------------------|
| Dallas      | https://dal.objectstorage.open.softlayer.com/ | 
| Londres      | https://lon.objectstorage.open.softlayer.com/ |


*Tableau 1. Point d'accès {{site.data.keyword.objectstorageshort}}*


### API {{site.data.keyword.objectstorageshort}}

Voir [OpenStack Swift API Complete Reference](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window} pour une liste complète des options d'API REST {{site.data.keyword.objectstorageshort}} et des exemples.

## Utilisation d'{{site.data.keyword.objectstorageshort}} sur plusieurs régions {: #multi-regions}  

IBM {{site.data.keyword.objectstorageshort}} pour service {{site.data.keyword.Bluemix_notm}} prend en charge les régions de stockage Dallas et Londres. Ces régions de stockage sont indépendantes de la région {{site.data.keyword.Bluemix_notm}} (Sud des Etats-Unis ou Royaume-Uni, par exemple) dans laquelle l'instance de service {{site.data.keyword.objectstorageshort}} est créée.  Ainsi, si vous créez une instance {{site.data.keyword.objectstorageshort}} dans la région {{site.data.keyword.Bluemix_notm}} Sud des Etats-Unis, vous pouvez lire et écrire des données dans l'une des deux régions de stockage, Dallas ou Londres.  

Pour la région {{site.data.keyword.Bluemix_notm}} Sud des Etats-Unis, la région de stockage Dallas est le paramètre par défaut. Pour la région {{site.data.keyword.Bluemix_notm}} Royaume-Uni, la région de stockage par défaut est Londres.  L'interface utilisateur {{site.data.keyword.objectstorageshort}} se lance toujours sur la région de stockage par défaut de la région {{site.data.keyword.Bluemix_notm}} utilisée. Pour changer de région, cliquez sur la liste déroulante Région {{site.data.keyword.objectstorageshort}} et choisissez une autre région.

**Remarque :** le service {{site.data.keyword.objectstorageshort}} NE prend PAS en charge la réplication sur différentes régions de stockage.

### Accès multi-région

Pour utiliser le service {{site.data.keyword.objectstorageshort}}, vous devez [vous authentifier auprès
d'OpenStack Keystone](#keystone-authentication). Une
fois que vous vous êtes authentifié, un élément ```X-Subject-Token``` et les noeuds finaux
{{site.data.keyword.objectstorageshort}} deviennent disponibles dans la réponse.


Par exemple, pour créer un conteneur nommé ```mon_conteneur ``` dans la région de stockage Dallas, spécifiez un point d'accès
Dallas dans la commande curl comme suit :


	# curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/mon_conteneur -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT


Pour créer un conteneur nommé ```mon_conteneur ``` dans la région de stockage Londres, spécifiez un point d'accès Londres dans
la commande curl comme suit :


	# curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/mon_conteneur -X PUT -H "Content-Length: 0" -H
"X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT

**Remarque :** l'élément ```X-Subject-Token``` que vous avez acquis auprès de Keystone fonctionne dans toutes
les régions de stockage.
 

Pour plus d'informations sur les points d'accès pour les différentes régions, voir le tableau [Point d'accès Object Storage](#access-points).


## Présentation de l'authentification et des données d'identification {: #understanding-authentication-credentials}

### Génération des données d'identification {{site.data.keyword.objectstorageshort}} sans liaison avec une application

Pour générer les données d'identification de cloud {{site.data.keyword.objectstorageshort}} afin de les utiliser en dehors d'une application {{site.data.keyword.Bluemix_notm}}, vous devez générer une clé de service pour votre instance {{site.data.keyword.objectstorageshort}}. Vous
pouvez générer une nouvelle clé en sélectionnant **Données d'identification pour le service** depuis la barre latérale de l'interface
utilisateur ou en utilisant l'interface de ligne de commande Cloud Foundry (version 6.11.3 ou ultérieure). Après avoir généré et extrait une clé de service pour votre instance {{site.data.keyword.objectstorageshort}}, vous pouvez utiliser les informations d'intégration de cloud pour demander un jeton Keystone en utilisant un kit SDK OpenStack ou l'API OpenStack Identity API. Vous démarrez ensuite en vous servant du compte Swift pour gérer les objets.
   
Pour créer la clé en utilisant l'interface de ligne de commande Cloud Foundry, connectez-vous et exécutez la commande suivante :
 
    cf create-service-key <nom_instance_object_storage> <nom_unique_pour_cette_clé>

Pour extraire les données d'identification du service à partir de l'interface de ligne de commande Cloud Foundry, exécutez la commande suivante :

	cf service-key <nom_instance_object_storage> <nom_unique_pour_cette_clé>


### Utilisateurs et projets de cloud
La mise à disposition d'une nouvelle instance {{site.data.keyword.objectstorageshort}} crée un projet Keystone isolé dans le cloud public IBM. Quand vous liez une nouvelle application à l'instance {{site.data.keyword.objectstorageshort}}, un nouvel utilisateur Keystone avec un accès au projet est créé. Quand vous annulez la mise à disposition de l'instance, le projet et l'utilisateur sont supprimés.

### OpenStack Identity (Keystone) v3 {: #keystone-authentication}
La structure de données d'identification contient un ensemble complet d'attributs pour vous permettre de choisir la méthode de demande de jeton OpenStack ou le kit SDK OpenStack qui convient le mieux pour votre application. 
 
La demande de jeton v3 recommandée est une demande POST vers https://identity.open.softlayer.com/v3/auth/tokens, comme illustré dans la commande curl suivante :

	curl -i \
	  -H "Content-Type: application/json" \
	  -d '
	{
		"auth": {
			"identity": {
				"methods": [
					"password"
				],
				"password": {
					"user": {
						"id": "ad78b2a3f843466988afd077731c61fc",
						"password": "K/jyIi2jR=1?D.TP"
					}
				}
			},
			"scope": {
				"project": {
					"id": "0f47b41b06d047f9aae3b33f1db061ed"
				}
			}
		}
	}' \
	  https://identity.open.softlayer.com/v3/auth/tokens ; echo

Utilisez la valeur de la zone ```X-Subject-Token``` figurant dans l'en-tête de réponse comme zone ```X-Auth-Token``` lorsque
vous envoyez des demandes au service {{site.data.keyword.objectstorageshort}}. 

Voici un exemple de réponse. La réponse est tronquée afin de n'afficher que les informations pertinentes pour
{{site.data.keyword.objectstorageshort}}.


	HTTP/1.1 201 Created
	Date: Mon, 29 Feb 2016 21:03:41 GMT
	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.1e-fips mod_wsgi/3.4 Python/2.7.5
	X-Subject-Token: gAAAAABW1LIubUgqKl-eInzhZUHWEnXijp7t6_5inl4DTRLxDhNbJ25ly2X7bASNvH7ocxinaJu_kdhSfnHNRwPAeYY77Ii2Cwp02-bvxUA1S9lV_knT6EyCOW2mSBl_HuuDD2cEgdiKmyZTVt-RvDxhPKYD-rHkJz-dHO4Folg8TVXotilb1uw
	Vary: X-Auth-Token
	x-openstack-request-id: req-01e096c8-5393-4f98-8ff6-029c55e42524
	Content-Length: 12051
	Content-Type: application/json

	{
	  "token" : {
	    "roles" : [
	      {
	        "id" : "f61f06a84f6443e880210fa986bd8691",
	        "name" : "ObjectStorageOperator"
	      }
	    ],
	    "catalog" : [
	      {
	        "endpoints": [
			{
	            "id" : "20cbfa6ff22b4a67a1484d30235bfc80",
	            "region" : "londres",
	            "region_id" : "londres",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "38b8c081b11a452bb951698c334a406d",
	            "region" : "londres",
	            "region_id" : "londres",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          },
	          {
	            "id" : "4207049680fa4effbecd044c7448a8cb",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "8a65a0cf38ac4211ad6a3c9c0eb337ff",
	            "region" : "londres",
	            "region_id" : "londres",
	            "url" : "https:\/\/lon.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "a60cf32be624491d89170ef8264de5e8",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "c769862200124a308d6748e418c971ba",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          }
	        ],
	        "id" : "896e4064cbe742afbf9a543c15f27ac0",
	        "type" : "object-store",
	        "name" : "swift"
	      },
	    ],
	    "extras" : {

	    },
	    "user" : {
	      "id" : "0b8aebd924ef4cc7aa9232f07e47e874",
	      "name" : "user_87c094ce47a9feae3a137ffcbbfa098a888c12a8",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "expires_at" : "2016-02-29T22:03:42.061343Z",
	    "audit_ids" : [
	      "cbA-iL2dSheyB72PHd7q8Q"
	    ],
	    "issued_at" : "2016-02-29T21:03:42.000000Z",
	    "project" : {
	      "id" : "3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	      "name" : "object_storage_c1d8b3a1",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "methods" : [
	      "password"
	    ]
	  }
	}


L'adresse URL {{site.data.keyword.objectstorageshort}} se trouve dans le catalogue de service. Ce dernier est contenu dans le corps de réponse de la demande de jeton. La réponse est un catalogue complet des services OpenStack qui sont disponibles. Sélectionnez
le noeud final dans le catalogue de service avec le type ```object-store``` et la région correspondant à la zone de région dans les
données d'identification.


**Remarque :** utilisez l'interface publique (`publicURL`). L'interface interne (`internalURL`)
n'est pas accessible depuis {{site.data.keyword.Bluemix_notm}}.


## Annulation de la liaison et de la mise à disposition d'{{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}

### Comment annuler la mise à disposition de votre service {{site.data.keyword.objectstorageshort}} ?
1.	Sélectionnez votre service depuis le tableau de bord {{site.data.keyword.Bluemix_notm}}.  
2.	Cliquez sur l'icône représentant un engrenage et sélectionnez **Supprimer le service**.
	
**Avertissement :** si vous annulez la mise à disposition d'un espace IBM {{site.data.keyword.objectstorageshort}} pour  l'instance de service {{site.data.keyword.Bluemix_notm}}, le projet de cloud et le compte Swift sont supprimés. Tous les conteneurs et les objets de l'instance concernée sont supprimés de Swift et ne peuvent être restaurés.

### Annulation de la liaison d'une application ou suppression d'une clé de service

Si vous annulez la liaison d'une application depuis l'instance {{site.data.keyword.objectstorageshort}} ou supprimez la clé de service, les  données d'identification sont supprimées. Le compte {{site.data.keyword.objectstorageshort}} n'est pas supprimé tant que la mise à disposition de l'instance {{site.data.keyword.objectstorageshort}} n'est pas annulée. Vous pouvez générer de nouvelles données d'identification de cloud en [ effectuant une nouvelle liaison ou en créant une nouvelle clé de service.](#bind-object-storage-to-application).

