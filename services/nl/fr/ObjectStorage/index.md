{:new_window: target="_blank"}

# Initiation à {{site.data.keyword.objectstorageshort}}  {: #getting-started-with-object-storage} 

{{site.data.keyword.objectstoragefull}} permet d'accéder à un compte Swift {{site.data.keyword.objectstorageshort}} complet pour gérer vos données. Swift fournit une plateforme de stockage accessible par API, totalement distribuée. Vous pouvez l'utiliser directement dans vos applications ou pour les sauvegardes, ce qui en fait un outil idéal pour un stockage économique et dimensionnable.

IBM {{site.data.keyword.objectstorageshort}} pour {{site.data.keyword.Bluemix_notm}}, qui utilise OpenStack Identity (Keystone) pour l'authentification, est accessible directement en utilisant les appels d'API v1 OpenStack Object Storage (Swift). IBM {{site.data.keyword.objectstorageshort}} peut être lié à une application {{site.data.keyword.Bluemix_notm}} ou être accédée depuis une application {{site.data.keyword.Bluemix_notm}}, en dehors de celle-ci. 

Vous trouverez plus d'informations et de documentation sur l'utilisation d'OpenStack Swift et Keystone sur le [site de documentation OpenStack](http://docs.openstack.org){: new_window}.

Le diagramme de l'architecture de {{site.data.keyword.objectstorageshort}} est illustré ci-dessous :

[![{{site.data.keyword.objectstorageshort}} - Diagramme Architecture](images/object_storage_solution_archectiture_small.png)](http://www.ng.bluemix.net/docs/api/content/services/ObjectStorage/images/object_storage_solution_archectiture.png){: new_window}

*Figure 1. Diagramme de l'architecture d'{{site.data.keyword.objectstorageshort}}*

**Remarque :** aucun chiffrement côté fournisseur n'est fourni. C'est la responsabilité de l'application client de chiffrer les données avant leur téléchargement.

**Remarque :** le plan de service bêta {{site.data.keyword.objectstorageshort}} sera retiré du catalogue une fois effective la disponibilité générale du service {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}}. Après une période de grâce, les instances de service qui se servent du plan bêta seront retirées. [Mettez à jour votre plan de tarification](#changeplan) pour continuer à utiliser le service {{site.data.keyword.objectstorageshort}}. 




## Création d'une instance {{site.data.keyword.objectstorageshort}} sur {{site.data.keyword.Bluemix_notm}} {: #creating-object-storage-instance} 

### Comment créer une instance de service {{site.data.keyword.objectstorageshort}} ?
1.	Accédez à l'onglet {{site.data.keyword.Bluemix_notm}} **Catalogue** et entrez **{{site.data.keyword.objectstorageshort}}** dans la zone de recherche, ou allez sur **Services** et sélectionnez **Stockage**. Cliquez sur le service **{{site.data.keyword.objectstorageshort}}**. 
2.	Sélectionnez votre espace, votre application, le nom de service et le plan puis cliquez sur **Créer**. 
**Remarque :** si vous avez choisi initialement l'option **Laisser non lié** pour la zone **Application**, vous pourrez toujours lier l'instance de service à votre application {{site.data.keyword.Bluemix_notm}} une fois que vous aurez terminé la configuration. Voir les instructions ci-après.

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

## Utilisation de l'interface utilisateur {{site.data.keyword.objectstorageshort}} {: #using-object-storage-ui}

### Eléments d'interface utilisateur et navigation
Quand {{site.data.keyword.objectstorageshort}} est provisionné, vous pouvez voir vos informations d'instance dans {{site.data.keyword.objectstorageshort}} pour le tableau de bord d'instance de service {{site.data.keyword.Bluemix_notm}}. Depuis le tableau de bord, sélectionnez votre instance {{site.data.keyword.objectstorageshort}} pour afficher le panneau avec des informations plus détaillées.  
#### Données d'utilisation
En haut du panneau, vous voyez les informations de données d'utilisation pour votre instance. A cet emplacement s'affichent aussi le nombre actuel de **conteneurs de stockage** et le nombre total d'**objets** dans tous vos conteneurs. Votre utilisation de la mémoire en mégaoctets est aussi indiquée. L'espace de **stockage consommé** se réfère au volume actuel d'espace qui est utilisé. 
#### Actions
Pour extraire les dernières données d'utilisation, cliquez sur le bouton **Actualiser**.   
####Navigateur d'objet 
La section inférieure du panneau contient le navigateur d'objet. Utilisez ce dernier pour gérer les objets et conteneurs de stockage d'objets. Vous pouvez créer des conteneurs, télécharger des fichiers, supprimer des conteneurs ou des fichiers, et effectuer d'autres actions.

## Utilisation de Swift CLI pour accéder à {{site.data.keyword.objectstorageshort}} {: #using-swift-cli}

Vous pouvez accéder au service {{site.data.keyword.objectstorageshort}} sur Internet et à partir des applications et machines virtuelles au sein d'IBM {{site.data.keyword.Bluemix_notm}}. Des cas d'utilisation courants du service {{site.data.keyword.objectstorageshort}} sont présentés ci-dessous :

* Sauvegarde de données de volume depuis vos instances
* Utilisation d'un emplacement intermédiaire lors du transfert de volumes importants de données
* Transfert de données entre des environnements non directement connectés
* Rôle de référentiel central

Le service {{site.data.keyword.objectstorageshort}}, qui repose sur OpenStack Swift, est accessible en utilisant une application client compatible. Cette section décrit comme se servir du client Python Swift, qui est l'interface CLI (Command-Line Interface) pour l'API {{site.data.keyword.objectstorageshort}} et ses extensions, pour utiliser des conteneurs et des fichiers.

### Installation du client Swift

Installez les logiciels prérequis suivants, si ce n'est pas déjà fait. Pour plus d'informations, voir la [documentation OpenStack](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}. 
* Python 2.7 ou ultérieur
* Package setuptools
* Package pip

Installez le client Python Swift en utilisant Python pip :

	sudo pip install python-swiftclient

### Configuration du client

Le client Swift prend les informations d'authentification dans les variables d'environnement suivantes :
* `OS_AUTH_URL` est l'URL de noeud final
* `OS_USER_ID` est le nom d'utilisateur
* `OS_PASSWORD` est le mot de passe

Définissez les informations d'authentification comme suit. 

	export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
	export OS_PASSWORD=aaa55AAAaaaaa]?,
	export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
	export OS_AUTH_URL=https://identity.open.softlayer.com/v3
	export OS_REGION_NAME=dallas
	export OS_IDENTITY_API_VERSION=3
	export OS_AUTH_VERSION=3

