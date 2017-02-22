---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Génération des données d'identification de service {: #credentials}

Les données d'identification sont utilisées pour fournir l'authentification et la sécurité pour le service. Vous pouvez générer de nouvelles données d'identification en utilisant l'interface de ligne de commande ou l'interface utilisateur {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}


## Pour ajouter les données d'identification dans l'interface utilisateur :

1. Dans l'onglet **Données d'identification pour le service**, cliquez sur **Nouvelles données d'identification** et donnez-leur un nom.
2. (Facultatif) - dans la zone de texte **Ajouter des paramètres de configuration en ligne**, entrez les données d'identification pour le rôle avec le [type d'accès](/docs/services/ObjectStorage/os_access_types.html) que vous voulez donner. Ces informations doivent être formatées en tant que contenu JSON.
    - Pour créer un utilisateur administrateur : `{"role":"admin"}`
    - Pour créer un utilisateur non administrateur : `{"role":"member"}`
3. Cliquez sur **Ajouter**.


## Pour ajouter des données d'identification en utilisant les commandes Cloud Foundry dans l'interface de ligne de commande :

1. Si vous n'êtes pas connecté à {{site.data.keyword.Bluemix_notm}}, connectez-vous en tant qu'utilisateur avec un rôle développeur. Vous devez vous trouver au sein de l'espace de l'instance de service que vous voulez gérer.
  ```
  cf login -a api.ng.bluemix.net -u <ID_utilisateur> -p <mot_de_passe> -o <organisation> -s <space>
  ```
  {: pre}

2. Générez les données d'identification de service. Donnez un nom à vos données d'identification en remplaçant la variable `nom-clé-service`. Vous pouvez, si vous le souhaitez, affecter un [rôle utilisateur](/docs/services/ObjectStorage/os_access_types.html).

  ```
  cf create-service-key "<nom_instance_service>" <nom-clé-service> -c '{"role":"<rôle_utilisateur>"}'
  ```
  {: pre}

  Exemple :
  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'
  ```
  {: screen}

3. Validez les données d'identification pour la clé que vous avez créée.

  ```
  cf service-keys <nom_instance_service>
  ```
  {: pre}

  Exemple de clé pour une instance nommée Object-Storage-Acl-Test, pour un utilisateur avec un rôle de membre :

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



#### Pour ajouter des données d'identification en utilisant les commandes cURL dans l'interface de ligne de commande :

1. Si vous n'êtes pas connecté à {{site.data.keyword.Bluemix_notm}}, connectez-vous en tant qu'utilisateur avec un rôle développeur. Vous devez vous trouver au sein de l'espace de l'instance de service que vous voulez gérer.

  ```
  cf login -a api.ng.bluemix.net -u <ID_utilisateur> -p <mot_de_passe> -o <organisation> -s <space>
  ```
  {: pre}

2. Exécutez la commande suivante pour générer les données d'identification. 

  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<guid_instance_service>",   "name: <nom_instance_service>", "role: <rôle_utilisateur>"}' -X POST -H "Authorization: <jeton_bearer>" -H "Content-Type: <type_contenu" -H "Cookie: <cookie>"
  ```
  {: pre}

  <table>
  <caption> Tableau 1. Explication des variables des données d'identification du service dans la commande cURL</caption>
    <tr>
      <th> Variable  </th>
      <th> Explication </th>
    </tr>
    <tr>
      <td> <code>https://api.ng.bluemix.net/v2/service_keys</code> </td>
      <td> Noeud final de clé de service  </td>
    </tr>
    <tr>
      <td><i> guid_instance_service </i></td>
      <td> Vous le trouverez dans votre URL.  </td>
    </tr>
    <tr>
      <td><i> nom</i></td>
      <td> Nom de votre instance de service. </td>
    </tr>
    <tr>
      <td><i> rôle </i></td>
      <td> Spécifie le <a href= /docs/services/ObjectStorage/os_constructing.html>rôle utilisateur</a> en tant qu'administrateur ou membre. </td>
    </tr>
    <tr>
      <td><i> jeton_bearer </i></td>
      <td> Jeton reçu lors de l'authentification de votre instance auprès de Keystone. </td>
    </tr>
  </table>



3. Validez vos données d'identification en exécutant la commande suivante.

  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <jeton_bearer>" -H "Cookie: "
  ```
  {: screen}
