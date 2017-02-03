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


# Attribution d'un accès en lecture

Un utilisateur {{site.data.keyword.objectstorageshort}} avec un [rôle admin](/docs/services/ObjectStorage/os_access_types.html) peut accorder un accès en lecture à un conteneur pour un autre utilisateur et proposer différentes combinaisons de liste de contrôle d'accès en lecture.
{: shortdesc}

<table>
<caption> Tableau 1. Options d'octroi de droits d'accès en lecture </caption>
  <tr>
    <th> Droit d'accès </th>
    <th> Options LCA en lecture </th>
  </tr>
  <tr>
    <td> Lecture pour tous les référents quelle que soit leur affiliation de compte </td>
    <td> <code> .r,&#42;  </code> </td>
  </tr>
  <tr>
    <td> Lecture et liste pour tous les référents et listes </td>
    <td> <code> .r:&#42;,.rlistings </code> </td>
  </tr>
  <tr>
    <td> Lecture et liste pour un utilisateur spécifié dans un projet spécifique </td>
    <td> <code> ID_projet:ID_utilisateur </code> </td>
  </tr>
  <tr>
    <td> Lecture et liste pour un utilisateur spécifié dans chaque projet </td>
    <td> <code> &#42;:ID_utilisateur </code> </td>
  </tr>
  <tr>
    <td> Lecture et liste pour chaque utilisateur dans un projet spécifié </td>
    <td> <code> ID_projet:&#42; </code> </td>
  </tr>
  <tr>
    <td> Lecture et liste pour chaque utilisateur dans chaque projet  </td>
    <td> <code> &#42;:&#42; </code> </td>
  </tr>
</table>



1. Authentifiez vos données d'identification. Vous pouvez utiliser les données d'identification qui se trouvent dans l'onglet des données d'identification de service de l'interface utilisateur ou générer de nouvelles données d'identification. Pour plus d'informations sur la génération de nouvelles données d'identification, voir la rubrique relative à la [génération des données d'identification de service](/docs/services/ObjectStorage/os_credentials.html). Vous recevez votre URL {{site.data.keyword.objectstorageshort}} et votre jeton d'authentification dans une sortie spécifique.

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

    Exemple : La valeur `X-Container-Read` indique à qui le droit d'accès en lecture est accordé et à quel conteneur.

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
