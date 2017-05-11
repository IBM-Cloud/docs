---

copyright:
  years: 2015, 2017
lastupdated: "2016-08-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Gestion des bundles
{: #globalizationpipeline_workingwithbundles}


Chaque bundle que vous créez contient les paires clé/valeur de votre fichier de ressources et le jeu complet de traductions qui a été généré.
{:shortdesc}

Les fichiers de ressources que vous téléchargez peuvent correspondre à n'importe lequel des formats suivants et leur contenu doit se présenter sous la forme de paires clé/valeur qui représentent les chaînes d'interface utilisateur de votre application.


* Type de fichier : *Fichiers de propriétés Java (.properties)*<br>
Exemple :
```js
logout=Logout 
back=Back 
examples=Menu 
home=Home 
web=Web 
enterprise=Enterprise 
extra=Resources 
about=About 
settings=Settings 
help=Help 
support=Support 
topics=Topics 
appExitMsg=Are you sure you want to quit the application?
```
* Type de fichier : *AMD I18N (.js)*<br>
Exemple :
```js
define({
    "root": {
       logout: "Logout",
       back: "Back",
       examples: "Menu",
       home: "Home",
       web: "Web",
       enterprise: "Enterprise",
       extra: "Resources",
       about: "About",
       settings: "Settings",
       help: "Help",
       support: "Support",
       topics: "Topics",
       appExitMsg: "Are you sure you want to quit the application?"
    }
});
``` 
* Type de fichier : *JSON (.json)*<br>
Exemple :
```js
{
  "logout": "Logout",
  "back": "Back",
  "examples": "Menu",
  "home": "Home",
  "web": "Web",
  "enterprise": "Enterprise",
  "extra": "Resources",
  "about": "About",
  "settings": "Settings",
  "help": "Help",
  "support": "Support",
  "topics": "Topics",
  "appExitMsg": "Are you sure you want to quit the application?"
}
``` 

De plus, un fichier de ressources doit également être conforme aux instructions suivantes :
* Chaque clé peut comporter 255 caractères maximum.
* Chaque valeur peut comporter 8191 caractères maximum.
* Chaque bundle peut contenir 500 paires clé/valeur maximum.


## Traduction d'un bundle
{: #globalizationpipeline_translatingabundle}

Seuls les fichiers de ressources téléchargés seront traduits. Vous pouvez télécharger un fichier de ressources lors de la [création d'un bundle](index.html#globalizationpipeline_creatingbundles) ou de la [modification avec des détails de bundle](bundles.html#globalizationpipeline_modifyingbundles).

Après avoir téléchargé un fichier de ressources, vous pouvez traduire son contenu dans n'importe laquelle des langues fournies par le moteur de traduction automatique par défaut. Vous pouvez éventuellement choisir un autre moteur de traduction automatique, comme indiqué dans la section [Configuration de la traduction automatique](managing_translations.html#globalizationpipeline_service_to_service). Le moteur par défaut prend en charge les langues cible suivantes :

<table>
<thead>
<tr>
<th>Langues cible</th>
</tr>
</thead>
<tbody>
<tr>
<td>Chinois (simplifié)</td>
</tr>
<tr>
<td>Chinois (traditionnel)</td>
</tr>
<tr>
<td>Français</td>
</tr>
<tr>
<td>Allemand</td>
</tr>
<tr>
<td>Italien</td>
</tr>
<tr>
<td>Japonais</td>
</tr>
<tr>
<td>Coréen</td>
</tr>
<tr>
<td>Portugais (Brésil)</td>
</tr>
<tr>
<td>Espagnol</td>
</tr>
</tbody>
</table>

**Remarque : ** le moteur de traduction automatique par défaut de {{site.data.keyword.GlobalizationPipeline_short}} ne fournit une prise en charge que pour l'anglais comme langue source. Toutefois, d'autres moteurs de traduction automatique disponibles pour configuration au sein de {{site.data.keyword.GlobalizationPipeline_short}} prennent en charge la traduction d'autres paires de langues, avec une langue source différente de l'anglais.

A mesure que vous créez des bundles, ils sont ajoutés à l'onglet **Bundles** et sont plus facilement accessibles. A partir de cet onglet, d'autres tâches peuvent être effectuées sur vos traductions.


## Sélection d'un bundle à gérer
{: #globalizationpipeline_selectingabundle}

1. Cliquez sur l'onglet **Bundles** pour afficher tous les bundles que vous avez créés.
2. Cliquez sur un **ID de bundle** dans la liste pour voir des détails supplémentaires sur ce bundle, ou cliquez sur l'icône d'**affichage des détails de bundle** ![Sélectionnez l'icône d'affichage des détails de bundle pour ouvrir un bundle et gérer ses traductions](images/viewProjectDetailIcon.png) dans la colonne Actions.

![Affichez tous les bundles disponibles à partir de l'onglet Bundles.](images/translationBundles.png)

Après avoir sélectionné un bundle à gérer, vous pouvez afficher le statut de ses traductions, ajouter ou retirer des langues, éditer les traductions ou appliquer des mises à jour au fichier de ressources.

Si vous n'avez plus besoin d'un bundle, vous pouvez le supprimer à partir de l'onglet **Bundles**. Toutes les traductions qui sont associées au bundle sont également supprimées.

## Modification des détails de bundle
{: #globalizationpipeline_modifyingbundles}

Lorsque vous ouvrez un bundle, vous pouvez afficher tous les détails le concernant. Toutes les langues cible contenues dans le bundle sont répertoriées, ainsi que le statut de traduction en cours pour chacune d'elles.

![La page des détails de bundle affiche des informations sur un bundle et ses traductions.](images/bundleDetails.png)

Le statut possible pour chaque langue contenue dans le bundle est In Progress, Failed ou Translated :

| Statut | Description |
|--------|-------------|
| In Progress | La traduction automatique est toujours en cours. |
| Failed | Une erreur s'est produite lors de la traduction du fichier de ressources dans la langue cible. |
| Translated | La traduction dans la langue cible est terminée. |

Vous pouvez mettre à jour le fichier de ressources que le bundle utilise, ajouter une langue cible à un bundle, supprimer une langue cible d'un bundle et télécharger les traductions générées pour une langue cible.

### Mise à jour du fichier de ressources utilisé par le bundle

1. En regard de la langue source, cliquez sur l'icône de **téléchargement de ressources** ![Sélectionnez cette icône pour télécharger un nouveau fichier de ressources](images/uploadIcon.png) dans la colonne Actions.
2. Cliquez sur **Browse** et sélectionnez le nouveau fichier de ressources à télécharger.
3. Sélectionnez le type de fichier de ressources que vous téléchargez :
 * Fichier de propriété Java
 * AMD I18N
 * JSON
4. Cliquez sur **Update** pour télécharger le nouveau fichier de ressources.

Les paires clé/valeur contenues dans le fichier de ressources nouveau ou mis à jour sont synchronisées avec les valeurs qui étaient déjà téléchargées. Seul le contenu nouveau ou modifié sera traduit.

### Ajout d'une langue cible à un bundle

1. Cliquez sur le bouton **Add Language**.
2. Toutes les langues cible disponibles sont affichées. Sélectionnez les langues à ajouter au bundle.

La traduction pour les langues sélectionnées va immédiatement commencer.

### Suppression d'une langue cible d'un bundle

Lorsque vous supprimez une langue cible d'un bundle, vous retirez du projet la langue cible et toutes les traductions qui lui sont associées. Dans la colonne Actions de la langue cible à retirer, cliquez sur l'icône de **retrait de cette langue cible** ![Sélectionnez l'icône de retrait de cette langue cible](images/trashIcon.png).

### Téléchargement des traductions générées pour une langue cible

{{site.data.keyword.GlobalizationPipeline_short}} vous offre la possibilité de procéder de différentes manières pour intégrer la traduction pour une langue cible dans votre application. Vous pouvez télécharger la traduction sous la forme d'un fichier de ressources et l'inclure dans votre génération d'application. Vous pouvez également faire référence à la traduction de manière dynamique à partir de {{site.data.keyword.GlobalizationPipeline_short}} en utilisant l'un des [SDK](https://github.com/IBM-Bluemix/gp-common) open source. 

<!-- For information on {{site.data.keyword.GlobalizationPipeline_full}} SDKs, see <link>. -->

Pour télécharger la traduction d'un fichier de ressources : 

1. Dans la colonne **Actions** de la langue source ou cible à télécharger, cliquez sur l'icône de **téléchargement des traductions** ![Sélectionnez l'icône de téléchargement pour télécharger les clés ou traductions source pour une langue cible](images/downloadIcon.png).
2. Sélectionnez un format de fichier.
3. Cliquez sur **Download**.
