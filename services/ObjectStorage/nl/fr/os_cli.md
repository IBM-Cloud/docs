---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
# Commencer à utiliser {{site.data.keyword.objectstorageshort}}  {: #using-object-storage}
*Dernière mise à jour : 19 octobre 2016*
{: .last-updated}

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
  sudo pip install python-swiftclient
  ```
  {: pre}

Pour installer le client Python Keystone, exécutez la commande suivante :
  ```
  sudo pip install python-keystoneclient
  ```
  {: pre}




## Configuration du client {: #setup-swift-client}

Pour configurer le client Swift, vous devez `exporter` vos informations d'authentification. Vous pouvez utiliser vos données d'identification disponibles dans l'interface utilisateur ou [générer de nouvelles données d'identification](../ObjectStorage/os_cli.html#generating-cli).

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
  {: codeblock}




## Génération des données d'identification de service {{site.data.keyword.objectstorageshort}} {: #generating-cli}

Pour générer des données d'identification de service en utilisant Swift CLI, procédez comme suit.

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}} en tant qu'utilisateur avec un rôle développeur. Vous devez vous trouver au sein de l'espace de l'instance de service que vous voulez gérer.
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
      cf service-key <nom_clé_service> <nom_membre>
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

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}}. Assurez-vous d'être dans la bonne organisation et dans l'espace qui convient pour travailler avec votre instance d'{{site.data.keyword.objectstorageshort}}.
    ```
    cf login -a api.ng.bluemix.net -u <ID_utilisateur> -p <mot_de_passe> -o <organisation> -s <space>
    ```
    {: pre}
2. Créez un nouveau conteneur  en exécutant la commande suivante. Vous définissez vous-même la variable *nom_conteneur*, à ce moment là.
    ```
    swift post <nom_conteneur>
    ```
    {: pre}
3. (*Facultatif*) Pour vérifier que votre conteneur a été créé, exécutez la commande suivante pour répertorier vos conteneurs.
    ```
    swift list
    ```
    {: pre}
4. Téléchargez un fichier dans votre conteneur en exécutant la commande suivante.
    ```
    swift upload <nom_conteneur> <nom_fichier>
    ```
    {: pre}
    **Remarque** : pour télécharger des fichiers qui font plus de 5 Go, des étapes supplémentaires sont nécessaires. Pour plus d'informations, voir [Utilisation de fichiers volumineux](../ObjectStorage/os_large_files.html#large-files).
5. (*Facultatif*) Pour vérifier que le chargement a abouti, affichez le contenu de votre conteneur en exécutant la commande suivante :
    ```
    swift list <nom_conteneur>
    ```
    {: pre}

**Remarque** : quand vous téléchargez un fichier portant le même nom, {{site.data.keyword.objectstorageshort}} remplace le fichier stocké par le nouveau fichier. Si vous téléchargez un fichier et effectuez des modifications, prenez soin de donner un autre nom au fichier ou [configurez la fonctionnalité de gestion de versions](../ObjectStorage/os_versioning.html#work-with-object-versioning) avant le téléchargement pour conserver les deux versions du fichier.



## Téléchargement d'objets avec Swift CLI {: #downloading-cli}

1.  Connectez-vous à {{site.data.keyword.Bluemix_notm}}. Assurez-vous d'être dans la bonne organisation et dans l'espace qui convient pour travailler avec votre instance d'{{site.data.keyword.objectstorageshort}}.
    ```
    cf login -a api.ng.bluemix.net -u <ID_utilisateur> -p <mot_de_passe> -o <organisation> -s <space>
    ```
    {: pre}
2. Téléchargez un fichier en exécutant la commande suivante :
    ```
    swift download <nom_conteneur> <nom_fichier>
    ```
    {: pre}




## Suppression d'objets et de conteneurs via l'interface de ligne de commande{: #deleting-cli}

1.  Connectez-vous à {{site.data.keyword.Bluemix_notm}}. Assurez-vous d'être dans la bonne organisation et dans l'espace qui convient pour travailler avec votre instance d'{{site.data.keyword.objectstorageshort}}.
    ```
    cf login -a api.ng.bluemix.net -u <ID_utilisateur> -p <mot_de_passe> -o <organisation> -s <space>
    ```
    {: pre}
2. Exécutez la commande suivante pour supprimer un fichier :
    ```
    swift delete <nom_conteneur> <nom_fichier>
    ```
    {: pre}
    **Remarque** : vous pouvez planifier un [moment spécifique pour la suppression de votre objet](../ObjectStorage/os_deletion.html#schedule-object-deletion).
3. Pour supprimer votre conteneur, exécutez la commande suivante :
    ```
    swift delete <nom_conteneur>
    ```
    {: pre}
    **Attention** : si vous supprimez votre conteneur, vous supprimez aussi tous les objets qui y sont stockés.
## Utilisation de répertoires {: #directory-cli}

#### Ajout d'un répertoire à un conteneur avec Swift CLI

Swift n'a pas de véritable structure de répertoires mais utilise la convention d’affectation de noms pour représenter la disposition d'un répertoire. Si vous spécifiez un nom de répertoire, il sera attaché à tous les noms de fichier en tant qu'élément du chemin relatif.

1. Exécutez la commande suivante pour ajouter un répertoire à un conteneur :
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
