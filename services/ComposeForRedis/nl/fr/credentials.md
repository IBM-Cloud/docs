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
Le modèle d'application [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs) montre comment utiliser Node.js pour établir une connexion au
service {{site.data.keyword.composeForRedis}} à l'aide des données
d'identification.

Nom de zone|Description
----------|-----------
`uri`|URI à utiliser pour la connexion au service et qui comprend le
schéma (redis:), le nom et le mot de passe de l'administrateur, le nom d'hôte du serveur
et le numéro de port auquel se connecter.
`uri_cli`|Ligne de commande `redis-cli` qui permet d'établir la connexion à l'instance de base de données.
`deployment_id`|Identificateur interne du service, créé dans Compose.
`db_type`|Type de base de données fourni par le service, en l'occurrence, `redis`.
`name`|Nom du déploiement de base de données.
{: caption="Tableau 1. Données d'identification Compose for Redis" caption-side="top"}
