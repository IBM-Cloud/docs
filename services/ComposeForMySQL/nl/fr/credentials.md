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
Le modèle d'application [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) montre comment utiliser Node.js pour établir une connexion au service
{{site.data.keyword.composeForMySQL}} à l'aide des données d'identification.

Nom de zone|Description
----------|-----------
`db_type`|Type de base de données fourni par le service, `mysql`, dans ce cas.
`name`|Nom du déploiement de base de données.
`uri_cli`|Ligne de commande shell `mysql` qui permet d'établir la connexion à l'instance de base de données.
`ca_certificate_base64`|Certificat autosigné utilisé pour confirmer qu'une application se connecte au serveur approprié. Le certificat est codé en base64.
`deployment_id`|Identificateur interne du service, créé dans Compose.
`uri`|Identificateur URI qui est utilisé pour la connexion au service et qui comprend le schéma (`mysql:`), le nom et le mot de passe de l'administrateur, le nom d'hôte du serveur, le numéro de port auquel se connecter et le nom vhost.
{: caption="Tableau 1. Données d'identification Compose for MySQL" caption-side="top"}
