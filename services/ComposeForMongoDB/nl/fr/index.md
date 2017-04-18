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

# Initiation à Compose for MongoDB
{: #getting-started-with-compose-for-mongodb}

{{site.data.keyword.composeForMongoDB_full}} utilise la prise en charge puissante d'indexation et d'interrogation, d'agrégation et de pilote étendu propre à MongoDB qui a fait de ce dernier le magasin de données JSON incontournable d'un grand nombre de startups et d'entreprises. {{site.data.keyword.composeForMongoDB}} fournit un système de déploiement de mise à l'échelle automatique facile à utiliser. Il offre haute des fonctions de haute disponibilité et de redondance, des sauvegardes sans interruption automatisées et à la demande, des outils de surveillance, l'intégration dans des systèmes d'alerte, des vues d'analyse de performance, etc., via une interface utilisateur simple et nette.
{:shortdesc}

**Remarque :** Les instances de service Compose qui ont été mises à disposition avant le 14 septembre 2016 et qui sont toujours actives peuvent encore être utilisées et sont directement accessibles sur le site [https://www.compose.com/](https://www.compose.com). Les instances de service Compose mises à disposition depuis cette date sont directement accessibles et utilisables dans votre compte Bluemix.

Exécutez les étapes décrites ci-dessous pour commencer à utiliser {{site.data.keyword.composeForMongoDB}} :

1. [Créez une instance {{site.data.keyword.composeForMongoDB}}](https://console.ng.bluemix.net/catalog/services/compose-for-mongodb/).

   Lorsque vous créez une instance du service, prenez soin de sélectionner un nom pour votre service et un nom de données d'identification. Laissez le service non lié ; vous pourrez connecter une application à votre service ultérieurement en utilisant les données d'identification fournies lors de la mise à disposition du service.  La section *Données d'identification disponibles* répertorie les différentes valeurs de données d'identification.

2. Connectez-vous au service {{site.data.keyword.composeForMongoDB}}.

   Pour connecter une application à votre service, utilisez les données d'identification créées en même temps que le service. L'exemple d'application montre comment utiliser Node.js pour établir une connexion au service {{site.data.keyword.composeForMongoDB}}.

   Téléchargez l'exemple d'application [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs) et suivez les instructions contenues dans le fichier Readme. Ensuite, cliquez sur **Afficher l'application** sur la page des détails d'application dans Bluemix.


## Données d'identification disponibles

Nom de zone|Description
----------|-----------
`uri`|URI à utiliser pour établir la connexion au service. `uri` comprend le schéma (`mongodb:`), le nom et le mot de passe administrateur, le nom d'hôte du serveur, le numéro de port auquel se connecter, le nom de base de données, ainsi que `?ssl=true` pour activer les connexions SSL.
`uri_cli`|Ligne de commande shell `mongo` qui permet d'établir la connexion à l'instance de base de données.
`ca_certificate_base64`|Certificat autosigné utilisé pour confirmer qu'une application se connecte bien au serveur approprié. Le certificat est codé en base64. Vous devez décoder la clé avant de l'utiliser, comme illustré dans l'exemple d'application.
`deployment_id`|Identificateur interne du service, créé dans Compose.
`db_type`|Type de base de données fourni par le service, en l'occurrence, `mongodb`.
`name`|Nom du déploiement de base de données.
{: caption="Table 1. {{site.data.keyword.composeForMongoDB}} credentials" caption-side="top"}

# Liens connexes
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose Articles](https://www.compose.com/articles/){:new_window}

## Tutoriels et exemples
{: #samples}
* [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs){:new_window}

## Liens connexes
{: #general}
* [Aide sur Compose](https://help.compose.com/docs){:new_window}
