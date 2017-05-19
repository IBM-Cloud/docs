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

# Données d'identification disponibles
{: #available-credentials}

Pour connecter une application à votre service, utilisez les données d'identification créées en même temps que le service. 
Le modèle d'application [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) montre comment utiliser Node.js pour établir une connexion au service
{{site.data.keyword.composeForElasticsearch}} à l'aide des données
d'identification.

Nom de zone|Description
----------|-----------
`uri`|URI à utiliser pour établir la connexion au service. Comprend le schéma (`https:`), le nom et le mot de passe de l'administrateur, le nom d'hôte du serveur et le numéro de port auquel se connecter.
`uri_direct_1`|URI alternatif qui peut être utilisé lors de la connexion au service. Utilise le même format qu'`uri`.
`uri_health`|Commande `curl` qui demande l'état de santé du cluster au premier haproxy.
`uri_health_1`|Commande `curl` qui demande l'état de santé du cluster au second haproxy.
`ca_certificate_base64`|Certificat autosigné utilisé pour confirmer qu'une application se connecte au serveur approprié. Le certificat est codé en base64. Vous devez décoder la clé avant de l'utiliser, comme illustré dans le modèle d'application.
`deployment_id`|Identificateur interne du service, créé dans Compose.
`db_type`|Type de base de données fourni par le service, en l'occurrence, `elastic_search`.
`name`|Nom du déploiement de base de données.
{: caption="Tableau 1. Données d'identification Compose for Elasticsearch" caption-side="top"}

**Remarque :** deux portails `haproxy` permettent d'accéder au cluster Elasticsearch. Les zones `uri` et `uri_direct_1` peuvent toutes deux être utilisées pour établir la connexion au cluster. Dans vos applications, utilisez `uri` ou `uri_direct_1` pour gérer les réponses aux pannes de connexion.
