---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Utilisation de fichiers volumineux{: #large-files}
*Dernière mise à jour : 19 octobre 2016*
{: .last-updated}

Le téléchargement des objets est limité à une taille maximale de 5 Go par téléchargement. Vous pouvez toutefois télécharger des objets dont la taille dépasse les 5 Go si vous les segmenter en objets plus petits. Une fois que les objets segmentés ont été téléchargés, un fichier manifeste est aussi nécessaire pour concaténer les segments dans l'objet d'origine. Vous disposez de deux façons de faire, selon qu'il s'agissent d'objets DLO (Dynamic Large Object) ou d'objets SLO (Static Large Object).
{: shortdesc}

### Objets DLO (Dynamic Large Object) : {: #dynamic}

Il y a deux manières de gérer les objets DLO :
  * Laisser le client Swift gérer tout automatiquement
  * Utiliser l'API Swift pour le faire vous-même

#### Utilisation du client Swift pour gérer les objets DLO

Le client Swift utilise le paramètre `-segment-size` pour décomposer votre objet en élément plus petits. Le client crée un nouveau conteneur, avec le nom du conteneur dans lequel vous voulez télécharger des fichiers et ajoute un suffixe incluant le numéro de segment (`<nom_conteneur>_segments`). Les segments sont téléchargés en parallèle. Une fois que tous les segments ont été envoyés par téléchargement, leur réception par téléchargement s'effectue sous la forme d'un objet concaténé dans un fichier manifeste avec le nom de fichier d'origine.

1. Après que vous vous soyez connecté à {{site.data.keyword.Bluemix_notm}} et que vous êtes prêt à procéder au téléchargement, exécutez la commande suivante pour segmenter votre fichier.

    ```
    swift upload <nom_conteneur> <nom_fichier> --segment-size <taille_en_octets>
    ```
    {: pre}

#### Utilisation de l'API Swift pour gérer les objets DLO

Vous pouvez segmenter vous-même les objets pour qu'ils fassent 5 Go ou moins puis les télécharger via l'API Swift. Lors de l'envoi par téléchargement, il est important d'envoyer d'abord tous les segments avant d'envoyer le manifeste. Si lors de l'exécution des téléchargements (envoi et réception par téléchargement), la réception de l'objet s'effectue avant que l'envoi de tous les segments ne soit terminé, cet objet risque d'être incohérent. Vous pouvez télécharger des fichiers volumineux en procédant comme suit.

1. Triez les segments par nom dans l'ordre dans lequel ils doivent être concaténés pour former l'objet d'origine.
2. Téléchargez vos segments dans un conteneur qui est séparé du conteneur qui renferme le fichier manifeste. La régulation des téléchargements, qui démarre une fois traité le dixième segment, augmente considérablement le temps de téléchargement. Pour cette raison, la taille de segment recommandée ne doit pas être inférieure à la taille du fichier divisée par 10.

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
    
    **Remarque** : le fichier manifeste doit être vide. Si ce n'est pas le cas, le contenu du fichier sera considéré comme l'un des segments et échouera dans l'ordre de concaténation qui est dicté par les noms triés.
4. Téléchargez l'objet. Vous recevrez la totalité de l'objet en tant que résultat. Vous pouvez ajouter ou retirer des segments sans avoir à mettre à jour le fichier manifeste. Les segments dont le préfixe est correct seront conservés dans l'objet. La suppression du manifeste ne supprimera pas les segments.

    ```
    curl -i -O -H "X-Auth-Token: <jeton>" https://<url-stockage-objet>/<nom_conteneur_manifeste>/<nom_objet>
    ```
    {: pre}


### Objets SLO (Static Large Object) {: #static}

Les objets SLO utilisent eux aussi des segments et un fichier manifeste mais permettent un plus grand contrôle. Avec SLO, les segments n'ont pas besoin de se trouver dans le même conteneur ; ils peuvent être placés dans le conteneur de votre choix et porter le nom que vous définissez. Les segments doivent toutefois faire au moins 1 Mo. Il ne vous est pas demandé de définir un en-tête pour le fichier manifeste, même si l'en-tête “X-Static-Large-Object” est automatiquement ajouté et paramétré sur true une fois qu'un manifeste correct a été téléchargé.
{: shortdesc}

Le fichier manifeste est un document JSON qui fournit les détails des segments et doit être téléchargé après téléchargement de tous les segments. Les données fournies pour chaque segment du manifeste sont comparées aux métadonnées des segments réels. Si un élément ne correspond pas, le manifeste n'est pas téléchargé.

<table>
  <tr>
    <th> Attribut </th>
    <th> Description </th>
  </tr>
  <tr>
    <td> path </td>
    <td> Emplacement et nom du segment. Spécifié sous la forme nom_conteneur/nom_objet. </td>
  </tr>
  <tr>
    <td> etag </td>
    <td> Fourni par la demande PUT quand l'objet est téléchargé. Vous pouvez aussi le trouver en effectuant une action HEAD sur l'objet. </td>
  </tr>
  <tr>
    <td> size_bytes </td>
    <td> Taille de l'objet en octets. </td>
  </tr>
</table>

*Tableau 1 : attributs JSON dans le fichier manifeste dans l'ordre de concaténation*

Vous pouvez télécharger des fichiers volumineux en procédant comme suit :

1. Exécutez la commande suivante pour télécharger les segments. La régulation des téléchargements, qui démarre une fois traité le dixième segment, augmente considérablement le temps de téléchargement. Pour cette raison, la taille de segment recommandée ne doit pas être inférieure à la taille du fichier divisée par 10.

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
    
3. Téléchargez le manifeste. Pour ce faire, vous devez ajouter la requête `multipart-manifest=put` au nom du manifeste en exécutant la commande suivante :

    ```
    curl -i -X PUT --data-binary @object_name -H "X-Auth-Token: <jeton>" https://<url-stockage-objet>/conteneur_deux/<nom_objet>?multipart-manifest=put
    ```
    {: pre}
    
4. Téléchargez l'objet. 

    ```
    curl -O -X GET -H "X-Auth-Token: <jeton>" https://<url-stockage-objet>/<conteneur_deux>/<nom_objet>
    ```
    {: pre}
    
Quelques commandes qui pourront vous être utiles lors de l'utilisation des objets SLO sont présentées ci-dessous.

* Pour télécharger le contenu du fichier manifeste, vous devez ajouter la requête `multipart-manifest=get` à votre commande. Le contenu que vous recevez ne sera pas identique au contenu que vous avez envoyé par téléchargement.

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

**Remarque** : pour ajouter des segments à l'objet ou pour en retirer, vous devez télécharger un nouveau fichier manifeste avec une nouvelle liste de segments. Le nom du manifeste peut rester le même.
