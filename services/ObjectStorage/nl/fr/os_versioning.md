---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilisation de la gestion des versions d'objets {: #work-with-object-versioning}

*Dernière mise à jour : 19 octobre 2016*
{: .last-updated}

Avec la fonctionnalité de gestion des versions d'objets, vous êtes en mesure de conserver des versions séparées de vos objets sans renommer vos fichiers, ce qui vous permet de disposer d'un historique de chaque objet et d'effectuer un suivi des changements effectués.
{: shortdesc}


### Configuration de la gestion des versions d'objets {: #setting-up-versioning}

Vous pouvez configurer des versions de chaque objet dans votre conteneur en utilisant le paramètre `X-Versions-Location`. Pour ce
faire, créez un conteneur supplémentaire dans lequel placer les anciennes versions de vos objets comme suit.

Vous pouvez configurer la fonctionnalité de gestion des versions d'objets via le client Swift ou en utilisant des commandes cURL.
* Si vous utilisez le client Swift, exécutez la commande suivante :

    ```
    swift post <nom_conteneur> -H "X-Versions-Location:<nom_conteneur_sauvegarde>"
    ```
    {: pre}
    
* Si vous utilisez cURL, vous pouvez le configurer ainsi :

    ```
    curl -i -X PUT -H "X-Auth-Token: <jeton>" -H "X-Versions-Location:<nom_conteneur_sauvegarde>" https://<url-stockage-objet>/<nom_conteneur>
    ```
    {: pre}
    
**Remarque** : les objets de votre conteneur de sauvegarde sont nommés automatiquement selon le format suivant : `<Longueur><Nom_objet>/<Nom_objet>`.
<table>
  <tr>
    <th> Attribut </th>
    <th> Description </th>
  </tr>
  <tr>
    <td> `Longueur` </td>
    <td> Longueur du nom de votre objet. Il s'agit d'un nombre hexadécimal de trois caractères remplis avec des zéros. </td>
  </tr>
  <tr>
    <td> `Nom_objet` </td>
    <td> Nom de votre objet. </td>
  </tr>
  <tr>
    <td> `Horodatage` </td>
    <td> Horodatage du téléchargement initial de cette version particulière de l'objet. </td>
  </tr>
</table>

### Désactivation de la gestion des versions d'objets{: #disabling-versioning}

Vous pouvez désactiver la gestion des versions via le client Swift ou en utilisant les commandes cURL.

* Pour utiliser le client Swift, exécutez la commande suivante :

    ```
    swift post <nom_conteneur> -H "X-Remove-Versions-Location:"
    ```
    {: pre}
    
* Exécutez la commande cURL suivante pour désactiver la gestion des versions :

    ```
    cURL -i -X POST -H "X-Auth-Token: <jeton>" -H "X-Remove-Versions-Location: anyvalue" https://<url-stockage-objet>/<nom_conteneur>
    ```
    {: pre}


### Tutoriel relatif à la gestion des versions d'objets{: #versioning-tutorial}
<!--- SHAWNA: This needs more background information. What are they doing? Why are they doing it? What is the outcome? --->

Vous pouvez utiliser le tutoriel suivant pour comprendre comment se déroule le cycle de vie complet de la gestion des versions d'objets.

1. Créez un conteneur intitulé `conteneur_un`.

    ```
    swift post conteneur_un
    ```
    {: pre}
    
3. Créez un second conteneur, intitulé `conteneur_deux`.

    ```
    swift post conteneur_deux
    ```
    {: pre}
    
2. Configurez la gestion des versions.

    ```
    swift post conteneur_un -H "X-Versions-Location:conteneur_deux"
    ```
    {: pre}
    
4. Téléchargez un objet dans votre conteneur principal, pour la première fois.

    ```
    swift upload conteneur_un object
    ```
    {: pre}
    
7. Téléchargez une nouvelle version de l'objet dans conteneur_un. Quand vous téléchargez une nouvelle version de votre fichier, la version précédente est automatiquement déplacée dans le conteneur de sauvegarde que vous avez spécifié quand vous avez configuré la gestion des versions.

    ```
    swift upload conteneur_un object
    ```
    {: pre}
    
8. Pour définir la nouvelle version de votre fichier dans le conteneur, répertoriez les objets de conteneur_un.

    ```
    swift list conteneur_un
    ```
    {: pre}
    
9. Répertoriez les objets de conteneur_deux. La version précédente de votre fichier sera stockée dans ce conteneur.

    ```
    swift list conteneur_deux
    ```
    {: pre}
    
10. Supprimez l'objet dans conteneur_un. Quand vous supprimez l'objet, la version précédente qui se trouve dans le conteneur de sauvegarde sera automatiquement déplacée dans votre conteneur principal.

    ```
    swift delete conteneur_un object
    ```
    {: pre}
    
11. Répertoriez le contenu des deux conteneurs. `conteneur_un` comporte votre fichier d'origine et `conteneur_deux` est vide.

    ```
    swift list conteneur_un
    swift list conteneur_deux
    ```
    {: pre}
