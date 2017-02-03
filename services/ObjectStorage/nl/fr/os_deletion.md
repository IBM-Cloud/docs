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


# Suppression d'objets

Quand ils ne vous sont plus nécessaires, vous pouvez supprimer les objets et les conteneurs depuis votre instance de stockage. Vous pouvez procéder à une suppression manuelle ou [planifier le moment](/docs/services/ObjectStorage/os_deletion.html#schedule-object-deletion) où vous voulez que les objets expirent.
{: shortdesc}

**Remarque** : si vous supprimez votre conteneur, tous les objets qui sont stockés dans ce conteneur sont supprimés.


## Suppression d'objets et de conteneurs via l'interface utilisateur {: #deleting-ui}

1. Dans votre tableau de bord d'instance de service, sélectionnez le conteneur avec le fichier dont vous n'avez plus besoin.
2. Sélectionnez la commande de suppression du fichier dans le menu déroulant **Actions**.
3. Si vous n'avez plus besoin d'utiliser votre conteneur, sélectionnez **Supprimer le conteneur** dans le menu déroulant **Actions**.



## Suppression d'objets et de conteneurs via l'interface de ligne de commande {: #deleting-cli}

1.  Si vous n'êtes pas connecté à {{site.data.keyword.Bluemix_notm}}, connectez-vous à l'organisation et l'espace contenant votre instance d'{{site.data.keyword.objectstorageshort}}.
  ```
  cf login -a api.ng.bluemix.net -u <ID_utilisateur> -p <mot_de_passe> -o <organisation> -s <space>
  ```
  {: pre}

2. Facultatif : Vérifiez que vous disposez d'une sauvegarde de vos objets avant de supprimer vos fichiers et conteneurs.

3. Exécutez la commande suivante pour supprimer un fichier :
  ```
  swift delete <nom_conteneur> <nom_fichier>
  ```
  {: pre}

4. Pour supprimer votre conteneur, exécutez la commande suivante :
  ```
  swift delete <nom_conteneur>
  ```
  {: pre}



## Planification de la suppression d'un objet {: #schedule-object-deletion}


Vous pouvez planifier la suppression de vos objets à l'aide de l'en-tête
`X-Delete-At` ou `X-Delete-After`.
{: shortdesc}

L'en-tête `X-Delete-At` reçoit un entier qui représente la date et heure à laquelle supprimer l'objet. L'en-tête
`X-Delete_After` reçoit un entier qui représente le nombre de secondes après lequel l'objet est supprimé.

**Remarque :** il se peut que la suppression réelle d'un objet ne survienne pas exactement à l'heure indiquée. Cependant,
l'objet arrive effectivement à expiration à l'heure spécifiée, Des lors, l'objet n'est plus accessible. La suppression effective a lieu
lors de la prochaine exécution du démon swift-object-expirer configurée dans votre cluster Swift.

#### Pour utiliser les commandes Swift :

* Pour définir la suppression de l'objet à une date et heure spécifiques, exécutez la commande suivante :

    ```
    swift post -H "X-Delete-At:<période>" <nom_conteneur> <nom_objet>
    ```
    {: pre}

    Exemple : pour que l'objet soit supprimé le 01/04/2016 à 08:00:00, exécutez la commande suivante :

    ```
    swift post -H "X-Delete-At:1459515600" container1 file7
    ```
    {: screen}

* Pour que l'objet soit supprimé après une durée spécifique, utilisez la commande suivante :

    ```
    swift post -H "X-Delete-After:<nombre_de_secondes>" <nom_conteneur> <nom_objet>
    ```
    {: pre}

    Exemple : pour que l'objet soit supprimé dans une heure, exécutez la commande suivante :

    ```
    swift post -H "X-Delete-After:3600" container1 file7
    ```
    {: screen}

* Pour retirer la date et l'heure d'expiration de votre objet, utilisez la commande suivante :

    ```
    swift post -H "X-Remove-Delete-After:<nombre_de_secondes>" <nom_conteneur> <nom_objet>
    ```
    {: pre}



#### Pour utiliser les commandes cURL :

* Pour que l'objet soit supprimé le 01/04/2016 à 08:00:00, utilisez la commande suivante :

    ```
    cURL -X POST -H "X-Auth-Token: <jeton>" -H "X-Delete-At:<période>" https://<url-stockage-objet>/<nom_conteneur>/<nom_objet>
    ```
    {: pre}

* Pour que l'objet soit supprimé dans une heure, utilisez la commande suivante :

    ```
    cURL -X POST -H "X-Auth-Token: <jeton>" -H "X-Delete-After:<nombre_de_secondes>" https://<url-stockage-objet>/<nom_conteneur>/<nom_objet>
    ```
    {: pre}

* Pour vérifier si l'objet comporte l'en-tête, utilisez la commande suivante :

    ```
    cURL -I -H "X-Auth-Token: <jeton>" https://<url-stockage-objet>/<nom_conteneur>/<nom_objet>
    ```
    {: pre}

* Pour retirer la date et l'heure d'expiration, utilisez la commande suivante :

    ```
    cURL -X POST -H "X-Auth-Token: <jeton>" -H "X-Remove-Delete-At:<période>" https://<url-stockage-objet>/<nom_conteneur>/<nom_objet>
    ```
    {: pre}
