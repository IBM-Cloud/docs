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

# Initiation à Compose for PostgreSQL
{: #getting-started-with-compose-for-postgreSQL}

{{site.data.keyword.composeForPostgreSQL}} fournit une base de données relationnelle objet open source puissante hautement personnalisable. Postgres permet un développement rapide et facilement évolutif. Vous pouvez développer dans le langage que vous préférez, par exemple, C/C++, Perl, Python, TCL/TK, Delphi/Kylix, VB, PHP, ASP et Java. Vous disposez d'une base de données d'entreprise possédant de nombreuses fonctions grâce à la prise en charge JSON et vous obtenez ainsi le meilleur des environnements SQL et NoSQL.
{:shortdesc}

**Remarque :** les instances de service Compose qui ont été mises à disposition avant le 14 septembre 2016 et qui sont toujours actives peuvent encore être utilisées et sont directement accessibles sur le site [https://www.compose.com/](https://www.compose.com). Les instances de service Compose mises à disposition depuis cette date sont directement accessibles et utilisables dans votre compte Bluemix.

Exécutez les étapes décrites ci-dessous pour commencer à utiliser Compose for PostgreSQL :

1. [Créez une instance {{site.data.keyword.composeForPostgreSQL}}](https://console.ng.bluemix.net/catalog/services/compose-for-postgresql/).

  Lorsque vous créez une instance du service, prenez soin de sélectionner un nom pour votre service et un nom de données d'identification. Laissez le service non lié ; vous pourrez connecter une application à votre service ultérieurement en utilisant les données d'identification fournies lors de la mise à disposition du service. La section *Données d'identification disponibles* répertorie les différentes valeurs de données d'identification.

2. Connectez-vous au service {{site.data.keyword.composeForPostgreSQL}}.

  Pour connecter une application à votre service, utilisez les
[données d'identification](./credentials.html) créées en même temps que
le service. Le modèle d'application montre comment utiliser Node.js pour établir une connexion au service {{site.data.keyword.composeForPostgreSQL}}.

  Téléchargez le modèle d'application [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs) et suivez les instructions contenues dans le fichier Readme. Ensuite, cliquez sur **Afficher l'application** sur la page des détails d'application pour afficher le contenu du tableau *Exemples*.