Vous pouvez trouver les valeur de données d'identification pour votre service {{site.data.keyword.objectstorageshort}} sur la page **Données d'identification pour le service** de l'interface utilisateur {{site.data.keyword.objectstorageshort}} 

**Remarque :** prenez soin d'ajouter `/v3` à `auth_url` depuis les données d'identification de l'interface utilisateur {{site.data.keyword.objectstorageshort}} quand vous configurez les variables d'environnement `OS_AUTH_URL` pour le client Swift.


![Données d'identification du service {{site.data.keyword.objectstorageshort}}](images/service_credentials.jpg)

*Figure 2. Données d'identification du service {{site.data.keyword.objectstorageshort}}*

### Utilisation des conteneurs

Création d'une liste des conteneurs :

	swift list
	
Création d'un conteneur :

	swift post <container_name>
	
Création d'une liste du contenu d'un conteneur :

	swift list <container_name>

### Utilisation des objets

#### Ajout d'un fichier à un conteneur

	swift upload <container_name> <file_name>

#### Ajout dans un conteneur d'un fichier supérieur à 5 Go

Si vous téléchargez un fichier qui fait plus de 5 Go, vous devez le diviser en parties plus petites. Vous pouvez demander au client Swift de gérer un téléchargement de ce type en fournissant le paramètre `-segment-size` :

	swift upload <container_name> <file_name> --segment-size <size_in_bytes>
	
Chaque segment est téléchargé en parallèle dans un conteneur séparé intitulé `<container_name>_segments`. Une fois que tous les segments ont été transférés, Swift crée un fichier manifeste de façon à ce que les segments puissent être téléchargés dans un fichier unique à partir du conteneur d'origine `<container_name>` avec le nom de fichier d'origine `<file_name>`.

Ainsi, la commande ci-après télécharge un fichier intitulé `large_file` depuis un conteneur intitulé `test_container` avec la taille de segment `1073741824`.

	swift upload test_container -S 1073741824 large_file

Vous pouvez exécuter la commande suivante pour télécharger le fichier :

	swift download test_container large_file

#### Téléchargement d'un fichier

	swift download <container_name> <file_name>
	
#### Ajout d'un répertoire à un conteneur

Swift n'a pas de véritable structure de répertoires, mais utilise la désignation pour en représenter une. Pour ajouter un répertoire à un conteneur, exécutez la commande suivante :

	swift upload <container_name> <directory_name>
	
Cette commande télécharge la structure de répertoire complète en tant que chemin relatif. Ainsi, si vous spécifiez `/mnt/volume1`, la structure de répertoire mnt/volume1 sera attachée à tous les noms de fichier pour indiquer la structure de répertoire.

	
#### Téléchargement d'un répertoire

Pour télécharger une structure de répertoire, utilisez le paramètre `-prefix` pour indiquer le répertoire ou la structure de répertoire que vous voulez charger.

	swift download <container_name> --prefix <directory>
	
#### Suppression d'un fichier

	swift delete <container_name> <file_name>

### Création d'une URL temporaire

Une URL temporaire est une URL longue et difficile à deviner qui peut être utilisée pour une période spécifiée pour télécharger des objets sans nécessiter plus d'authentification. Générez une URL temporaire en procédant comme suit :

1. Identifiez votre compte d'authentification.
2. Définissez une clé secrète.
3. Créez l'URL temporaire.

#### Identification de votre compte d'authentification

La commande Swift `stat` imprime les informations relatives à votre compte

	swift stat

Localisez la zone Compte et prenez note de la chaîne complète qui suit *Compte :*, incluant `AUTH_`.

#### Définition d'une clé secrète

Cette clé peut contenir tout ce que vous sélectionnez mais il est conseillé de choisir une chaîne longue, aléatoire et difficile à deviner.

	swift post -m "Temp-URL-Key:<key>"

#### Création de l'URL temporaire

La commande Swift `tempurl` prend les arguments de position suivants :

* [method] GET pour permettre la réception par téléchargement, PUT pour autoriser l'envoi par téléchargement
* [seconds] Durée en secondes pendant laquelle l'URL temporaire sera disponible
* [path] Chemin complet de l'objet, exprimé sous la forme <auth_account>/<container_name>/<object_name>
* [key] Clé que vous avez configurée à l'étape 2

```
swift tempurl GET <seconds> <path> <key>
```

Cette commande retourne une URL que vous pouvez ajouter à votre nom de cluster pour obtenir une URL complète. Utilisez cette URL complète pour télécharger l'objet avec tout client HTTP compatible comme curl, wget ou Firefox.

## Utilisation de l'API Swift REST pour accéder à {{site.data.keyword.objectstorageshort}} {: #using-swift-restapi}

Vous pouvez vous servir de l'API Swift REST avec une interface client de ligne de commande, comme cURL, ou appeler l'API depuis votre application.  

### URL {{site.data.keyword.objectstorageshort}} {: #access-points}

Pour interagir avec l'API {{site.data.keyword.objectstorageshort}}, construisez l'URL {{site.data.keyword.objectstorageshort}} comme suit :

	https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>

Exemple :

URL ![{{site.data.keyword.objectstorageshort}}](images/Swift_URL.png)

*Figure 3. URL {{site.data.keyword.objectstorageshort}}*

L'URL se compose des cinq parties suivantes : ```<API version>``` est v1. Vous trouverez ```<project ID>``, ```<container namespace>`` et ```<object namespace>`, associés à votre espace {{site.data.keyword.objectstorageshort}} dans l'interface utilisateur {{site.data.keyword.objectstorageshort}}.  Pour `<access point>`, voir le tableau suivant : 


| **Région**  |     **Point d'accès interne**                             |     **Point d'accès public**                   |
|-------------|-----------------------------------------------------------|-----------------------------------------------|
| Dallas      | https://dal.objectstorage.service.open.networklayer.com/  | https://dal.objectstorage.open.softlayer.com/ | 
| Londres      | https://lon.objectstorage.service.open.networklayer.com/  | https://lon.objectstorage.open.softlayer.com/ |


*Tableau 1. Point d'accès {{site.data.keyword.objectstorageshort}}*

Utilisez le point d'accès interne quand vous accédez au service {{site.data.keyword.objectstorageshort}} depuis {{site.data.keyword.Bluemix_notm}} ou le point d'accès public lorsque l'accès au service {{site.data.keyword.objectstorageshort}} s'effectue en dehors de {{site.data.keyword.Bluemix_notm}}.

### API {{site.data.keyword.objectstorageshort}}

Voir [OpenStack Swift API Complete Reference](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window} pour une liste complète des options d'API REST {{site.data.keyword.objectstorageshort}} et des exemples.

## Utilisation d'{{site.data.keyword.objectstorageshort}} sur plusieurs régions {: #multi-regions}  

IBM {{site.data.keyword.objectstorageshort}} pour service {{site.data.keyword.Bluemix_notm}} prend en charge les régions de stockage Dallas et Londres. Ces régions de stockage sont indépendantes de la région {{site.data.keyword.Bluemix_notm}} (Sud des Etats-Unis ou Royaume-Uni, par exemple) dans laquelle l'instance de service {{site.data.keyword.objectstorageshort}} est créée.  Ainsi, si vous créez une instance {{site.data.keyword.objectstorageshort}} dans la région {{site.data.keyword.Bluemix_notm}} Sud des Etats-Unis, vous pouvez lire et écrire des données dans l'une des deux régions de stockage, Dallas ou Londres.  

Pour la région {{site.data.keyword.Bluemix_notm}} Sud des Etats-Unis, la région de stockage Dallas est le paramètre par défaut. Pour la région {{site.data.keyword.Bluemix_notm}} Royaume-Uni, la région de stockage par défaut est Londres.  L'interface utilisateur {{site.data.keyword.objectstorageshort}} se lance toujours sur la région de stockage par défaut de la région {{site.data.keyword.Bluemix_notm}} utilisée. Pour changer de région, cliquez sur la liste déroulante Région {{site.data.keyword.objectstorageshort}} et choisissez une autre région.

![Changement de région {{site.data.keyword.objectstorageshort}}](images/change_region.png)

*Figure 4. Changement de région {{site.data.keyword.objectstorageshort}}*

**Remarque :** le service {{site.data.keyword.objectstorageshort}} NE prend PAS en charge la réplication sur différentes régions de stockage.

### Accès multi-région

Pour utiliser le service {{site.data.keyword.objectstorageshort}}, vous devez [ vous authentifier sur OpenStack Keystone](#keystone-authentication). Une fois authentifié, un jeton `X-Subject-Token` et les noeuds finaux {{site.data.keyword.objectstorageshort}} sont disponibles dans la réponse.

Ainsi, pour créer un conteneur intitulé `my_container` dans la région de stockage Dallas, spécifiez un point d'accès Dallas dans la commande curl, comme suit :

	# curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT


Pour créer un conteneur intitulé `my_container` dans la région de stockage Londres, spécifiez un point d'accès Londres dans la commande curl, comme suit :

	# curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT

**Remarque :** le jeton `X-Subject-Token` que vous avez acquis depuis Keystone fonctionne sur différentes régions de stockage. 

Pour plus d'informations sur les points d'accès pour les différentes régions, voir le tableau [Point d'accès Object Storage](#access-points).


## Présentation de l'authentification et des données d'identification {: #understanding-authentication-credentials}

### Génération des données d'identification {{site.data.keyword.objectstorageshort}} sans liaison avec une application

Pour générer les données d'identification de cloud {{site.data.keyword.objectstorageshort}} afin de les utiliser en dehors d'une application {{site.data.keyword.Bluemix_notm}}, vous devez générer une clé de service pour votre instance {{site.data.keyword.objectstorageshort}}. Vous pouvez générer une nouvelle clé en sélectionnant **Données d'identification pour le service** depuis la barre latérale de l'interface utilisateur ou en utilisant l'interface CLI Cloud FoundryCloud (version 6.11.3 ou ultérieure). Après avoir généré et extrait une clé de service pour votre instance {{site.data.keyword.objectstorageshort}}, vous pouvez utiliser les informations d'intégration de cloud pour demander un jeton Keystone en utilisant un kit SDK OpenStack ou l'API OpenStack Identity API. Vous démarrez ensuite en vous servant du compte Swift pour gérer les objets.
   
Pour créer la clé en utilisant l'interface Cloud Foundry CLI, connectez-vous et exécutez la commande suivante :
 
    cf create-service-key <object_storage_instance_name> <unique_name_for_this_key>

Pour extraire les données d'identification du service à partir de l'interface Cloud Foundry CLI, exécutez la commande suivante :

	cf service-key <object_storage_instance_name> <unique_name_for_this_key>


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

Utilisez la valeur de la zone `X-Subject-Token` depuis l'en-tête de réponse comme zone `X-Auth-Token` quand vous effectuez des demandes vers le service {{site.data.keyword.objectstorageshort}}.

Une réponse exemple est présentée ci-dessous :

	HTTP/1.1 201 Created
	X-Subject-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9
	Vary: X-Auth-Token
	Content-Type: application/json
	Content-Length: 960
	Date: Tue, 10 Jun 2014 20:40:14 GMT
	
	{"token": 
	{"audit_ids": ["ECwrVNWbSCqmEgPnu0YCRw"], "methods": ["password"],
	 "roles": [{"id": "c703057be878458588961ce9a0ce686b", "name": "admin"}],
	 "expires_at": "2014-06-10T21:40:14.360795Z", 
	 "project": {"domain": {"id": "default", "name": "Default"}, "id": "3d4c2c82bd5948f0bcab0cf3a7c9b48c", "name": "demo"}, 
	 "catalog": [
	 {
		"endpoints": [
			{
			"adminURL": "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"id": "20cbfa6ff22b4a67a1484d30235bfc80",
			"internalURL": "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"publicURL": "https://lon.objectstorage.open.softlayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"region": "london"
			},
			{
			"adminURL": "https://dal.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"id": "4207049680fa4effbecd044c7448a8cb",
			"internalURL": "https://dal.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"publicURL": "https://dal.objectstorage.open.softlayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"region": "dallas"
			}
			],
		"endpoints_links": [],
		"name": "swift",
		"type": "object-store"
		},
	 ], 
	 "extras": {},
	 "user": {"domain": {"id": "default", "name": "Default"}, "id": "3ec3164f750146be97f21559ee4d9c51", "name": "admin"},  "issued_at": "2014-06-10T20:40:14.360822Z"}}


L'URL {{site.data.keyword.objectstorageshort}} se trouve dans le catalogue de service. Ce dernier est contenu dans le corps de réponse de la demande de jeton. La réponse est un catalogue complet des services OpenStack qui sont disponibles. Sélectionnez le noeud final depuis le catalogue de service avec le type `object-store`, la région qui correspond à la zone région des données d'identification et l'interface interne (`internalURL`) quand vous accédez au service {{site.data.keyword.objectstorageshort}} depuis {{site.data.keyword.Bluemix_notm}}, ou l'interface publique `publicURL`) lorsque l'accès au service {{site.data.keyword.objectstorageshort}} s'effectue en dehors de {{site.data.keyword.Bluemix_notm}}.



## Annulation de la liaison et de la mise à disposition d'{{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}

### Comment annuler la mise à disposition de votre service {{site.data.keyword.objectstorageshort}} ?
1.	Sélectionnez votre service depuis le tableau de bord {{site.data.keyword.Bluemix_notm}}.  
2.	Cliquez sur l'icône représentant un engrenage dans l'angle supérieur droit et sélectionnez **Supprimer le service**.
	
**Avertissement :** si vous annulez la mise à disposition d'un espace IBM {{site.data.keyword.objectstorageshort}} pour  l'instance de service {{site.data.keyword.Bluemix_notm}}, le projet de cloud et le compte Swift sont supprimés. Tous les conteneurs et les objets de l'instance concernée sont supprimés de Swift et ne peuvent être restaurés.

### Annulation de la liaison d'une application ou suppression d'une clé de service

Si vous annulez la liaison d'une application depuis l'instance {{site.data.keyword.objectstorageshort}} ou supprimez la clé de service, les  données d'identification sont supprimées. Le compte {{site.data.keyword.objectstorageshort}} n'est pas supprimé tant que la mise à disposition de l'instance {{site.data.keyword.objectstorageshort}} n'est pas annulée. Vous pouvez générer de nouvelles données d'identification de cloud en [ effectuant une nouvelle liaison ou en créant une nouvelle clé de service.](#bind-object-storage-to-application).

## Foire aux questions {: #FAQ} 

### Comment les tarifs varient selon le plan que vous choisissez ?
La tarification est fonction du plan choisi. Pour plus d'informations sur la tarification, voir la [page relative à la tarification IBM Bluemix](https://console.ng.bluemix.net/pricing/){: new_window} ou utilisez la [calculatrice](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet){: new_window} pour obtenir des estimations plus détaillées.

### Comment changer mon plan de Bêta à Standard ? {: #changeplan}  
Le plan de service bêta {{site.data.keyword.objectstorageshort}} sera retiré du catalogue une fois effective la disponibilité générale du service {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}}. Les instances de service clients NE sont PAS migrés automatiquement du plan Bêta au plan Standard. Vous devrez mettre à jour votre plan en procédant comme suit :

1.	Cliquez sur **Plan** dans la barre de navigation de gauche de l'interface utilisateur {{site.data.keyword.objectstorageshort}}.
2.	Sélectionnez **Standard** en tant que nouveau plan puis cliquez sur **Sauvegarder**.

![Changer de plan de tarification {{site.data.keyword.objectstorageshort}}](images/Change_plan.png)

*Figure 5. Changement de plan de tarification {{site.data.keyword.objectstorageshort}}*

Vos instances de services et vos données client sont déplacées vers le nouveau plan.

Vous pouvez aussi changer votre plan de paiement en utilisant l'interface de ligne de commande. Pour plus d'informations, voir [Comment changer votre plan ?](../../pricing/index.html#changing)  

**Remarque :** les instances de service de plan bêta ne peuvent être déplacées vers le plan gratuit. Toutes les instances de service non migrées seront désactivées puis, après 60 jours, supprimées. 

### Quels comptes et plans de paiement puis-je utiliser pour {{site.data.keyword.objectstorageshort}} ?
Le service {{site.data.keyword.objectstorageshort}} est fourni avec plusieurs options de plan différentes. Dans le cadre de notre édition en disponibilité générale, deux plans sont actuellement proposés, Standard et Gratuit. Le plan Standard est disponible uniquement pour les comptes payants {{site.data.keyword.Bluemix_notm}} (sous la forme Paiement à la carte ou Abonnement) ou pour les utilisateurs internes IBM.

Les comptes d'essai qui sont toujours actifs sont en mesure d'utiliser le plan gratuit qui autorise l'existence d'une instance unique dans une organisation {{site.data.keyword.Bluemix_notm}}. Une fois expiré la période d'essai {{site.data.keyword.Bluemix_notm}}, l'instance de service {{site.data.keyword.objectstorageshort}} associée est désactivée, ce qui signifie qu'il n'est plus possible d'accéder au compte de stockage par la ligne de commande ou l'interface utilisateur {{site.data.keyword.Bluemix_notm}}. Après une période de grâce de 30 jours, votre compte {{site.data.keyword.Bluemix_notm}} est purgé et toutes les données supprimées. Pour éviter de perdre des données, il est donc conseillé de procéder à une mise à niveau vers un compte payant {{site.data.keyword.Bluemix_notm}} aussi vite que possible. Pour mettre à niveau votre compte, cliquez sur le menu de gestion utilisateur dans l'angle supérieur droit puis sélectionnez l'option **Compte**, qui vous donne des instructions sur le processus de mise à niveau.

Les instances qui sont créées sur le plan gratuit peuvent être mises à niveau sur le plan Standard en suivant la procédure décrite dans [Comment changer mon plan de Bêta à Standard ?](#changeplan). Pour mettre à niveau vers le plan Standard, l'organisation associée doit être un compte payant {{site.data.keyword.Bluemix_notm}}. Les comptes d'essai avec instances {{site.data.keyword.objectstorageshort}} ne peuvent être mis à niveau vers le plan Standard, et les instances du plan Standard ne peuvent être rétrogradées vers d'autres plans.

### Comment serais-je facturé pour mon utilisation d'{{site.data.keyword.objectstorageshort}} ?

Le service {{site.data.keyword.objectstorageshort}} ne vous facture que pour ce que vous utilisez. Il n'y a pas de frais minimum, de frais d'installation ou d'engagements pour pouvoir utiliser le service. Les requêtes d'API ou le trafic réseau liés aux données entrantes ne sont pas facturés.

Votre utilisation d'{{site.data.keyword.objectstorageshort}} est facturée en se basant que l'utilisation moyenne quotidienne d'espace de stockage au cours du cycle de facturation. Toutes les données objet se trouvant dans des conteneurs ayant été créées sous votre compte d'organisation {{site.data.keyword.Bluemix_notm}} sont prises en compte. 

Les frais pour le transfert de données sortantes s'appliquent dès lors que des données sont lues depuis n'importe quel conteneur d'objets sur le réseau public. Ces frais sont calculés en se basant sur le transfert moyen quotidien de données sortantes publiques au cours du cycle de facturation.

Les composants de mesure pour la tarification d'{{site.data.keyword.objectstorageshort}} sont les suivants :
* Utilisation d'espace de stockage - 0,04 $ par Go/mois
* Transfert de données sortantes publiques - 0,09 $ par Go/mois 

A la fin du cycle de facturation, {{site.data.keyword.Bluemix_notm}} vous facturera automatiquement l'utilisation du service pour la période de facturation en cours. Vous pouvez afficher vos frais pour la période de facturation en cours via la génération de rapports {{site.data.keyword.Bluemix_notm}}.

Le plan de service standard qui est publié pour Londres et Dallas dispose de la même tarification.

### Comment est effectuée la réplication des données dans {{site.data.keyword.objectstorageshort}} ?
Le service {{site.data.keyword.objectstorageshort}} conserve trois copies de vos données, qui sont répliquées sur différents noeuds de stockage. Pour plus d'informations, consultez le document [OpenStack Swift Replication](http://docs.openstack.org/developer/swift/overview_replication.html){: new_window}.

># Liens apparentés {:class="linklist"}
>## Référence API {:id="api"}
>* [API OpenStack Object Storage (Swift) version 1](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}
>* [Identity API v3 (CURRENT)](http://developer.openstack.org/api-ref-identity-v3.html){: new_window}
>
># Liens apparentés {:class="linklist"}
>## SDK {:id="sdk"}
>* [Kits de développement de logiciels (SDK) OpenStack](https://wiki.openstack.org/wiki/SDKs){: new_window}
>
># Liens apparentés {:class="linklist"}
>## Tutoriels et exemples {:id="samples"}
>* [Connecting to IBM Object Storage for Bluemix with Java](https://developer.ibm.com/recipes/tutorials/connecting-to-ibm-object-storage-for-bluemix-with-java/){: new_window}
>* [Use Python to access your Bluemix Object Storage](https://developer.ibm.com/recipes/tutorials/use-python-to-access-your-bluemix-object-storage/){: new_window}
>* [Communauties - Bluemix Object Storage Service](https://www.ibm.com/developerworks/community/groups/service/html/communityoverview?communityUuid=1b48459f-4091-43cb-bca4-37863606d989){: new_window}
>
># Liens apparentés {:class="linklist"}
>## Contextes d'exécution compatibles {:id="buildpacks"}
>* [Liberty for Java](https://www.ng.bluemix.net/docs/starters/liberty/index.html){: new_window}
>* [SDK for Node.js](https://www.ng.bluemix.net/docs/starters/nodejs/index.html){: new_window}
>* [Go](https://www.ng.bluemix.net/docs/starters/go/index.html){: new_window}
>* [PHP](https://www.ng.bluemix.net/docs/starters/php/index.html){: new_window}
>* [Python](https://www.ng.bluemix.net/docs/starters/python/index.html){: new_window}
>* [Ruby](https://www.ng.bluemix.net/docs/starters/rails/index.html){: new_window}
>* [Community buildpacks](https://www.ng.bluemix.net/docs/starters/byob.html){: new_window}
>
># Liens apparentés {:class="linklist"}
>## Liens apparentés {:id="general"}
>* [IBM Bluemix - Tarification](https://www.ng.bluemix.net/#/pricing){: new_window}
>* [IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
>
>{:elementKind="article" id="rellinks"}
