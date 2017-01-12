---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-04"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Accès à {{site.data.keyword.objectstorageshort}} via Swift CLI {: #using-swift-cli}


Le service {{site.data.keyword.objectstorageshort}}, qui repose sur OpenStack Swift, est accessible via une application client compatible. Cette
section explique comment se servir du client Python Swift, qui est l'interface de ligne de commande pour l'API
{{site.data.keyword.objectstorageshort}} et ses extensions, pour utiliser des conteneurs et des fichiers.
{: shortdesc}




## Installation du client Swift {: #install-swift-client}

Si ce n'est déjà fait, installez les [logiciels prérequis](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window} suivants.
* Python 2.7 ou ultérieur
* Package setuptools
* Package pip


Pour installer le client Python Swift, exécutez la commande suivante :
```
pip install python-swiftclient
```
{: pre}

Pour installer le client Python Keystone, exécutez la commande suivante :
```
pip install python-keystoneclient
```
{: pre}




## Configuration du client {: #setup-swift-client}

Pour configurer le client Swift, vous devez `exporter` vos informations d'authentification. Vous pouvez générer les données d'identification [ via l'interface utilisateur](../ObjectStorage/os_security.html#understanding-credentials) ou [par le biais de l'interface de ligne de commande](../ObjectStorage/os_cli.html#generating-cli).

Pour exporter vos informations d'authentification, entrez vos données d'identification et exécutez les commandes suivantes :
```
export OS_USER_ID=
export OS_PASSWORD=
export OS_PROJECT_ID=
export OS_AUTH_URL=
export OS_REGION_NAME=
export OS_IDENTITY_API_VERSION=
export OS_AUTH_VERSION=

swift auth
```
{: codeblock}


Exemple :
```
export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
  export OS_PASSWORD=*******
  export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=dallas
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

swift auth
```
{: screen}




## Génération des données d'identification de service {{site.data.keyword.objectstorageshort}} {: #generating-cli}

Pour générer des données d'identification de service en utilisant Swift CLI, procédez comme suit.

1. Si vous n'êtes pas connecté à {{site.data.keyword.Bluemix_notm}}, connectez-vous en tant qu'utilisateur avec un rôle développeur. Vous devez vous trouver au sein de l'espace de l'instance de service que vous voulez gérer.
  ```
  cf login -a api.ng.bluemix.net -u <ID_utilisateur> -p <mot_de_passe> -o <organisation> -s <space>
  ```
  {: pre}

2. Générez les données d'identification de service. `nom-clé-service` est le nom que vous donnez à vos données d'identification. Vous pouvez utiliser la commande Cloud Foundry ou la commande cURL.
  Commande Cloud Foundry :
  ```
  cf create-service-key "<nom_instance_service_conteneur_objet>" <nom-clé-service> -c '{"role":"<rôle_conteneur_objet>"}'
  ```
  {: pre}

  Exemple de commande Cloud Foundry :
  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'
  ```
  {: screen}

  Commande cURL :
  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "guid_instance_service" : "<guid_instance_service>",   "name": "<nom_utilisateur>", "role": "member"}' -X POST -H "Authorization: <jeton_bearer>" -H "Content-Type: " -H "Cookie: "
  ```
  {: pre}

3. Validez les données d'identification pour la clé de service que vous avez créée.
  Commande Cloud Foundry :
  ```
  cf service-keys <instance_service>
  ```
  {: pre}

  Exemple de clé de service de membre pour une instance intitulée Object-Storage-Acl-Test :

  ```
  {
    "auth_url": "https://identity.open.softlayer.com",
    "domainId": "8753ff40ac1a4f4a9f162ad8026b6ce0",
    "domainName": "757955",
    "password": "xxxxxxxx",
    "project": "object_storage_6046b6e2_ee53_4884_916f_89c65e4d408e",
    "projectId": "c727d7e248b448f6b268f31a1bd8691e",
    "region": "dallas",
    "role": "member",
    "userId": "3c5b516655e4479881d3d216895faedb",
    "username": "member_2afbeea1d58b1867f46c699553d1e4513e7df83a"
  }
  ```
  {: screen}

  Commande cURL :
  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <jeton_bearer>" -H "Cookie: "
  ```
  {: pre}




## Stockage d'objets dans des conteneurs via l'interface de ligne de commande {: #storing-cli}

1. Si vous n'êtes pas connecté à {{site.data.keyword.Bluemix_notm}}, connectez-vous à l'organisation et l'espace contenant votre instance d'{{site.data.keyword.objectstorageshort}}.
  ```
  cf login -a api.ng.bluemix.net -u <ID_utilisateur> -p <mot_de_passe> -o <organisation> -s <space>
  ```
  {: pre}

2. Créez un nouveau conteneur {{site.data.keyword.objectstorageshort}} en exécutant la commande suivante. Vous définissez vous-même la variable *nom_conteneur*, à ce moment là.
  ```
  swift post <nom_conteneur>
  ```
  {: pre}

**Remarque** : si vous recevez un message d'erreur, confirmez que vous avez installé [les logiciels prérequis](../ObjectStorage/os_cli.html##install-swift-client).

3. (Facultatif) - pour vérifier que votre conteneur a été créé, exécutez la commande suivante pour répertorier vos conteneurs.
  ```
  swift list
  ```
  {: pre}

4. Pour empêcher une destruction des données par un remplacement non intentionnel, [configurez la fonction de gestion des versions d'objets](../ObjectStorage/os_versioning.html#work-with-object-versioning). Si vous ne voulez pas mettre en place cette gestion, répertoriez les fichiers existants dans votre magasin et, si nécessaire, renommez le répertoire ou les fichiers avant l'envoi par téléchargement.

4. Téléchargez un fichier dans votre conteneur en exécutant la commande suivante.
  ```
  swift upload <nom_conteneur> <nom_fichier>
  ```
  {: pre}

**Remarque** : pour télécharger des fichiers qui font plus de 5 Go, des [étapes supplémentaires sont nécessaires](../ObjectStorage/os_large_files.html#large-files).


5. (Facultatif) - pour vérifier que le chargement a abouti, affichez le contenu de votre conteneur en exécutant la commande suivante :
  ```
  swift list <nom_conteneur>
  ```
  {: pre}




## Téléchargement d'objets avec Swift CLI {: #downloading-cli}


1.  Si vous n'êtes pas connecté à {{site.data.keyword.Bluemix_notm}}, connectez-vous à l'organisation et l'espace contenant votre instance d'{{site.data.keyword.objectstorageshort}}.

```
cf login -a api.ng.bluemix.net -u <ID_utilisateur> -p <mot_de_passe> -o <organisation> -s <space>
```
{: pre}

2. Pour empêcher une destruction des données par un remplacement non intentionnel, [configurez la fonction de gestion des versions d'objets](../ObjectStorage/os_versioning.html#work-with-object-versioning). Si vous ne voulez pas mettre en place cette gestion, répertoriez les fichiers existants dans votre magasin et, si nécessaire, renommez le répertoire ou les fichiers avant la réception par téléchargement.

3. Téléchargez un fichier en exécutant la commande suivante :

```
swift download <nom_conteneur> <nom_fichier>
```
{: pre}




## Suppression d'objets et de conteneurs via l'interface de ligne de commande {: #deleting-cli}

**Attention** : si vous supprimez votre conteneur, vous supprimez aussi tous les objets qui y sont stockés.

1.  Si vous n'êtes pas connecté à {{site.data.keyword.Bluemix_notm}}, connectez-vous à l'organisation et l'espace contenant votre instance d'{{site.data.keyword.objectstorageshort}}.
  ```
  cf login -a api.ng.bluemix.net -u <ID_utilisateur> -p <mot_de_passe> -o <organisation> -s <space>
  ```
  {: pre}

2. (Facultatif) - confirmez que vous disposez d'une sauvegarde de vos objets avant de supprimer vos fichiers et conteneurs.

3. Exécutez la commande suivante pour supprimer un fichier :
  ```
  swift delete <nom_conteneur> <nom_fichier>
  ```
  {: pre}

3. Pour supprimer votre conteneur, exécutez la commande suivante :
  ```
  swift delete <nom_conteneur>
  ```
  {: pre}

**Remarque** : vous pouvez planifier un [moment spécifique pour la suppression de votre objet](../ObjectStorage/os_deletion.html#schedule-object-deletion).




## Utilisation de répertoires {: #directory-cli}

#### Ajout d'un répertoire à un conteneur avec Swift CLI

Swift n'a pas de véritable structure de répertoires mais utilise la convention d’affectation de noms pour représenter la disposition d'un répertoire. Si vous spécifiez un nom de répertoire, il sera attaché à tous les noms de fichier en tant qu'élément du chemin relatif.

1. Localement, créez un répertoire et enregistrez-y votre fichier.
2. Exécutez la commande suivante pour télécharger un répertoire dans votre conteneur :
  ```
  swift upload <nom_conteneur> <nom_répertoire>
  ```
  {: pre}

#### Téléchargement d'un répertoire
Pour télécharger une structure de répertoire, utilisez le paramètre `-prefix` pour indiquer le répertoire ou la structure de répertoire que vous voulez charger.

1. Exécutez la commande suivante pour télécharger un répertoire :
  ```
  swift download <nom_conteneur> --prefix <répertoire>
  ```
  {: pre}
