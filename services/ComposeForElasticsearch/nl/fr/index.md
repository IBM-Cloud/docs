---

copyright:
  years: 2016
lastupdated: "2016-12-09"
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

**Remarque :** Les instances de service Compose qui ont été mises à disposition avant le 14 septembre 2016 et qui sont toujours actives peuvent encore être utilisées et sont directement accessibles sur le site [https://www.compose.com/](https://www.compose.com). Les instances de service Compose mises à disposition depuis cette date sont directement accessibles et utilisables dans votre compte Bluemix.

Exécutez les étapes décrites ci-dessous pour commencer à utiliser {{site.data.keyword.composeForElasticsearch}} :

1. [Créez une instance {{site.data.keyword.composeForElasticsearch}}](https://console.ng.bluemix.net/catalog/services/compose-for-elasticsearch/).

  Lorsque vous créez une instance du service, prenez soin de sélectionner un nom pour votre service et un nom de données d'identification. Laissez le service non lié ; vous pourrez connecter une application à votre service ultérieurement en utilisant les données d'identification fournies lors de la mise à disposition du service. La section *Données d'identification disponibles* répertorie les différentes valeurs de données d'identification.

2. Connectez-vous au service {{site.data.keyword.composeForElasticsearch}}.

  Pour connecter une application à votre service, utilisez les données d'identification créées en même temps que le service. L'exemple d'application montre comment utiliser Node.js pour établir une connexion au service {{site.data.keyword.composeForElasticsearch}}.

  Téléchargez l'exemple d'application [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) et suivez les instructions contenues dans le fichier Readme. Ensuite, cliquez sur **Afficher l'application** sur la page des détails d'application pour afficher le contenu de l'index *Exemples*.

## Données d'identification disponibles

Nom de zone|Description
----------|-----------
`uri`|URI à utiliser pour établir la connexion au service. Comprend le schéma (`https:`), le nom d'utilisateur et le mot de passe administrateur, le nom d'hôte du serveur et le numéro de port auquel se connecter.
`uri_direct_1`|URI alternatif qui peut être utilisé lors de la connexion au service. Utilise le même format que `uri`.
`uri_health`|Commande `curl` qui demande l'état de santé du cluster au premier haproxy.
`uri_health_1`|Commande `curl` qui demande l'état de santé du cluster au second haproxy.
`ca_certificate_base64`|Certificat autosigné utilisé pour confirmer qu'une application se connecte bien au serveur approprié. Le certificat est codé en base64. Vous devez décoder la clé avant de l'utiliser, comme illustré dans l'exemple d'application.
`deployment_id`|Identificateur interne du service, créé dans Compose.
`db_type`|Type de base de données fourni par le service, en l'occurrence, `elastic_search`.
`name`|Nom du déploiement de base de données.
{: caption="Table 1. {{site.data.keyword.composeForElasticsearch}} credentials" caption-side="top"}

**Remarque :** Deux portails `haproxy` permettent d'accéder au cluster Elasticsearch. Les zones `uri` et `uri_direct_1` peuvent toutes deux être utilisées pour établir la connexion au cluster. Dans vos applications, utilisez `uri` ou `uri_direct_1` pour gérer les réponses aux pannes de connexion.

# Liens connexes
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose Articles](https://www.compose.com/articles/){:new_window}

## Tutoriels et exemples
{: #samples}
* [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs){:new_window}

## Liens connexes
{: #general}
* [Aide sur Compose](https://help.compose.com/docs){:new_window}
