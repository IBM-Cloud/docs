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


# Stockage d'objets volumineux {: #large-files}

Les téléchargements sont limités à une taille maximale de 5 Go par téléchargement. Vous pouvez toutefois segmenter les objets plus volumineux en pièces plus petites et utiliser un fichier manifeste pour concaténer les segments. Une
fois un objet concaténé, sa taille n'est pas limitée.
{: shortdesc}

Les objets volumineux peuvent être dynamiques ou statiques. Dans le cas d'objets statiques volumineux (SLO), les segments n'ont pas besoin de résider dans le
même conteneur ; chaque segment peut être placé dans le conteneur de votre choix et porter un nom quelconque. Dans le cas d'objets dynamiques volumineux,
le client Swift crée un conteneur et les segments numérotés sont téléchargés en parallèle dans le conteneur.


## Objets dynamiques volumineux : {: #dynamic}

Vous pouvez télécharger des objets dynamiques volumineux de deux manières :
  * Laisser le client Swift gérer tout automatiquement
  * Utiliser l'API Swift pour le faire vous-même

#### Utilisation du client Swift pour traiter les objets dynamiques volumineux

Le client Swift utilise le paramètre `-segment-size` pour décomposer votre objet en élément plus petits. Le client crée un nouveau conteneur, avec le nom du conteneur dans lequel vous voulez télécharger des fichiers et ajoute un suffixe incluant le numéro de segment (`<nom_conteneur>_segments`). Les segments sont téléchargés en parallèle. Une fois que tous les segments ont été envoyés par téléchargement, leur réception par téléchargement s'effectue sous la forme d'un objet concaténé dans un fichier manifeste avec le nom de fichier d'origine.

1. Après que vous vous soyez connecté à {{site.data.keyword.Bluemix_notm}} et que vous êtes prêt à procéder au téléchargement, exécutez la commande suivante pour segmenter votre fichier.
    ```
    swift upload <nom_conteneur> <nom_fichier> --segment-size <taille_en_octets>
    ```
    {: pre}

#### Utilisation de l'API Swift pour gérer les objets DLO

Vous pouvez segmenter vous-même les objets pour qu'ils fassent 5 Go ou moins puis les télécharger via l'API Swift.

**Remarque **: Lors du téléchargement, tous les segments doivent être téléchargés avant le fichier manifeste. Si l'objet est téléchargé
avant que tous ses segments aient été téléchargés, la concaténation de l'objet téléchargé est incohérente.

Vous pouvez télécharger des fichiers volumineux en procédant comme suit.

1. Triez les segments par nom dans l'ordre dans lequel ils doivent être concaténés pour former l'objet d'origine.
2. Téléchargez vos segments dans un conteneur qui est séparé du conteneur qui renferme le fichier manifeste. La régulation des téléchargements commence
après
que le dixième segment ait été téléchargé, ce qui accroît considérablement le temps de téléchargement.  

    ```
    curl -i -X PUT --data-binary @segment1 -H "X-Auth-Token: <jeton>" https://<url-stockage-objet>/<nom_conteneur>/<nom_objet>/000001
    curl -i -X PUT --data-binary @segment2 -H "X-Auth-Token: <jeton>" https://<url-stockage-objet>/<nom_conteneur>/<nom_objet>/000002
    ```
    {: pre}

3. Téléchargez un fichier manifeste vide avec l'en-tête `X-Object-Manifest` défini sur la valeur `<conteneur>/prefix>` correspondante.

    ```
    curl -i -X PUT -H "X-Auth-Token: <jeton>" -H "X-Object-Manifest: <nom_conteneur>/<nom_objet>/" https://<url-stockage-objet>/<nom_conteneur_manifeste>/<nom_objet>
    ```
    {: pre}

    **Remarque** : le fichier manifeste doit être vide. Si ce n'est pas le cas, le contenu du fichier est considéré comme l'un des segments
et échoue dans l'ordre de concaténation dicté par les noms triés.
4. Téléchargez l'objet. Vous recevez alors l'objet complet. Vous pouvez ajouter ou retirer des segments sans avoir à mettre à jour le fichier manifeste. Les
segments dont le préfixe est correct sont conservés dans l'objet. La suppression du manifeste ne supprime pas les segments.

    ```
    curl -i -O -H "X-Auth-Token: <jeton>" https://<url-stockage-objet>/<nom_conteneur_manifeste>/<nom_objet>
    ```
    {: pre}


## Objets statiques volumineux {: #static}

