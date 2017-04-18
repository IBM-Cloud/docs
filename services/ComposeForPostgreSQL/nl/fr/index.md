---

copyright:
  years: 2016
lastupdated: "2016-12-09"
---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be --- surrounded by 3 dashes ---
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Initiation à {{site.data.keyword.composeForPostgreSQL}}
{: #getting-started-with-compose-for-postgreSQL}

{{site.data.keyword.composeForPostgreSQL}} fournit une base de données relationnelle objet open source puissante hautement personnalisable. Postgres permet un développement rapide et facilement évolutif. Vous pouvez développer dans le langage que vous préférez, par exemple, C/C++, Perl, Python, TCL/TK, Delphi/Kylix, VB, PHP, ASP et Java. Vous disposez d'une base de données d'entreprise possédant de nombreuses fonctions grâce à la prise en charge JSON et vous obtenez ainsi le meilleur des environnements SQL et NoSQL.
{:shortdesc}

**Remarque :** Les instances de service Compose qui ont été mises à disposition avant le 14 septembre 2016 et qui sont toujours actives peuvent encore être utilisées et sont directement accessibles sur le site [https://www.compose.com/](https://www.compose.com). Les instances de service Compose mises à disposition depuis cette date sont directement accessibles et utilisables dans votre compte Bluemix.

Exécutez les étapes décrites ci-dessous pour commencer à utiliser Compose for PostgreSQL :

1. [Créez une instance {{site.data.keyword.composeForPostgreSQL}}](https://console.ng.bluemix.net/catalog/services/compose-for-postgresql/).

  Lorsque vous créez une instance du service, prenez soin de sélectionner un nom pour votre service et un nom de données d'identification. Laissez le service non lié ; vous pourrez connecter une application à votre service ultérieurement en utilisant les données d'identification fournies lors de la mise à disposition du service. La section *Données d'identification disponibles* répertorie les différentes valeurs de données d'identification.

2. Connectez-vous au service {{site.data.keyword.composeForPostgreSQL}}.

  Pour connecter une application à votre service, utilisez les données d'identification créées en même temps que le service. L'exemple d'application montre comment utiliser Node.js pour établir une connexion au service {{site.data.keyword.composeForPostgreSQL}}.

  Téléchargez l'exemple d'application [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs) et suivez les instructions contenues dans le fichier Readme. Ensuite, cliquez sur **Afficher l'application** sur la page des détails d'application pour afficher le contenu du tableau *Exemples*.

## Données d'identification disponibles

Nom de zone|Description
----------|-----------
`uri`|URI à utiliser pour établir la connexion au service. Comprend le schéma (`postgres:`), le nom et le mot de passe administrateur, le nom d'hôte du serveur, le numéro de port auquel se connecter, le nom de base de données, ainsi que "?ssl=true" pour activer les connexions SSL.
`uri_cli`|Ligne de commande shell `psql` qui permet d'établir la connexion à l'instance de base de données.
`ca_certificate_base64`|Certificat autosigné utilisé pour confirmer qu'une application se connecte bien au serveur approprié. Le certificat est codé en base64. Vous devez décoder la clé avant de l'utiliser, comme illustré dans l'exemple d'application.
`deployment_id`|Identificateur interne du service, créé dans Compose.
`db_type`|Type de base de données fourni par le service, en l'occurrence, `postgresql`.
`name`|Nom du déploiement de base de données.
{: caption="Table 1. {{site.data.keyword.composeForPostgreSQL}} credentials" caption-side="top"}

# Liens connexes
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose Articles](https://www.compose.com/articles/){:new_window}

## Tutoriels et exemples
{: #samples}
* [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs){:new_window}

## Liens connexes
{: #general}
* [Aide sur Compose](https://help.compose.com/docs){:new_window}
