---

copyright:
  years: 2015, 2017
lastupdated: "2016-09-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Initiation à {{site.data.keyword.GlobalizationPipeline_short}}
{: #globalizationpipeline}


{{site.data.keyword.GlobalizationPipeline_full}} est un service qui fournit des fonctions de traduction et d'édition automatiques permettant de traduire rapidement des interfaces utilisateur Web ou mobiles. Grâce à son tableau de bord, son API RESTful et son intégration à la pipeline de distribution de votre application, vous pouvez effectuer une mise en production auprès de clients globaux sans avoir à régénérer ou redéployer votre application.
{:shortdesc}

Vous pouvez utiliser le service {{site.data.keyword.GlobalizationPipeline_short}} avec n'importe quelle application figurant dans {{site.data.keyword.Bluemix}} ou de manière non liée, sans rien d'autre. Vous pouvez créer, gérer et réviser des traductions rapidement, avec un minimum d'effort et sans avoir à quitter votre environnement DevOps.

Depuis l'interface {{site.data.keyword.GlobalizationPipeline_short}}, vous pouvez traduire rapidement vos applications {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations sur la traduction de vos applications à l'aide de l'API RESTful, voir [API Reference](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}. 


## Création d'un bundle
{: #globalizationpipeline_creatingbundles}

Le service {{site.data.keyword.GlobalizationPipeline_short}} vous permet de créer des bundles, qui incluent les fichiers de ressources des applications que vous allez traduire. Les fichiers de ressources peuvent être des fichiers de propriétés Java, des fichiers AMD I18N ou des fichiers JSON et leur contenu doit se présenter sous la forme de paires clé/valeur qui représentent les chaînes d'interface utilisateur de votre application.  Pour obtenir plus d'informations et des exemples des types de fichiers pris en charge, voir [Utilisation de bundles](./bundles.html){: new_window}.

Pour créer un bundle, procédez comme suit :

<ol>
<li>Sur l'onglet <strong>Overview</strong>, cliquez sur <strong>New Bundle</strong>.</li>

<li>Entrez des informations sur votre bundle :</li>
<table>
<thead>
<tr>
<th>Champ</th>
<th>Obligatoire</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Bundle ID</strong></td>
<td>Oui</td>
<td>Nom unique permettant d'identifier le bundle.</td>
</tr>
<tr>
<td><strong>Source language</strong></td>
<td>Oui</td>
<td>Langue d'origine du fichier source.</td>
</tr>
<tr>
<td><strong>Resource File</strong></td>
<td>Non</td>
<td><a href=https://new-console.ng.bluemix.net/docs/services/GlobalizationPipeline/bundles.html>Fichier de ressources</a> à traduire. La taille de fichier maximale est limitée à 2 Mo. Les fichiers de ressources spécifiés seront téléchargés.</td>
</tr>
<tr>
<td><strong>File format</strong></td>
<td>Non</td>
<td>Type de fichier téléchargé.</td>
</tr>
<tr>
<td><strong>Target language</strong></td>
<td>Non</td>
<td>Langue dans laquelle vous souhaitez effectuer la traduction.</td>
</tr>
</tbody>
</table>

<p><strong>Remarque :</strong> Pour modifier le service de langue qui fournit la traduction automatique pour vos bundles, cliquez sur l'onglet <a href=https://new-console.ng.bluemix.net/docs/services/GlobalizationPipeline/managing_translations.html#globalizationpipeline_service_to_service>MT Configuration</a> pour afficher les autres moteurs de traduction automatique pris en charge.</p>

<li>Cliquez sur <strong>Sauvegarder</strong></li></ol>


Une fois le bundle créé, le fichier de ressources téléchargé est traduit dans toutes les langues cible que vous avez spécifiées. Le nouveau bundle est ajouté à l'onglet Bundles à partir duquel vous pouvez effectuer les actions suivantes :

* Ajouter ou retirer des langues
* Editer les traductions générées
* Mettre à jour le fichier source qui est utilisé dans le bundle et régénérer les traductions

## Importation de bundles traduits
{: #globalizationpipeline_importtranslatedbundlesintoservice}

Sinon, si vous disposez déjà de fichiers de ressources traduits, vous pouvez les importer dans un nouveau bundle. Pour plus d'informations, voir [Java Client Tools for {{site.data.keyword.GlobalizationPipeline_short}}](https://github.com/IBM-Bluemix/gp-java-tools).

**Remarque :** Si le fichier source d'origine est mis à jour, les clés et valeurs définies dans le fichier sont synchronisées avec la version la plus récente du fichier source de sorte que seules les clés et valeurs modifiées soient traduites.

## Estimation de l'utilisation des données {{site.data.keyword.GlobalizationPipeline_short}}
{: #globalizationpipeline_documentpricing}

{{site.data.keyword.GlobalizationPipeline_short}} stocke vos traductions dans une base de données de back end. Pour estimer la taille des données actives, vous pouvez vous référer à la formule d'estimation du stockage de données suivante :

`<Taille du stockage des données de ressource attendue en Mo> ˜= 0.0005 * < nombre de paires clé/valeur dans la ressource source> * <nombre de langues, y compris la langue source>`

En fonction de la formule, la taille d'un bundle typique est `longueur de clé + longueur de valeur en UTF-8 = ˜40 octets)`.

Par exemple, si vous disposez des 100 paires clé/valeur et que vous les traduisez dans 9 langues, la taille de stockage estimée est : 0,0005 100 (9+1) = 0,5 Mo. La taille réelle peut être différente selon la taille clé/valeur réelle et les métadonnées stockées avec la traduction.

Utilisez la [calculatrice de prix](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet&orgGuid=127a45f4-4461-4d5b-a26b-6dc2fdd1a3a2&spaceGuid=208fb1ff-413b-4fd9-9615-e8226062d0f3) de Bluemix pour déterminer quels seront vos coûts de service mensuels.


# Liens connexes
{: #rellinks}
## Tutoriels et exemples
{: #samples}

* [Exemple Node.js](https://github.com/IBM-Bluemix/gp-nodejs-sample){: new_window}
* [Exemple Ruby](https://github.com/IBM-Bluemix/gp-ruby-sample){: new_window}

## SDK
{: #sdk}

* [Client Java](https://github.com/IBM-Bluemix/gp-java-client){: new_window}
* [Outils Java](https://github.com/IBM-Bluemix/gp-java-tools){: new_window}
* [Client JavaScript](https://github.com/IBM-Bluemix/gp-js-client){: new_window}
* [Client AngularJS](https://github.com/IBM-Bluemix/gp-angular-client){: new_window}
* [Client Ruby](https://github.com/IBM-Bluemix/gp-ruby-client){: new_window}
* [Client Python](https://github.com/IBM-Bluemix/gp-python-client){: new_window}

## Référence d'API
{: #api}

* [API RESTful IBM Globalization Pipeline](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}

## Liens connexes
{: #general}

* [Intégrer Globalization Pipeline à Delivery Pipeline](https://hub.jazz.net/docs/deploy_ext/#globalize){: new_window}
* [Fiche des prix IBM Bluemix](https://www.ng.bluemix.net/#/pricing){: new_window}
* [Prérequis IBM Bluemix](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
