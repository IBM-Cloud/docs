---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Attribution d'un accès en écriture

Un utilisateur {{site.data.keyword.objectstorageshort}} avec un [rôle admin](/docs/services/ObjectStorage/os_access_types.html) peut accorder un accès en écriture pour un autre utilisateur et proposer différentes combinaisons de liste de contrôle d'accès en écriture.
{: shortdesc}

<table>
<caption> Tableau 1. Options d'octroi de droits d'accès en écriture </caption>
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
    <td> <code> &#42;:ID_utilisateur </code> </td>
  </tr>
  <tr>
    <td> Ecriture pour chaque utilisateur dans un projet spécifié </td>
    <td>  <code> ID_projet:&#42; </code> </td>
  </tr>
  <tr>
    <td> Ecriture pour chaque utilisateur dans chaque projet </td>
    <td>  <code> &#42;:&#42; </code> </td>
  </tr>
</table>



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

2. Accordez l'accès en écriture en exécutant la commande suivante.

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
