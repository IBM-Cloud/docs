---

copyright:
  years: 2016,2017
lastupdated: "2017-04-27"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Initiation à Compose for Elasticsearch
{: #getting-started-with-compose-for-elasticsearch}

{{site.data.keyword.composeForElasticsearch_full}} allie la puissance d'un moteur de recherche en texte intégral à la puissance d'indexation d'une base de données de documents JSON. Combinées, ces deux fonctions constituent un outil puissant dédié aux analyses de données enrichies sur d'importantes quantités de données. Elasticsearch vous permet de définir des scores d'exactitude pour vos recherches, et ainsi, de parcourir votre fichier à la recherche de concordances parfaites et de concordances approximatives que vous pourriez manquer.
{:shortdesc}

**Remarque :** les instances de service Compose qui ont été mises à disposition avant le 14 septembre 2016 et qui sont toujours actives peuvent encore être utilisées et sont directement accessibles sur le site [https://www.compose.com/](https://www.compose.com). Les instances de service Compose mises à disposition depuis cette date sont directement accessibles et utilisables dans votre compte Bluemix.

Exécutez les étapes décrites ci-dessous pour commencer à utiliser {{site.data.keyword.composeForElasticsearch}} :

1. [Créez une instance {{site.data.keyword.composeForElasticsearch}}](https://console.ng.bluemix.net/catalog/services/compose-for-elasticsearch/).

  Lorsque vous créez une instance du service, prenez soin de sélectionner un nom pour votre service et un nom de données d'identification. Laissez le service non lié ; vous pourrez connecter une application à votre service ultérieurement en utilisant les données d'identification fournies lors de la mise à disposition du service. La section *Données d'identification disponibles* répertorie les différentes valeurs de données d'identification.

2. Connectez-vous au service {{site.data.keyword.composeForElasticsearch}}.

  Pour connecter une application à votre service, utilisez les
[données d'identification](./credentials.html) créées en même temps que
le service. Le modèle d'application montre comment utiliser Node.js pour établir une connexion au service {{site.data.keyword.composeForElasticsearch}}.

  Téléchargez le modèle d'application [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) et suivez les instructions contenues dans le fichier Readme. Ensuite, cliquez sur **Afficher l'application** sur la page des détails d'application pour afficher le contenu de l'index *Exemples*.
