---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Création d'une URL temporaire {: #create-temporary-url}

*Dernière mise à jour : 19 octobre 2016*
{: .last-updated}

Une URL temporaire est une URL longue et difficile à deviner qui peut être utilisée pour une période spécifiée pour télécharger des objets sans nécessiter plus d'authentification.
{: shortdesc}


1. Identifiez vos informations d'authentification en imprimant vos informations de compte avec la commande suivante :

    ```
    swift stat
    ```
    {: pre}
    
    **Remarque** : localisez la zone Compte et prenez note de la chaîne complète figurant après *Compte* et incluant `AUTH_`.
2. Définissez une clé secrète. Vous pouvez choisir la clé de votre choix, mais il est conseillé de choisir une chaîne longue, aléatoire et difficile à deviner. Pour définir la clé, exécutez la commande suivante :

    ```
    swift post -m "Temp-URL-Key:<key>"
    ```
    {: pre}
    
3. Vérifiez que `Temp-URL-Key` a été correctement définie en exécutant la commande suivante.

    ```
    swift stat
    ```
    {: pre}
    
4. Créez une URL temporaire en exécutant la commande suivante :

    ```
    swift tempurl GET <seconds> <path> <key>
    ```
    {: pre}
    
    Le tableau suivant présente les arguments de position utilisés par la commande Swift `tempurl`.
    <table>
      <tr>
        <th> Argument </th>
        <th> Description </th>
      </tr>
      <tr>
        <td> [method] </td>
        <td> GET pour permettre la réception par téléchargement. PUT pour permettre l'envoi par téléchargement. </td>
      </tr>
      <tr>
        <td> [seconds] </td>
        <td> Durée en secondes pendant laquelle l'URL temporaire sera disponible. </td>
      </tr>
      <tr>
        <td> [path] </td>
        <td> Chemin complet de l'objet,  exprimé sous la forme `/v1/<compte_auth>/<nom_conteneur>/<nom_objet>`. Pour plus d'informations, voir la [documentation sur l'URL {{site.data.keyword.objectstorageshort}}](/os_api.html#access-points). </td>
      </tr>
      <tr>
        <td> [key] </td>
        <td> Clé secrète que vous avez définie à l'étape 2. </td>
      </tr>
    </table>
    *Tableau 2 : arguments de position de tempurl*
5. (*Facultatif*) : Ajoutez l'URL retournée à votre nom de cluster pour obtenir une URL complète. Vous pouvez ensuite utiliser cette URL complète pour télécharger des objets avec tout client HTTP compatible comme cURL, wget ou Firefox.
