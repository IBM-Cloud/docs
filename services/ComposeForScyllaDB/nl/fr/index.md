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

# Initiation à Compose for ScyllaDB
{: #getting-started-with-compose-for-scylladb}

ScyllaDB est un remplacement interne pour la base de données répartie Cassandra à colonnes larges. ScyllaDB est écrit en C++, plutôt qu'en Java Cassandra, pour une meilleure utilisation des ressources pouvant conduire à des performances dix fois meilleures dans les tests de performances. En plus du maintien de la compatibilité avec les fichiers de données et l'outil Cassandra, ScyllaDB ajoute des fonctionnalités de réglage automatique. {{site.data.keyword.composeForScyllaDB_full}} étend les fonctionnalités de ScyllaDB en les gérant à votre place, vous offrant un système de déploiement à dimensionnement automatique facile à utiliser qui fournit des fonctions de haute disponibilité et de redondance ainsi des sauvegardes automatisées.
{:shortdesc}

**Remarque: ** {{site.data.keyword.composeForScyllaDB_full}} ne donne pas l'accès à l'interface utilisateur Compose. Voir [Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support) pour plus de détails.

Exécutez les étapes décrites ci-dessous pour commencer à utiliser {{site.data.keyword.composeForScyllaDB}} :

1. [Créez une instance {{site.data.keyword.composeForScyllaDB}}](https://console.ng.bluemix.net/catalog/services/compose-for-scylladb/).

   Quand vous créez une instance du service, choisissez un nom pour votre service et un nom de données d'identification. Laissez le service non lié ; vous pourrez connecter une application à votre service ultérieurement en utilisant les données d'identification fournies lors de la mise à disposition du service. La section "Données d'identification disponibles" répertorie les différentes valeurs de données d'identification.

2. Connectez-vous au service {{site.data.keyword.composeForScyllaDB}}.

   Pour connecter une application à votre service, utilisez les
[données d'identification](./credentials.html) créées en même temps que
le service. 

   Téléchargez le modèle d'application
[compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) et suivez les instructions contenues dans le fichier Readme. Ensuite, cliquez sur **Afficher l'application** sur la page des détails d'application .

   Le modèle d'application montre comment utiliser Node.js pour établir une connexion au service {{site.data.keyword.composeForScyllaDB}}.
