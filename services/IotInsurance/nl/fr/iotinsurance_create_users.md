---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Création d'utilisateurs et d'associations de bouclier
{: #gettingstartedtemplate}
Dernière mise à jour : 15 septembre 2016
{: .last-updated}

Une fois que vous avez créé le service {{site.data.keyword.iotinsurance_short}} et déployé les applications et les services de support
requis, vous pouvez tester le service en créant un utilisateur autorisé et une association de bouclier.
{:shortdesc}

**Configuration requise :** avant de commencer, assurez-vous de disposer des éléments requis suivants :

- [Node.js](https://nodejs.org/en/) installé sur votre ordinateur.  
- Un environnement d'exécution compatible avec Node.js tel qu'Eclipse.
- Le logiciel Git et l'accès au [référentiel de code source GitHub pour les exemples d'API](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).   Vous
pouvez aussi télécharger l'[archive avec les fichiers de code source](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip).
- Le code source préparé.  
  Pour préparer le code source, procédez comme suit :
  1. Clonez ou téléchargez le [référentiel de code source GitHub](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs) sur votre
ordinateur.
  2. Installez les éléments open source requis du projet en utilisant l'invite de commande pour accéder au dossier contenant les fichiers de code
source clonés et en exécutant la commande `npm install`.

Créez un utilisateur dont vous pouvez vous servir pour tester les fonctions du tableau de bord et du modèle d'application mobile.

1. Créez un utilisateur dans le système {{site.data.keyword.iotinsurance_short}}.
  1. Editez le fichier createUser.js pour remplacer les valeurs figurant dans la variable **user** par des informations
utilisateur uniques.
  2. Sauvegardez le fichier.
  3. Exécutez `node createUser.js`. L'exécution du processus prend quelques minutes.
  4. Prenez note du nom d'utilisateur ; il vous sera demandé à l'étape suivante.
2. Créez une association de bouclier pour l'utilisateur.
  1. Editez le fichier createUserShieldAssociation.js pour ajouter le nom d'utilisateur créé à l'étape précédente dans la variable
**username**.
  2. Sauvegardez le fichier.
  3. Exécutez `node createUserShieldAssociation.js`. Pour plus d'informations sur les boucliers, voir
[Composants](iotinsurance_overview.html#components}).
3. (Facultatif) Le moteur d'analyse est mis à jour automatiquement ; toutefois, si les données affichées ne sont pas correctes, vous pouvez
actualiser le moteur d'analyse en exécutant `node updateAnalyticsEngine.js`.
4. (Facultatif) Simulez un événement de risque pour l'utilisateur.
  1. Editez le fichier simulateHazard.js pour ajouter le nom d'utilisateur mentionné dans les étapes précédentes dans la
variable **usr**.
  2. Sauvegardez le fichier.
  3. Exécutez `node simulateHazard.js`.
5. (Facultatif) Créez un ensemble de données d'historique simulées en exécutant `node
createHistoricalData.js`.


# Liens connexes
{: #rellinks}

## Référence d'API
{: #api}
* [Exemples d'API {{site.data.keyword.iotinsurance_short}}](https://iot4i-docs-api.mybluemix.net/dist/){:new_window}

## Liens connexes
{: #general}
* [Forum
de support des développeurs](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Forum de support stackoverflow](http://stackoverflow.com/questions/tagged/ibm-bluemix)
