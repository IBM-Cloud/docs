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


# Création d'une URL temporaire {: #create-temporary-url}

Une URL temporaire est une URL longue et difficile à deviner, qui peut être utilisée pendant une période déterminée
afin de télécharger des objets sans requérir d'authentification supplémentaire ou d'accorder un accès complet au compte de stockage.
{: shortdesc}


1. Identifiez vos informations d'authentification en imprimant vos informations de compte avec la commande suivante :

  ```
  swift stat
  ```
  {: pre}
  **Remarque** : notez la chaîne complète qui suit *Account*, incluant `AUTH_`.

2. Définissez une clé secrète. Choisissez une chaîne longue, aléatoire et difficile à deviner. Pour définir la clé, exécutez la commande suivante :

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
  <caption> Tableau 1. Arguments de position d'URL temporaire </caption>
    <tr>
      <th> Argument </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i> méthode </i> </td>
      <td> GET pour permettre la réception par téléchargement. PUT pour permettre l'envoi par téléchargement. </td>
    </tr>
    <tr>
      <td> <i> secondes </i> </td>
      <td> Durée pendant laquelle l'URL temporaire est disponible, exprimée en secondes. </td>
    </tr>
    <tr>
      <td> <i> chemin </i> </td>
      <td> Chemin complet de l'objet, exprimé sous la forme <code>/v1/<i>compte_auth</i>/<i>nom_conteneur</i>/<i>nom_objet</i></code>.</td>
    </tr>
    <tr>
      <td> <i> clé </i> </td>
      <td> Clé secrète que vous avez définie à l'étape 2. </td>
    </tr>
  </table>

5. Facultatif - ajoutez l'URL retournée à votre nom de cluster pour obtenir une URL complète. Vous pouvez ensuite utiliser cette URL complète pour télécharger des objets avec tout client HTTP compatible comme cURL, wget ou Firefox.
