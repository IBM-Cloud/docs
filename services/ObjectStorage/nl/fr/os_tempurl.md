---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Création d'une URL temporaire {: #create-temporary-url}


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
    <td> Durée pendant laquelle l'URL temporaire sera disponible, exprimée en secondes. </td>
  </tr>
  <tr>
    <td> [path] </td>
    <td> Chemin complet de l'objet, exprimé sous la forme <code>/v1/<i>compte_auth</i>/<i>nom_conteneur</i>/<i>nom_objet</i>.</code> Pour plus d'informations, voir la <a href="https://console.bluemix.net/docs/services/ObjectStorage/os_api.html#access-points">documentation relative à votre URL {{site.data.keyword.objectstorageshort}}.</a>. </td>
  </tr>
  <tr>
    <td> [key] </td>
    <td> Clé secrète que vous avez définie à l'étape 2. </td>
  </tr>
</table>

Tableau 2 : arguments de l'URL temporaire

5. Facultatif - ajoutez l'URL retournée à votre nom de cluster pour obtenir une URL complète. Vous pouvez ensuite utiliser cette URL complète pour télécharger des objets avec tout client HTTP compatible comme cURL, wget ou Firefox.
