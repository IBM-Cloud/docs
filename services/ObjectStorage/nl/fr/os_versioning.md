---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Configuration de la gestion des versions d'objets {: #setting-up-versioning}

La gestion des versions d'objets vous permet de conserver les anciennes versions de vos objets en les stockant automatiquement dans un conteneur de sauvegarde, ce qui vous permet de disposer d'un historique de chaque objet et d'effectuer un suivi des changements apportés.
{: shortdesc}

Quand vous téléchargez une nouvelle version de votre fichier dans votre conteneur principal, la version précédente est automatiquement déplacée dans votre conteneur de sauvegarde. Si vous supprimez le fichier depuis votre conteneur principal, la version la plus récente est automatiquement déplacée depuis le conteneur de sauvegarde vers le conteneur principal pour remplacer le fichier supprimé.

1. Créez un conteneur et donnez-lui un nom. Remplacez la variable *nom_conteneur* par le nom que vous voulez donner à votre conteneur.

    ```
    swift post <nom_conteneur>
    ```
    {: pre}

2. Créez un second conteneur qui vous servira de conteneur de stockage et donnez-lui un nom.

    ```
    swift post <nom_conteneur_sauvegarde>
    ```
    {: pre}

3. Configurez la gestion des versions.

    Commande Swift :

    ```
    swift post <nom_conteneur> -H "X-Versions-Location:<nom_conteneur_sauvegarde>"
    ```
    {: pre}

    Commande cURL :

    ```
    curl -i -X PUT -H "X-Auth-Token: <jeton>" -H "X-Versions-Location:<nom_conteneur_sauvegarde>" https://<url-stockage-objet>/<nom_conteneur>
    ```
    {: pre}

4. Téléchargez un objet dans votre conteneur principal, pour la première fois.

    ```
    swift upload <nom_conteneur> <object>
    ```
    {: pre}

5. Modifiez votre objet.

6. Téléchargez une nouvelle version de l'objet dans votre conteneur principal.

    ```
    swift upload <nom_conteneur> <object>
    ```
    {: pre}

7.  Les objets de votre conteneur de sauvegarde sont nommés automatiquement selon le format suivant : `<Longueur><Nom_objet>/<Horodatage>`.
  <table>
    <tr>
      <th> Attribut </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i>Longueur</i> </td>
      <td> Longueur du nom de votre objet. Il s'agit d'un nombre hexadécimal de trois caractères remplis avec des zéros. </td>
    </tr>
    <tr>
      <td> <i>Nom_objet</i> </td>
      <td> Nom de votre objet. </td>
    </tr>
    <tr>
      <td> <i>Horodatage</i> </td>
      <td> Horodatage du téléchargement initial de cette version particulière de l'objet. </td>
    </tr>
  </table>

  Tableau 1 : description des attributs de noms

6. Répertoriez les objets de votre conteneur principal pour voir la nouvelle version de votre fichier.

    ```
    swift list --lh <nom_conteneur>
    ```
    {: pre}

7. Répertoriez les objets de votre conteneur de sauvegarde. Vous voyez la version précédente de votre fichier qui est stockée dans ce conteneur. Notez qu'un horodatage a été ajouté à votre fichier.

    ```
    swift list --lh <nom_conteneur_sauvegarde>
    ```
    {: pre}

8. Supprimez l'objet dans votre conteneur principal. Quand vous supprimez l'objet, la version la plus récente qui se trouve dans votre conteneur de sauvegarde est automatiquement déplacée dans votre conteneur principal.

    ```
    swift delete <nom_conteneur> <object>
    ```
    {: pre}

9. (Facultatif) - désactivez la gestion des versions d'objets.

    Commande Swift :

    ```
    swift post <nom_conteneur> -H "X-Remove-Versions-Location:"
    ```
    {: pre}

    Commande cURL :

    ```
    cURL -i -X POST -H "X-Auth-Token: <jeton>" -H "X-Remove-Versions-Location: anyvalue" https://<url-stockage-objet>/<nom_conteneur>
    ```
    {: pre}
