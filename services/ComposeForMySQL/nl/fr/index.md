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

# Initiation à Compose for MySQL
{: #getting-started-with-compose-for-mysql}

Avec un vaste sous-ensemble ANSI SQL 99 et un large ensemble de ses propres extensions, dont un document JSON, une recherche en texte intégral et des vues qu'il est possible de mettre à jour, MySQL offre une riche palette de fonctions à laquelle les développeurs peuvent faire appel dans leurs applications. Les administrateurs bénéficient aussi d'une grande sélection d'outils de gestion de base de données compatibles avec MySQL. Par le biais d'{{site.data.keyword.composeForMySQL_full}}, MySQL étend ses propres fonctionnalités en les gérant à votre place, vous offrant un système de déploiement à dimensionnement automatique facile à utiliser qui fournit des fonctions de haute disponibilité et de redondance et des sauvegardes automatisées.
{:shortdesc}

**Remarque: ** {{site.data.keyword.composeForMySQL_full}} ne donne pas l'accès à l'interface utilisateur Compose. Voir [Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support) pour plus de détails.

Exécutez les étapes décrites ci-dessous pour commencer à utiliser {{site.data.keyword.composeForMySQL}} :

1. [Créez une instance {{site.data.keyword.composeForMySQL}}](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/).

   Quand vous créez une instance du service, choisissez un nom pour votre service et un nom de données d'identification. Laissez le service non lié ; vous pourrez connecter une application à votre service ultérieurement en utilisant les données d'identification fournies lors de la mise à disposition du service.  La section "Données d'identification disponibles" répertorie les différentes valeurs de données d'identification.

2. Connectez-vous au service {{site.data.keyword.composeForMySQL}}.

  Pour connecter une application à votre service, utilisez les
[données d'identification](./credentials.html) créées en même temps que
le service. 

  Téléchargez le modèle d'application [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) et suivez les instructions contenues dans le fichier Readme. Ensuite, cliquez sur **Afficher l'application** sur la page des détails d'application .

  Le modèle d'application montre comment utiliser Node.js pour établir une connexion au service {{site.data.keyword.composeForMySQL}}.
