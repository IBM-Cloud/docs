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

# Initiation à Compose for ScyllaDB
{: #getting-started-with-compose-for-scylladb}

ScyllaDB est un remplacement interne pour la base de données répartie Cassandra à colonnes larges. ScyllaDB est écrit en C++, plutôt qu'en Java Cassandra, pour une meilleure utilisation des ressources pouvant conduire à des performances dix fois meilleures dans les tests de performances. En plus du maintien de la compatibilité avec les fichiers de données et l'outil Cassandra, ScyllaDB ajoute des fonctionnalités de réglage automatique. {{site.data.keyword.composeForScyllaDB_full}} étend les fonctionnalités de ScyllaDB en les gérant à votre place, vous offrant un système de déploiement à dimensionnement automatique facile à utiliser qui fournit des fonctions de haute disponibilité et de redondance ainsi des sauvegardes automatisées.
{:shortdesc}

**Remarque: ** {{site.data.keyword.composeForScyllaDB_full}} ne donne pas l'accès à l'interface utilisateur Compose. Voir [Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support) pour plus de détails.

Exécutez les étapes décrites ci-dessous pour commencer à utiliser {{site.data.keyword.composeForScyllaDB}} :

1. [Créez une instance {{site.data.keyword.composeForScyllaDB}}](https://console.ng.bluemix.net/catalog/services/compose-for-scylladb/).

   Quand vous créez une instance du service, choisissez un nom pour votre service et un nom de données d'identification. Laissez le service non lié ; vous pourrez connecter une application à votre service ultérieurement en utilisant les données d'identification fournies lors de la mise à disposition du service. La section "Données d'identification disponibles" répertorie les différentes valeurs de données d'identification.

2. Connectez-vous au service {{site.data.keyword.composeForScyllaDB}}.

   Pour connecter une application à votre service, utilisez les données d'identification créées en même temps que le service.

   Téléchargez l'exemple d'application [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) et suivez les instructions contenues dans le fichier Readme. Ensuite, cliquez sur **Afficher l'application** sur la page des détails d'application .

   L'exemple d'application montre comment utiliser Node.js pour établir une connexion au service {{site.data.keyword.composeForScyllaDB}}.


## Données d'identification disponibles

Nom de zone|Description
----------|-----------
`db_type`|Type de base de données fourni par le service, `scylla`, dans ce cas.
`uri_cli_1`|Ligne de commande shell `cqlsh` alternative qui permet d'établir la connexion à l'instance de base de données.
`maps`|Carte de connexion ScyllaDB qui fournit les informations requises par les différents pilotes pour associer les adresses IP internes aux noms DNS  externes d'une base de données ScyllaDB.
`name`|Nom du déploiement de base de données.
`uri_cli`|Ligne de commande shell `cqlsh` qui permet d'établir la connexion à l'instance de base de données.
`uri_direct_2`|Identificateur URI alternatif qui peut être utilisé pour se connecter au service. Utilise le même format que `uri`.
`uri_direct_1`|Identificateur URI alternatif qui peut être utilisé pour se connecter au service. Utilise le même format que `uri`.
`ca_certificate_base64`|Certificat autosigné utilisé pour confirmer qu'une application se connecte bien au serveur approprié. Le certificat est codé en base64.
`deployment_id`|Identificateur interne du service, créé dans Compose.
`uri_cli_2`|Ligne de commande shell `cqlsh` alternative qui permet d'établir la connexion à l'instance de base de données.
`uri`|Identificateur URI qui est utilisé pour la connexion au service et qui comprend le schéma (`scylla:`), le mot de passe, le nom d'hôte du serveur, le numéro de port auquel se connecter et le nom de la base de données.
{: caption="Table 1. {{site.data.keyword.composeForScyllaDB}} credentials" caption-side="top"}


# Liens connexes
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose Articles](https://www.compose.com/articles/){:new_window}

## Tutoriels et exemples
{: #samples}
* [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs){:new_window}

## Liens connexes
{: #general}
* [Aide sur Compose](https://help.compose.com/docs){:new_window}
