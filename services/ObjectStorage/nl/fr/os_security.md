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


# Sécurisation des fichiers {: #understanding-authentication}


## Présentation des données d'identification de service {: #understanding-credentials}

Les données d'identification sont utilisées pour fournir l'authentification et la sécurité pour le service. Un ensemble de données d'identification est généré automatiquement quand une instance est mise à disposition. Le client Swift prend les informations d'authentification dans les variables d'environnement du tableau ci-après.

<table>
  <tr>
    <th> Variable d'environnement </th>
    <th> Description </th>
  </tr>
  <tr>
    <td> <code>OS_USER_ID</code> </td>
    <td> Votre ID utilisateur {{site.data.keyword.objectstorageshort}}. </td>
  </tr>
  <tr>
    <td> <code>OS_PASSWORD</code> </td>
    <td> Mot de passe pour votre instance {{site.data.keyword.objectstorageshort}}. </td>
  </tr>
  <tr>
    <td> <code>OS_PROJECT_ID</code> </td>
    <td> Votre ID projet. </td>
  </tr>
  <tr>
    <td> <code>OS_REGION_NAME</code> </td>
    <td> Région dans laquelle vos objets sont stockés. {{site.data.keyword.objectstorageshort}} est disponible dans les régions Dallas et Londres. </td>
  </tr>
  <tr>
    <td> <code>OS_AUTH_URL</code> </td>
    <td> URL du noeud final. Assurez-vous que `/v3` est ajouté à la fin de l'URL. </td>
  </tr>
</table>

Tableau 1 : variables d'authentification et descriptions

