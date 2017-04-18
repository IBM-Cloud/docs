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

# Initiation à {{site.data.keyword.composeForRabbitMQ}}
{: #getting-started-with-compose-for-rabbitmq}

RabbitMQ gère de façon asynchrone les messages qui transitent entre vos applications et des bases de données, permettant ainsi de séparer les données et les couches d'application. RabbitMQ permet aux développeurs d'acheminer, de suivre et de placer en file d'attente des messages avec des niveaux de persistance et des paramètres de distribution personnalisables, ainsi qu'une publication confirmée. {{site.data.keyword.composeForRabbitMQ_full}} vous permet d'accéder à l'interface d'administration conviviale avec un hôte de fonctions de gestion, telles que la surveillance du déploiement, la mise à l'échelle en un seul clic, la configuration utilisateur et l'accès aux fichiers journaux.
{:shortdesc}

**Remarque :** Les instances de service Compose qui ont été mises à disposition avant le 14 septembre 2016 et qui sont toujours actives peuvent encore être utilisées et sont directement accessibles sur le site [https://www.compose.com/](https://www.compose.com). Les instances de service Compose mises à disposition depuis cette date sont directement accessibles et utilisables dans votre compte Bluemix.

Exécutez les étapes décrites ci-après pour commencer à utiliser {{site.data.keyword.composeForRabbitMQ}}.

1. [Créez une instance {{site.data.keyword.composeForRabbitMQ}}](https://console.ng.bluemix.net/catalog/services/compose-for-rabbitmq/).

  Lorsque vous créez une instance du service, prenez soin de sélectionner un nom pour votre service et un nom de données d'identification. Laissez le service non lié ; vous pourrez connecter une application à votre service ultérieurement en utilisant les données d'identification fournies lors de la mise à disposition du service.  La section *Données d'identification disponibles* répertorie les différentes valeurs de données d'identification.

2. Connectez-vous au service {{site.data.keyword.composeForRabbitMQ}}.

  Pour connecter une application à votre service, utilisez les données d'identification créées en même temps que le service. L'exemple d'application montre comment utiliser Node.js pour établir une connexion au service {{site.data.keyword.composeForRabbitMQ}}.

  Téléchargez l'exemple d'application [compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs) et suivez les instructions contenues dans le fichier Readme. Ensuite, cliquez sur **Afficher l'application** sur la page des détails d'application dans Bluemix.

## Données d'identification disponibles

Nom de zone|Description
----------|-----------
``uri``|URI à utiliser pour établir la connexion au service. Comprend le schéma (`amqps:), le nom d'utilisateur et le mot de passe administrateur, le nom d'hôte du serveur, le numéro de port auquel se connecter et le nom vhost.
`uri_direct_1`|URI alternatif qui peut être utilisé lors de la connexion au service. Utilise le même format que `uri`.
`uri_admin`|URI qui doit être consulté dans un navigateur pour pouvoir accéder à l'interface d'administration de la base de données. Cet accès requiert le nom et le mot de passe administrateur indiqués dans la zone `uri`.
`uri_admin_1`|URI d'administration alternatif. Voir `uri_admin`.
`uri_admin_2`|URI d'administration alternatif. Voir `uri_admin`.
`uri_admin_3`|URI d'administration alternatif. Voir `uri_admin`.
`uri_admin_4`|URI d'administration alternatif. Voir `uri_admin`.
`ca_certificate_base64`|Certificat autosigné utilisé pour confirmer qu'une application se connecte bien au serveur approprié. Le certificat est codé en base64. Vous devez décoder la clé avant de l'utiliser, comme illustré dans l'exemple d'application.
`deployment_id`|Identificateur interne du service, créé dans Compose.
`db_type`|Type de base de données fourni par le service, en l'occurrence, `rabbitmq`.
`name`|Nom du déploiement de base de données.
{: caption="Table 1. {{site.data.keyword.composeForRabbitMQ}} credentials" caption-side="top"}

# Liens connexes
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose Articles](https://www.compose.com/articles/){:new_window}

## Tutoriels et exemples
{: #samples}
[compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs){:new_window}

## Liens connexes
{: #general}
* [Aide sur Compose](https://help.compose.com/docs){:new_window}
