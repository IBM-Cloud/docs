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

# Initiation à Compose for RethinkDB
{: #getting-started-with-compose-for-rethinkdb}

{{site.data.keyword.composeForRethinkDB}} fournit une base de données répartie basée sur un document JSON avec une console d'administration et d'exploration. RethinkDB utilise le langage d'interrogation ReQL, construit autour d'un chaînage de fonctions et disponible dans des bibliothèques client pour Java, JavaScript, Python et Ruby. ReQL permet d'utiliser des fonctions côté serveur RethinkDB, par exemple, des jointures et des sous-requêtes réparties sur les noeuds du cluster. En outre, RethinkDB prend en charge des index secondaires permettant d'améliorer les performances des requêtes de lecture. La fonction la plus puissante de RethinkDB, changefeeds, permet de convertir un grand nombre de requêtes ReQL en flux en temps réel.
{:shortdesc}

**Remarque :** les instances de service Compose qui ont été mises à disposition avant le 14 septembre 2016 et qui sont toujours actives peuvent encore être utilisées et sont directement accessibles sur le site [https://www.compose.com/](https://www.compose.com). Les instances de service Compose mises à disposition depuis cette date sont directement accessibles et utilisables dans votre compte Bluemix.

Exécutez les étapes décrites ci-après pour commencer à utiliser {{site.data.keyword.composeForRethinkDB}}.

1. [Créez une instance {{site.data.keyword.composeForRethinkDB}}](https://console.ng.bluemix.net/catalog/services/compose-for-rethinkdb/).

  Lorsque vous créez une instance du service, prenez soin de sélectionner un nom pour votre service et un nom de données d'identification. Laissez le service non lié ; vous pourrez connecter une application à votre service ultérieurement en utilisant les données d'identification fournies lors de la mise à disposition du service. La section *Données d'identification disponibles* répertorie les différentes valeurs de données d'identification.

2. Connectez-vous au service {{site.data.keyword.composeForRethinkDB}}.

   Pour connecter une application à votre service, utilisez les
[données d'identification](./credentials.html) créées en même temps que
le service. Le modèle d'application montre comment utiliser Node.js pour établir une connexion au service {{site.data.keyword.composeForRethinkDB}}.

   Téléchargez le modèle d'application [compose-rethinkdb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rethinkdb-helloworld-nodejs) et suivez les instructions contenues dans le fichier Readme. Ensuite, cliquez sur **Afficher l'application** sur la page des détails d'application dans Bluemix.