####  Ajout de données d'identification de service dans l'interface utilisateur
1. Dans l'onglet **Données d'identification pour le service**, cliquez sur **Nouvelles données d'identification** et donnez-leur un nom.
2. (*Facultatif*) Dans la zone de texte **Ajouter des paramètres de configuration en ligne**, entrez les données d'identification pour le rôle que vous voulez créer. Ces informations doivent être formatées en tant que contenu JSON. Pour plus d'informations sur les rôles utilisateur {{site.data.keyword.objectstorageshort}}, voir [Types d'accès](../os_security.html#access-types).
    - Pour créer un utilisateur administrateur : `{"role":"admin"}`
    - Pour créer un utilisateur non administrateur : `{"role":"member"}`
3. Cliquez sur **Ajouter**.


## Types d'accès {: #access-types}

L'accès au service est géré par les rôles utilisateur et les listes de contrôle d'accès aux conteneurs. Les utilisateurs {{site.data.keyword.objectstorageshort}} peuvent être ou non des administrateurs. Les listes de contrôle d'accès sont activées par les administrateurs au niveau conteneur et ne sont pas disponibles pour l'instance de service, le compte de stockage ou au niveau du projet.

<table>
  <tr>
    <th> Utilisateurs administrateur (admin) </th>
    <th> Utilisateurs non administrateur (membre) </th>
  </tr>
  <tr>
    <td> Gèrent le contrôle d'accès </td>
    <td> Par défaut, n'ont pas d'accès au service ou à ses conteneurs </td>
  </tr>
  <tr>
    <td> Peuvent créer et supprimer des conteneurs </td>
    <td> Peuvent exécuter des actions basées sur les listes de contrôle d'accès en lecture/écriture des conteneurs </td>
  </tr>
  <tr>
    <td> Peuvent lire et écrire dans les conteneurs </td>
    <td> Peuvent effectuer les actions, comme défini par l'administrateur </td>
  </tr>
</table>

Tableau 2 : définition des rôles utilisateur

Vous pouvez gérer les utilisateurs {{site.data.keyword.objectstorageshort}} via l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, l'API Cloud Foundry API ou l'interface de ligne de commande Cloud Foundry.




## Attribution d'un accès en lecture {: #read-access}

Un utilisateur {{site.data.keyword.objectstorageshort}} avec un rôle admin peut accorder un accès en lecture à un conteneur pour un autre utilisateur et proposer différentes combinaisons de liste de contrôle d'accès en lecture.

<table>
  <tr>
    <th> Droit d'accès </th>
    <th> Options LCA en lecture </th>
  </tr>
  <tr>
    <td> Lecture pour tous les référents quelle que soit leur affiliation de compte </td>
    <td> <code> .r,*` </code> </td>
  </tr>
  <tr>
    <td> Lecture et liste pour tous les référents et listes </td>
    <td> <code>.r:*,.rlistings</code> </td>
  </tr>
  <tr>
    <td> Lecture et liste pour un utilisateur spécifié dans un projet spécifique </td>
    <td> <code> ID_projet:ID_utilisateur </code> </td>
  </tr>
  <tr>
    <td> Lecture et liste pour un utilisateur spécifié dans chaque projet </td>
    <td> <code> *:ID_utilisateur </code> </td>
  </tr>
  <tr>
    <td> Lecture et liste pour chaque utilisateur dans un projet spécifié </td>
    <td> <code> ID_projet:* </code> </td>
  </tr>
  <tr>
    <td> Lecture et liste pour chaque utilisateur dans chaque projet  </td>
    <td> <code> *:* </code> </td>
  </tr>
</table>

Tableau 3 : droits d'accès en lecture par option



1. Authentifiez vos données d'identification. Vous pouvez utiliser les données d'identification qui se trouvent dans l'onglet des données d'identification de service de l'interface utilisateur ou générer de nouvelles données d'identification. Pour plus d'informations sur la génération de nouvelles données d'identification, voir la rubrique relative à la [génération des données d'identification de service](insert link here). Vous recevez votre URL {{site.data.keyword.objectstorageshort}} et votre jeton d'authentification dans une sortie spécifique.
    Commande Swift :

    ```
    export OS_USER_ID=<ID_utilisateur>
  export OS_PASSWORD=<mot_de_passe>
  export OS_TENANT_ID=<ID_projet>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<région>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

    swift auth
    ```
    {: codeblock}

    Commande cURL :

    ```
    curl -i -H "X-Auth-User: <ID_utilisateur>" -H "X-Auth-Key: <mot_de_passe>" <URL_auth>
    ```
    {: pre}

2. Accordez l'accès en lecture en exécutant la commande suivante :
    Commande Swift :

    ```
    swift post <nom_conteneur> --read-acl "<ID_utilisateur>:<ID_projet>"
    ```
    {: pre}

    Commande cURL :

    ```
    curl -i <URL_STOCKAGE_SE> -X POST -H "Content-Length: 0" -H "X-Container-Read: <ID_titulaire>:<ID_projet>" -H "X-Auth-Token: <JETON_AUTH_SE>"
    ```
    {: pre}
    **Remarque** : utilisez une virgule (,) pour séparer les listes de contrôle d'accès.


3. Vérifiez la valeur de liste de contrôle d'accès en lecture.
    Commande Swift :

    ```
    swift stat <nom_conteneur>
    ```
    {: pre}
    Commande cURL :

    ```
    curl -i <URL_STOCKAGE_SE> -I -H "X-Auth-Token:<JETON_AUTH_SE>"
    ```
    {: pre}

    La sortie exemple ci-dessous montre une attribution d'un accès en lecture :

    ```
    HTTP/1.1 204 No Content
  Content-Length: 0
  X-Container-Object-Count: 1
  Accept-Ranges: bytes
  X-Storage-Policy: standard
  X-Container-Read: c727d7e248b448f6b268f31a1bd8691e:3c5b516655e4479881d3d216895faedb
  X-Container-Bytes-Used: 31512
  X-Timestamp: 1462818314.11220
  Content-Type: text/plain; charset=utf-8
  X-Trans-Id: txad7fe001da274b9ba39a6-005772e4d6
  Date: Tue, 28 Jun 2016 20:57:58 GMT
    ```
    {: screen}



## Attribution d'un accès en écriture {: #write-access}

Un utilisateur {{site.data.keyword.objectstorageshort}} avec un rôle admin peut accorder un accès en écriture à un conteneur pour un autre utilisateur et proposer différentes combinaisons de liste de contrôle d'accès en écriture.

<table>
  <tr>
    <th> Droit d'accès </th>
    <th> Options LCA en écriture </th>
  </tr>
  <tr>
    <td> Ecriture pour un utilisateur spécifié dans un projet spécifique </td>
    <td> <code> ID_projet:ID_utilisateur </code> </td>
  </tr>
  <tr>
    <td> Ecriture pour un utilisateur spécifié dans chaque projet </td>
    <td> <code> *:ID_utilisateur </code> </td>
  </tr>
  <tr>
    <td> Ecriture pour chaque utilisateur dans un projet spécifié </td>
    <td>  <code> ID_projet:* </code> </td>
  </tr>
  <tr>
    <td> Ecriture pour chaque utilisateur dans chaque projet </td>
    <td>  <code> *:* </code> </td>
  </tr>
</table>

Tableau 4 : droits d'accès en écriture par option



1. Authentifiez vos données d'identification en utilisant les informations des données d'identification de service que vous avez créées.  Vous recevez votre URL {{site.data.keyword.objectstorageshort}} et votre jeton d'authentification dans une sortie spécifique.
    Commande Swift :

    ```
    export OS_USER_ID="<ID_utilisateur>"
    export OS_PASSWORD="<mot_de_passe>"
    export OS_TENANT_ID=<ID_projet>
    export OS_AUTH_URL=https://identity.open.softlayer.com/v3
    export OS_REGION_NAME=<région>
    export OS_IDENTITY_API_VERSION=3
    export OS_AUTH_VERSION=3

    swift auth
    ```
    {: codeblock}

    Commande cURL :

    ```
    curl -i -H "X-Auth-User:< ID_utilisateur>" -H "X-Auth-Key:< mot_de_passe>" https://identity.open.softlayer.com/v3
    ```
    {: pre}

2. Accordez l'accès en écriture en exécutant la commande suivante :
    Commande Swift :

    ```
    swift post <nom_conteneur> --write-acl "<ID_utilisateur>:<ID_projet>"
    ```
    {: pre}

    Commande cURL :

    ```
    curl -i <URL_STOCKAGE_SE> -X POST -H "Content-Length: 0" -H "X-Container-Write: <ID_utilisateur>: <ID_projet>" -H "X-Auth-Token:<JETON_AUTH_SE>"
    ```
    {: pre}

    **Remarque** : utilisez une virgule (,) pour séparer les listes de contrôle d'accès.

3. Vérifiez la valeur de liste de contrôle d'accès en écriture.
    Commande Swift :

    ```
    swift stat <nom_conteneur>
    ```
    {: pre}

    Commande cURL :

    ```
    curl -i <URL_STOCKAGE_SE> -I -H "X-Auth-Token:<JETON_AUTH_SE>"
    ```
    {: pre}



## Retrait de l'accès {: #removing-access}

Pour retirer les listes de contrôle d'accès en lecture d'un conteneur :
* Commande Swift :

    ```
    swift post <nom_conteneur> --read-acl “”
    ```
    {: pre}

*  Commande cURL :

    ```
    curl -i <URL_STOCKAGE_SE> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <JETON_AUTH_SE>"
    ```
    {: pre}

Pour retirer les listes de contrôle d'accès en écriture d'un conteneur :

* Commande Swift :

    ```
    swift post <nom_conteneur> --write-acl “”
    ```
    {: pre}

*  Commande cURL :

    ```
    curl -i <URL_STOCKAGE_SE> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <JETON_AUTH_SE>"
    ```
    {: pre}

Pour vérifier que vous avez retiré une liste de contrôle d'accès :

* Commande Swift :

    ```
    swift stat <nom_conteneur>
    ```
    {: pre}

  La sortie exemple suivante affiche des listes de contrôle d'accès vierges (Read ACL et Write ACL), ce qui indique que l'accès a été retiré.

  ```
           Account: AUTH_c727d7e248b448f6b268f31a1bd8691e
       Container: Test
         Objects: 1
           Bytes: 31512
        Read ACL:
       Write ACL:
         Sync To:
        Sync Key:
   Accept-Ranges: bytes
X-Storage-Policy: standard
     X-Timestamp: 1462818314.11220
      X-Trans-Id: txf04968bc9ef8431982b77-005772e34b
    Content-Type: text/plain; charset=utf-8
  ```
  {: screen}

* Commande cURL :
  ```
  curl -i <URL_STOCKAGE_SE> -I -H "X-Auth-Token:<JETON_AUTH_SE>"
  ```
  {: pre}