Les objets statiques volumineux utilisent des segments et un fichier manifeste, mais vous permettent plus de contrôle. Les segments d'un objet statique
volumineux n'ont pas besoin d'être dans le même conteneur ; chaque conteneur peut être stocké dans le conteneur de votre choix et porter un nom quelconque. Les segments doivent toutefois faire au moins 1 Mo. Vous
n'avez pas besoin de définir un en-tête pour le fichier manifeste, bien que l'en-tête “X-Static-Large-Object” soit automatiquement ajouté et défini à
True après qu'un manifeste correct ait été téléchargé.
{: shortdesc}

Le fichier manifeste est un document JSON qui fournit les détails des segments et doit être téléchargé après téléchargement de tous les segments. Les données
fournies pour chaque segment dans le manifeste sont comparées aux métadonnées des segments réels. En cas d'incohérence, le manifeste n'est pas téléchargé.

<table>
<caption> Tableau.1 Attributs JSON dans le fichier manifeste </caption>
  <tr>
    <th> Attribut </th>
    <th> Description </th>
  </tr>
  <tr>
    <td> <i> path </i> </td>
    <td> Emplacement et nom du segment. Spécifié sous la forme nom_conteneur/nom_objet. </td>
  </tr>
  <tr>
    <td> <i> etag </i> </td>
    <td> Fourni par la demande PUT quand l'objet est téléchargé. Vous pouvez aussi le trouver en effectuant une action HEAD sur l'objet. </td>
  </tr>
  <tr>
    <td> <i> size_bytes </i> </td>
    <td> Taille de l'objet en octets. </td>
  </tr>
</table>



#### Pour télécharger des fichiers volumineux

1. Exécutez la commande suivante pour télécharger les segments. La régulation des téléchargements commence après que le dixième segment ait été téléchargé,
ce
qui accroît considérablement le temps de téléchargement.  

    ```
    curl -i -X PUT --data-binary @segment1 -H "X-Auth-Token: <jeton>" https://<url-stockage-objet>/<conteneur_un>/<segment>
    curl -i -X PUT --data-binary @segment2 -H "X-Auth-Token: <jeton>" https://<url-stockage-objet>/<conteneur_deux>/<segment>
    curl -i -X PUT --data-binary @segment3 -H "X-Auth-Token: <jeton>" https://<url-stockage-objet>/<conteneur_un>/<segment>
    ```
    {: pre}

2. Générez le manifeste :

    ```
    [
        {
            "path": "<nom_conteneur>/<segment>",
            "etag": "e0ed3b751eb8d4b2c648d2dd78576e36",
            "size_bytes": 801882690
        },
        {
            "path": "conteneur_deux/<segment>",
            "etag": "65a301e71c82cbd325a5efe5877e1a24",
            "size_bytes": 1048576
        },
        {
            "path": "<conteneur_un>/<segment>",
            "etag": "aea8b7462d527ad5ed0cfc22ea161062",
            "size_bytes": 138257
        }
    ]
    ```
    {: pre}

3. Téléchargez le fichier manifeste en modifiant la requête `multipart-manifest=put` d'après le nom du
manifeste.

    ```
    curl -i -X PUT --data-binary @object_name -H "X-Auth-Token: <jeton>" https://<url-stockage-objet>/conteneur_deux/<nom_objet>?multipart-manifest=put
    ```
    {: pre}

4. Téléchargez l'objet.

    ```
    curl -O -X GET -H "X-Auth-Token: <jeton>" https://<url-stockage-objet>/<conteneur_deux>/<nom_objet>
    ```
    {: pre}


#### Utilisation d'objets statiques volumineux

Vous pouvez gérer vos fichiers à l'aide des commandes suivantes.

**Remarque **: Pour ajouter des segments à l'objet ou en retirer, téléchargez un nouveau fichier
manifeste avec la nouvelle liste de segments. Le nom du manifeste peut rester le même.

* Pour télécharger le contenu du fichier manifeste, vous devez ajouter la requête `multipart-manifest=get` à votre commande. Le contenu que
vous recevez n'est pas identique au contenu que vous avez téléchargé.

    ```
    curl -O -X GET -H "X-Auth-Token:<jeton>" https://<url-stockage-objet>/<conteneur_deux>/<nom_objet>?multipart-manifest=get
    ```
    {: pre}

* Pour supprimer le manifeste, exécutez la commande suivante :

    ```
    curl -i -X DELETE -H "X-Auth-Token: <jeton>" https://<url-stockage-objet>/<conteneur_deux>/<nom_objet>
    ```
    {: pre}

* Pour supprimer le manifeste et tous les segments, ajoutez la requête `multipart-manifest=delete` après le nom du manifeste :

    ```
    curl -i -X DELETE -H "X-Auth-Token: <jeton>" https://<url-stockage-objet>/<conteneur_deux>/<nom_objet>?multipart-manifest=delete
    ```
    {: pre}
