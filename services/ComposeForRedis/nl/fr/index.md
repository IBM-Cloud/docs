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

# Initiation à Compose for Redis
{: #getting-started-with-compose-for-redis}

Redis est un espace de stockage de paires clé-valeur en mémoire open source. Les valeurs Redis peuvent être des chaînes simples, des hachages, des listes, des jeux ou des bitmaps puissants, des journaux hyperlog et des index géospatiaux. Redis convient parfaitement en tant que cache d'applications ou magasin de données de réponse rapides. {{site.data.keyword.composeForRedis_full}} fournit une configuration préréglée pour la haute disponibilité et la persistance sur disque, le tout verrouillé avec des fonctions de sécurité supplémentaires.
{:shortdesc}

**Remarque :** les instances de service Compose qui ont été mises à disposition avant le 14 septembre 2016 et qui sont toujours actives peuvent encore être utilisées et sont directement accessibles sur le site [https://www.compose.com/](https://www.compose.com). Les instances de service Compose mises à disposition depuis cette date sont directement accessibles et utilisables dans votre compte Bluemix.

Exécutez les étapes décrites ci-après pour commencer à utiliser {{site.data.keyword.composeForRedis}}.

1. [Créez une instance {{site.data.keyword.composeForRedis}}](https://console.ng.bluemix.net/catalog/services/compose-for-redis/).

  Lorsque vous créez une instance du service, prenez soin de sélectionner un nom pour votre service et un nom de données d'identification. Laissez le service non lié ; vous pourrez connecter une application à votre service ultérieurement en utilisant les données d'identification fournies lors de la mise à disposition du service. La section *Données d'identification disponibles* répertorie les différentes valeurs de données d'identification.

2. Connectez-vous au service {{site.data.keyword.composeForRedis}}.

  Pour connecter une application à votre service, utilisez les
[données d'identification](./credentials.html) créées en même temps que
le service. Le modèle d'application montre comment utiliser Node.js pour établir une connexion au service {{site.data.keyword.composeForRedis}}.

  Téléchargez le modèle d'application [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs) et suivez les instructions contenues dans le fichier Readme. Ensuite, cliquez sur **Afficher l'application** sur la page des détails d'application dans Bluemix.
