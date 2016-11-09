---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Planification de la suppression d'un objet {: #schedule-object-deletion}
*Dernière mise à jour : 19 octobre 2016*
{: .last-updated}

Vous pouvez planifier la suppression de vos objets. Pour ce faire, utilisez l'un des en-têtes `X-Delete-At` ou `X-Delete-After`.
{: shortdesc}

L'en-tête `X-Delete-At` admet
un entier représentant la date et l'heure auxquelles supprimer l'objet. L'en-tête `X-Delete_After` admet
un entier représentant le nombre de secondes après lesquelles l'objet sera supprimé. Pour utiliser le client swift pour planifier une suppression d'objet, exécutez l'une des commandes ci-après, en choisissant celle qui correspond le mieux à vos besoins.

* Pour définir la suppression de l'objet à une date et heure spécifiques, exécutez la commande suivante :
    
    ```
    swift post -H "X-Delete-At:<période>" <nom_conteneur> <nom_objet>
    ```
    {: pre}
    
    Exemple :
    
    Pour que l'objet soit supprimé le 01/04/2016 à 08:00:00, exécutez la commande suivante :
    
    ```
    swift post -H "X-Delete-At:1459515600" <nom_conteneur> <nom_objet>
    ```
    {: screen}
* Pour que l'objet soit supprimé dans une heure, utilisez la commande suivante :
    
    ```
    swift post -H "X-Delete-After:<nombre_de_secondes" <nom_conteneur> <nom_objet>
    ```
    {: pre}
    
    Exemple :
    
    Pour que l'objet soit supprimé dans une heure, exécutez la commande suivante :
    
    ```
    swift post -H "X-Delete-After:3600" container object
    ```
    {: screen}
* Pour retirer la date et l'heure d'expiration de votre objet, utilisez la commande suivante :
    
    ```
    swift post -H "X-Remove-Delete-After:<nombre_de_secondes>" container object
    ```
    {: pre}

Pour utiliser des commandes cURL pour une suppression d'objet planifiée, vous pouvez exécuter l'une des commandes ci-après, en choisissant celle qui correspond le mieux à vos besoins. Les normes de définition des dates et heures sont les mêmes que celles du client Swift.

* Pour que l'objet soit supprimé le 01/04/2016 à 08:00:00, utilisez la commande suivante :
   
   ```
   cURL -X POST -H "X-Auth-Token: <jeton>" -H "X-Delete-At:<période>" https://<url-stockage-objet>/<nom_conteneur/<nom_objet>
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

**Remarque :** il se peut que la suppression réelle d'un objet ne survienne pas exactement à l'heure indiquée. Cependant,
l'objet arrive effectivement à expiration à l'heure spécifiée, ce qui signifie qu'il devient inaccessible. La suppression réelle a lieu lorsque le démon
swift-object-expirer configuré dans votre cluster s'exécute.
