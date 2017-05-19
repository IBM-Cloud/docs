---

copyright:
  years: 2016,2017
lastupdated: "2017-04-027"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Initiation à Compose for RabbitMQ
{: #getting-started-with-compose-for-rabbitmq}

RabbitMQ gère de façon asynchrone les messages qui transitent entre vos applications et des bases de données, permettant ainsi de séparer les données et les couches d'application. RabbitMQ permet aux développeurs d'acheminer, de suivre et de placer en file d'attente des messages avec des niveaux de persistance et des paramètres de distribution personnalisables, ainsi qu'une publication confirmée. {{site.data.keyword.composeForRabbitMQ_full}} vous permet d'accéder à l'interface d'administration conviviale avec un hôte de fonctions de gestion, telles que la surveillance du déploiement, la mise à l'échelle en un seul clic, la configuration utilisateur et l'accès aux fichiers journaux.
{:shortdesc}

**Remarque :** les instances de service Compose qui ont été mises à disposition avant le 14 septembre 2016 et qui sont toujours actives peuvent encore être utilisées et sont directement accessibles sur le site [https://www.compose.com/](https://www.compose.com). Les instances de service Compose mises à disposition depuis cette date sont directement accessibles et utilisables dans votre compte Bluemix.

Exécutez les étapes décrites ci-après pour commencer à utiliser {{site.data.keyword.composeForRabbitMQ}}.

1. [Créez une instance {{site.data.keyword.composeForRabbitMQ}}](https://console.ng.bluemix.net/catalog/services/compose-for-rabbitmq/).

  Lorsque vous créez une instance du service, prenez soin de sélectionner un nom pour votre service et un nom de données d'identification. Laissez le service non lié ; vous pourrez connecter une application à votre service ultérieurement en utilisant les données d'identification fournies lors de la mise à disposition du service.  La section *Données d'identification disponibles* répertorie les différentes valeurs de données d'identification.

2. Connectez-vous au service {{site.data.keyword.composeForRabbitMQ}}.

  Pour connecter une application à votre service, utilisez les
[données d'identification](./credentials.html) créées en même
temps que le
service. Le modèle d'application montre comment utiliser Node.js pour établir une connexion au service {{site.data.keyword.composeForRabbitMQ}}.

  Téléchargez le modèle d'application [compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs) et suivez les instructions contenues dans le fichier Readme. Ensuite, cliquez sur **Afficher l'application** sur la page des détails d'application dans Bluemix.
